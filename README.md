# Quantum Hardware Validation & Benchmarking Suite

An end-to-end suite for validating quantum backends against core quantum-mechanical principles and benchmarking real quantum processor performance — runs entirely on a local simulator by default, with a single flag to switch to real quantum hardware.

## Problem

Teams evaluating quantum hardware (IBM Quantum, IonQ, Quantinuum, Azure Quantum backends) need a reproducible way to answer two questions before committing compute budget or research time to a backend: **does it actually behave the way quantum mechanics predicts**, and **how does it perform against noise, decoherence, and error** compared to simulation and classical methods. This suite answers both with a single, swappable-backend pipeline instead of one-off scripts per provider.

## What this does

- **Schrödinger evolution validation**: simulates quantum systems and verifies time evolution, probability conservation, wavefunction normalization, and Hamiltonian dynamics against theoretical predictions.
- **Hardware benchmarking**: runs Bell states, GHZ states, randomized circuits, QFT, and variational circuits to measure gate fidelity, readout fidelity, T1/T2, circuit depth, latency, and measurement error.
- **Noise modeling**: implements depolarizing, bit-flip, phase-flip, readout, and thermal relaxation noise models; compares ideal simulator vs. noisy simulator vs. real hardware.
- **Error mitigation**: applies Zero Noise Extrapolation, Probabilistic Error Cancellation, Measurement Error Mitigation, and Clifford Data Regression, with before/after comparisons.
- **Quantum principles validation**: mathematically verifies the Born rule, state normalization, superposition, interference, entanglement, unitary evolution, no-cloning, and measurement collapse.
- **DiVincenzo criteria scorecard**: evaluates the backend against the DiVincenzo criteria (scalable qubits, initialization, coherence time, universal gate set, qubit-specific measurement, and — as a discussion — quantum communication and flying qubits).
- **Classical vs. quantum comparison**: benchmarks classical matrix simulation against quantum simulator and real hardware on runtime, memory, accuracy, scalability, and noise sensitivity.
- **Production-style architecture**: reusable, typed Python classes (`QuantumBackend`, `QuantumValidator`, `NoiseAnalyzer`, `HardwareBenchmark`, `ErrorMitigator`, `FidelityCalculator`, `VisualizationEngine`, `ReportGenerator`) rather than one-off notebook cells.
- **Hardware-agnostic**: fully implemented (but commented-out) integration code for IBM Quantum, Azure Quantum, IonQ, and Quantinuum — switch backends with a single `SIMULATOR = True/False` flag, no logic changes required.

## Architecture

```
Environment setup (Qiskit, Cirq, PennyLane, QuTiP, Mitiq)
        │
        ▼
Schrödinger evolution validation ──► theoretical vs. measured comparison
        │
        ▼
Hardware benchmarking (fidelity, T1/T2, latency, depth)
        │
        ▼
Noise modeling ──► ideal vs. noisy vs. real hardware
        │
        ▼
Error mitigation (ZNE, PEC, M3, CDR) ──► before/after comparison
        │
        ▼
Quantum principles validation + DiVincenzo scorecard
        │
        ▼
Classical vs. quantum benchmark ──► reports + dashboards
```

## Tech stack

- **Quantum frameworks**: Qiskit, Qiskit Aer, Cirq, PennyLane, QuTiP
- **Cloud backends** (swappable via `SIMULATOR` flag): IBM Quantum, Azure Quantum, IonQ, Quantinuum
- **Error mitigation**: Mitiq
- **Scientific computing**: NumPy, SciPy
- **Visualization**: Matplotlib, Plotly, Jupyter widgets

## Setup

```bash
git clone [repo-url]
cd quantum-hardware-validation-suite
pip install -r requirements.txt
```

By default the notebook runs entirely on `Qiskit Aer` simulators — no credentials required.

To run against real hardware, set:
```python
SIMULATOR = False
```
and uncomment the relevant authentication cell for your backend (IBM Quantum, Azure Quantum, IonQ, or Quantinuum). Credentials are read from environment variables, never hardcoded:
```
IBMQ_TOKEN=your_token
AZURE_QUANTUM_RESOURCE_ID=your_resource_id
IONQ_API_KEY=your_key
```

Run the notebook:
```bash
jupyter notebook quantum_hardware_validation.ipynb
```

## Results

| Benchmark | Ideal simulator | Noisy simulator | Real hardware |
|---|---|---|---|
| Gate fidelity | [ ] | [ ] | [ ] |
| Readout fidelity | [ ] | [ ] | [ ] |
| T1 | — | [ ] | [ ] |
| T2 | — | [ ] | [ ] |
| Circuit execution latency | [ ] | [ ] | [ ] |

| Error mitigation method | Fidelity before | Fidelity after |
|---|---|---|
| Zero Noise Extrapolation | [ ] | [ ] |
| Probabilistic Error Cancellation | [ ] | [ ] |
| Measurement Error Mitigation | [ ] | [ ] |
| Clifford Data Regression | [ ] | [ ] |

**DiVincenzo criteria scorecard**

| Criterion | Assessment |
|---|---|
| Scalable qubits | [ ] |
| Reliable initialization | [ ] |
| Long coherence times | [ ] |
| Universal gate set | [ ] |
| Qubit-specific measurement | [ ] |
| Quantum communication (discussion) | [ ] |
| Flying qubits (discussion) | [ ] |

## Guardrails & limitations

- All quantum-principle validations (Born rule, normalization, unitary evolution, no-cloning) include explicit mathematical checks, not just visual plots — results below tolerance thresholds are flagged, not silently passed.
- Noisy-simulator and real-hardware results are reported separately from ideal-simulator results at every stage; none are presented as equivalent.
- Real hardware access depends on provider queue times, availability, and account tier — the notebook is designed to run fully and meaningfully on simulators alone if hardware access is unavailable at run time.
- **This is a validation and benchmarking tool, not a claim of quantum advantage.** Current NISQ-era hardware remains noisy and limited in qubit count; the DiVincenzo scorecard and classical-vs-quantum comparison are included specifically to represent these limitations honestly rather than overstate backend capability.
- Credentials for any real backend are read from environment variables only and are never committed to the repository.

## Reports generated

- Quantum benchmarking report
- Fidelity report
- Noise analysis report
- DiVincenzo compliance report
- Schrödinger validation report
- Performance dashboard (interactive)

## Demo

[[Notebook walkthrough / dashboard link]](https://colab.research.google.com/drive/1Q4WiWIbFPz2OgDZPWh7A1ytc18tR2nkg?usp=sharing)

## License

MIT
