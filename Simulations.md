# Light as Logic: Simulating Photonic Qubits with Qiskit

## Abstract

Photonic qubits—qubits based on the quantum properties of light—offer unique advantages such as low decoherence and fast transmission. In this study, we simulate a photonic qubit using the Qiskit quantum computing framework. Specifically, we demonstrate how the quantum superposition state created by a Hadamard gate mirrors the behavior of a light wave passing through a beam splitter. By plotting measurement outcomes of the qubit in superposition, we reveal a strong analogy between probability amplitudes in quantum states and the intensity of electromagnetic waves. This simulation confirms that even with basic computational tools, core concepts of photonic quantum computing can be explored and validated.

---

## 1. Introduction

Quantum computing is not limited to superconductors or trapped ions. Photons—the fundamental particles of light—are compelling candidates for qubit implementation due to their natural behavior as quantum wave packets. In this paper, we simulate basic photonic qubit behavior using Qiskit and analyze it through the lens of electromagnetic wave properties: **amplitude**, **phase**, and **polarization**.

The experiment focuses on a qubit placed in superposition and measured multiple times. This emulates a photon split into two paths with equal probability, akin to interference in a Mach-Zehnder interferometer.

---

## 2. Theoretical Background

### A qubit in superposition is represented as:
|ψ⟩ = α|0⟩ + β|1⟩

### For a Hadamard gate applied to `|0⟩`, the result becomes:
|ψ⟩ = (1/√2)(|0⟩ + |1⟩)

This is directly comparable to a photon encountering a 50/50 beam splitter and having equal probability of being transmitted or reflected.

### Light-Wave Analogy

| Quantum Concept       | Light Equivalent         |
|-----------------------|--------------------------|
| Probability Amplitude | Wave Amplitude           |
| Phase (φ)             | Phase of EM wave         |
| Qubit Basis           | Polarization (H/V)       |

---

## 3. Qiskit Simulation: Superposition of a Photon Qubit

This code simulates a **single qubit** placed in superposition using a **Hadamard gate** and then measures the qubit. This mimics a photon that can take two polarization states or two paths after a beam splitter.

```python
# This script simulates a single qubit in superposition using Qiskit.
# It applies a Hadamard gate to put the qubit into a superposition state,
# measures it, and then plots the measurement results.

# Required imports for quantum circuit creation, simulation, and visualization.
# Aer is now imported from qiskit_aer in newer Qiskit versions.
from qiskit import QuantumCircuit, transpile
from qiskit_aer import Aer # Corrected import for Aer
from qiskit.visualization import plot_histogram
from matplotlib import pyplot as plt

# Step 1: Create a quantum circuit with one qubit and one classical bit.
# The qubit (index 0) will hold the quantum information.
# The classical bit (index 0) will store the measurement result.
qc = QuantumCircuit(1, 1)

# Step 2: Apply the Hadamard gate to the qubit.
# The Hadamard gate (H) puts the qubit into a superposition of |0⟩ and |1⟩.
# After this, the qubit has an equal probability of being measured as 0 or 1.
qc.h(0)

# Step 3: Measure the qubit and store the result in the classical bit.
# qc.measure(qubit_index, classical_bit_index)
qc.measure(0, 0)

# Step 4: Simulate the quantum circuit using the 'qasm_simulator'.
# The 'qasm_simulator' is a local simulator that mimics a real quantum computer
# by performing measurements and returning counts of outcomes.

# Get the simulator backend.
simulator = Aer.get_backend('qasm_simulator')

# Transpile the circuit for the chosen simulator.
# Transpilation optimizes the circuit for the target backend.
compiled_circuit = transpile(qc, simulator)

# Run the transpiled circuit on the simulator.
# We specify 'shots=1024' to run the circuit 1024 times to get statistical results.
# The .result() method retrieves the simulation results.
result = simulator.run(compiled_circuit, shots=1024).result()

# Step 5: Get the measurement counts and plot them.
# The get_counts() method returns a dictionary where keys are the measurement
# outcomes (e.g., '0' or '1') and values are the number of times each outcome occurred.
counts = result.get_counts()

# Create a Matplotlib figure and axes explicitly.
fig, ax = plt.subplots(figsize=(7, 5))

# Plot a histogram of the measurement results onto the created axes.
# This will visually show the probabilities of measuring 0 or 1.
# Changed the color of the histogram bars to blue.
plot_histogram(counts, ax=ax, color='blue')

# Set the title for the plot to clearly describe what it represents.
ax.set_title("Qubit in Superposition (|0⟩ + |1⟩) Measured")

# Save the plot to a file.
# This line is now uncommented to ensure the histogram is always saved.
# You can then open 'superposition_histogram.png' to view the plot.
plt.savefig('superposition_histogram.png')

# Display the plot.
# This might not work in all environments, in which case saving to file is recommended.
plt.show()

# Optional: Print the measurement counts to the console.
print("Measurement Counts:", counts)
```
##  4. Results and Interpretation
Measurement Counts: {'0': 539, '1': 485}
![image](https://github.com/user-attachments/assets/7b369756-7599-4f04-ba49-38d5675292ff)

This matches the expected 50/50 split from a Hadamard gate, proving that the qubit behaves like a wave—random collapse upon measurement.
Outcome	Count	Meaning
0	539	Photon detected in polarization path A
1	485	Photon detected in polarization path B

## 5. Significance of This Simulation
This simulation proves:

Qubits in superposition can be modeled with light wave concepts

You can simulate photon behavior without quantum hardware

Amplitude = Probability, Phase = Interference control

Can be extended to beam splitters, interferometers, polarization gates

## 6. Future Work
Future work includes:

Simulating Bell states using photon entanglement

Implementing quantum teleportation with polarized photons

Simulating Mach-Zehnder Interferometers

Adding polarization phase shifters and beam splitters

Visualizing interference patterns

## 7. Conclusion
The behavior of light waves—especially superposition, phase shift, and polarization—mirrors qubit
properties in quantum computing. This research demonstrates that light-based qubits are not just a theory,
but simulatable and visualizable using tools like Qiskit. This bridges quantum physics with classical optics 
and opens doors for further research into photonic quantum logic.

##  Author
Muhammad Abrar


