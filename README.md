# FHE Accelerator Simulators

How long does a CKKS bootstrap take on a given accelerator? Is the design bound by NTT throughput or by evaluation-key traffic? How much on-chip SRAM stops key traffic dominating, and does an optical NTT engine win once conversion energy and precision corrections are counted? Five interactive decks and a tested SimPy simulator work through these questions. They run from CKKS as a hardware workload and the anatomy of bootstrapping, through the simulator itself (**live in the browser**, a bit-exact JavaScript port) and optical transform engines, to design-space results, a reading list and practice questions.

**Live index:** https://brendanjameslynskey.github.io/FHE_Hub_Accelerator_Simulators/

## Presentations in this series

| # | Title | Status | What it covers |
|---|-------|--------|----------------|
| 01 | [FHE for Hardware Engineers: CKKS as a Workload](https://brendanjameslynskey.github.io/FHESim_01_FHE_for_Hardware_Engineers/) | live | CKKS seen from the datapath, not the proof: RNS polynomials in Zq[X]/(XN+1), how big ciphertexts and evaluation keys really are, the five primitive kernels (NTT, modular multiply-add, automorphism, base conversion, rescale), noise and levels, and why key switching dominates. Includes a live parameter calculator. |
| 02 | [Anatomy of CKKS Bootstrapping](https://brendanjameslynskey.github.io/FHESim_02_Anatomy_of_Bootstrapping/) | live | ModRaise, CoeffToSlot (a homomorphic DFT evaluated with baby-step giant-step rotations), EvalMod (a polynomial approximation of modular reduction) and SlotToCoeff, with exact operation counts per stage, where the levels go, and the data-movement profile that makes bootstrapping a memory problem. |
| 03 | [Simulating an FHE Accelerator](https://brendanjameslynskey.github.io/FHESim_03_Simulating_an_FHE_Accelerator/) | live | The modelled machine (NTT units, modular multiply-add lanes, an automorphism network, a scratchpad, HBM and key streaming), the operation-trace format and where traces come from (a scheme model, HEIR, OpenFHE), the SimPy engine, its metrics and its validation ladder, and the whole simulator running live in the browser. |
| 04 | [Optical NTT Engines: Precision, Conversion and Power](https://brendanjameslynskey.github.io/FHESim_04_Optical_NTT_Engines/) | live | Fourier transforms in optics, and what it takes to map an exact modular NTT onto an analogue complex FFT: digit decomposition, small-prime RNS, rounding and error correction, ENOB, DAC/ADC energy from a Walden figure of merit, and laser and thermal-tuning power. The simulator then shows when an optical engine wins and when it loses. |
| 05 | [Results and the Design Space](https://brendanjameslynskey.github.io/FHESim_05_Results_and_Design_Space/) | live | What the simulator says: SRAM size against key traffic, the NTT-bound and memory-bound regimes, power and energy per bootstrap under a TDP, the algorithmic acceleration techniques, a design-space sweep, the model's limitations, a reading list (F1, CraterLake, BTS, ARK, SHARP, GPU work, HEIR, OpenFHE, Lattigo) and practice questions. |

## Companion code

| Repo | What's inside |
|------|---------------|
| [FHE_Accelerator_Sim](https://github.com/BrendanJamesLynskey/FHE_Accelerator_Sim) | A SimPy discrete-event simulator of an FHE accelerator running CKKS bootstrapping: a scheme model that turns bootstrapping into NTT, base-conversion, multiply-add and automorphism kernels; NTT, MAC, automorphism and optional optical units; a scratchpad whose misses become evaluation-key, plaintext and ciphertext traffic over shared HBM; bound attribution, hot-spots, Perfetto traces; a power model with a dynamic power manager under a TDP, and DVFS; an optical precision model with a functional check; OpenFHE calibration and two recorded OpenFHE bootstrap traces it replays; 74 tests; and the JavaScript port used live in deck 03. |

## How to read this series

Decks 01 and 02 cover what is being simulated: CKKS as a workload, and bootstrapping stage by stage. Deck 03 is the simulator, its trace format, metrics and validation, with the live port. Deck 04 examines optical NTT engines. Deck 05 collects the results, the limitations, a reading list and practice questions. All hardware coefficients in the simulator are illustrative, and every number in the decks comes from a recorded run (`examples/results.py` in the code repo).

## Where this fits

* **FHE fundamentals:** the [Cryptography section](https://github.com/BrendanJamesLynskey/Mathematics#cryptography) of the Mathematics hub, especially [Cryptography 08: Fully Homomorphic Encryption](https://brendanjameslynskey.github.io/Cryptography/08-fully-homomorphic-encryption/) and [Cryptography 10: Crypto Hardware Accelerator Design](https://brendanjameslynskey.github.io/Cryptography/10-crypto-hardware-accelerator-design/).
* **Simulator methodology:** the sister series [LLM Inference Simulators](https://github.com/BrendanJamesLynskey/LLM_Hub_Inference_Simulators) (discrete-event simulation, metrics and validation, power and energy, accelerating simulators, PyTorch/ONNX/HEIR integration). Its code repo, [Disaggregated_Inference_Sim](https://github.com/BrendanJamesLynskey/Disaggregated_Inference_Sim), is the template this one follows.
* Indexed from the [Hardware hub](https://github.com/BrendanJamesLynskey/Hardware).
