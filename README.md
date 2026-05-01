# Emerging Technologies Assessment

This repository contains my submission for the **Emerging Technologies, Summer 25/26** assessment.

The assessment explores the difference between classical and quantum algorithms through Boolean functions, Deutsch's algorithm, and the Deutsch-Jozsa algorithm. The main work is contained in [`problems.ipynb`](problems.ipynb), which implements and explains each of the five required problems using Python and Qiskit.

## Repository Contents

| File | Description |
| --- | --- |
| `README.md` | Overview of the repository and setup instructions. |
| `problems.ipynb` | Main assessment notebook containing all five completed problems. |
| `requirements.txt` | Python packages required to run the notebook. |
| `.gitignore` | Excludes unnecessary local, cache, and temporary files from version control. |

## Assessment Problems Covered

### Problem 1: Generating Random Boolean Functions

Implements `random_constant_balanced`, a Python function that randomly creates a four-input Boolean function guaranteed to be either:

- **constant**, where every input maps to the same output; or
- **balanced**, where exactly half of the sixteen possible inputs return `0` and the other half return `1`.

The notebook represents each generated function through a truth table lookup, making the behaviour easy to test and verify.

### Problem 2: Classical Testing for Function Type

Implements `determine_constant_balanced`, which classifies a four-bit Boolean function as either `"constant"` or `"balanced"`.

This section explains the classical query cost. Since a four-bit function has sixteen possible inputs, a classical deterministic algorithm may need up to:

```text
2^(n-1) + 1 = 9 calls
```

to be certain whether the function is constant or balanced.

### Problem 3: Quantum Oracles

Uses Qiskit to construct the four possible one-bit Deutsch oracles:

| Function | Type | Oracle behaviour |
| --- | --- | --- |
| `f(x) = 0` | Constant | Leaves the output qubit unchanged. |
| `f(x) = 1` | Constant | Flips the output qubit. |
| `f(x) = x` | Balanced | Applies a controlled flip from input to output. |
| `f(x) = ¬x` | Balanced | Combines controlled and unconditional flips to represent NOT behaviour. |

The notebook demonstrates each oracle and explains how it implements the mapping:

```text
|x, y⟩ → |x, y ⊕ f(x)⟩
```

### Problem 4: Deutsch's Algorithm with Qiskit

Builds the full Deutsch circuit using the oracles from Problem 3.

The notebook shows how the circuit:

1. prepares the input and output qubits,
2. applies Hadamard gates to create superposition,
3. queries the oracle once,
4. applies interference using a final Hadamard gate, and
5. measures the input qubit to classify the function.

The final result is interpreted as:

| Measurement | Classification |
| --- | --- |
| `0` | Constant |
| `1` | Balanced |

### Problem 5: Scaling to the Deutsch-Jozsa Algorithm

Extends the single-bit Deutsch algorithm to the four-bit Deutsch-Jozsa case.

The notebook builds a circuit with:

- four input qubits; and
- one ancilla/output qubit.

It encodes classical four-bit Boolean functions as quantum oracles and demonstrates the circuit on:

- both constant functions; and
- two selected balanced functions.

The result is interpreted as:

| Measurement | Classification |
| --- | --- |
| `0000` | Constant |
| Any other bitstring | Balanced |

## Technologies Used

- Python
- Jupyter Notebook
- Qiskit
- Qiskit Aer
- Standard Python libraries such as `random` and `itertools`

## Setup Instructions

These instructions assume that Python is already installed.

### 1. Clone the repository

```bash
git clone https://github.com/sarahoconnor10/EmergingTech.git
cd EmergingTech
```

### 2. Create and activate a virtual environment

#### macOS / Linux

```bash
python3 -m venv .venv
source .venv/bin/activate
```

#### Windows

```bash
python -m venv .venv
.venv\Scripts\activate
```

### 3. Install dependencies

```bash
pip install -r requirements.txt
```

### 4. Open the notebook

```bash
jupyter notebook problems.ipynb
```

Alternatively, the notebook can be opened in JupyterLab:

```bash
jupyter lab
```

## References and Learning Resources

The notebook refers to supporting documentation and learning material, including:

- IBM Quantum Learning material on Deutsch's algorithm and the Deutsch-Jozsa algorithm.
- Qiskit documentation for creating and simulating quantum circuits.
- Python documentation and PEP8 guidance for clean, readable code.
- Module notes and lecture material on the Deutsch-Jozsa algorithm.

References are included in context throughout the notebook where they support the explanation or implementation.

## Author

Sarah O'Connor  
Student ID: G00423847  
BSc (Hons) in Computing in Software Development  
Atlantic Technological University
