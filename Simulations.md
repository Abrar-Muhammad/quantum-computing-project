![image](https://github.com/user-attachments/assets/51fe0aca-2368-4a03-8e3a-87f3a3b2aa43)# Light as Logic: Simulating Photonic Qubits with Qiskit

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




## Quantum Entanglement Using Light: Bell State with Polarization

One of the most profound phenomena in quantum mechanics is **entanglement**—a state where two qubits are linked such that measuring one instantly determines the state of the other, even if they are far apart. In our research using light as a medium for quantum logic, we simulate entanglement through the creation of a **Bell state** using Qiskit.

### Mapping to Light and Polarization

In photonic quantum computing, qubits can be encoded using **polarization**:

| Qubit Basis | Polarization       |
|-------------|--------------------|
| \|0⟩         | Horizontal (H)     |
| \|1⟩         | Vertical (V)       |


Thus, a Bell state:

|Φ⁺⟩ = (1/√2) × (|HH⟩ + |VV⟩)

…is the light equivalent of:

|Φ⁺⟩ = (1/√2) × (|00⟩ + |11⟩)

This state implies that both photons are **always polarized the same way**—either both `H` (horizontal) or both `V` (vertical). No case of one `H` and one `V` is possible.

---

### Bell State Simulation Results

We created this entangled state using Qiskit, and the measurement histogram confirmed the result:

![image](https://github.com/user-attachments/assets/12bc2e06-43c2-477b-af74-dec8649e8ae0)


✅ This shows perfect entanglement: **only `00` and `11` appeared**, with no `01` or `10`.

---

### Code to Reproduce This Simulation

````python
# This script simulates a Bell state (entangled qubits) using Qiskit.
# It creates a Bell pair, measures both qubits, and then plots the measurement results.

# STEP 1: Import necessary libraries
from qiskit import QuantumCircuit, transpile
from qiskit_aer import Aer
from qiskit.visualization import plot_histogram
from matplotlib import pyplot as plt

# STEP 2: Create a circuit with 2 qubits and 2 classical bits
# Qubit 0 and Qubit 1 will be entangled.
# Classical bits 0 and 1 will store their respective measurement results.
qc = QuantumCircuit(2, 2)

# STEP 3: Create entanglement (Bell pair)
# Apply Hadamard gate on Qubit 0: This puts Qubit 0 into a superposition
# of |0⟩ and |1⟩.
qc.h(0)

# Apply Controlled-NOT (CNOT) gate with Qubit 0 as control and Qubit 1 as target.
# This entangles Qubit 0 with Qubit 1. If Qubit 0 is |0⟩, Qubit 1 remains |0⟩.
# If Qubit 0 is |1⟩, Qubit 1 flips to |1⟩.
# The resulting state is a superposition of |00⟩ and |11⟩.
qc.cx(0, 1)

# STEP 4: Measure both qubits
# Measure Qubit 0 and store the result in Classical Bit 0.
qc.measure(0, 0)
# Measure Qubit 1 and store the result in Classical Bit 1.
qc.measure(1, 1)

# STEP 5: Run simulation
# Get the 'qasm_simulator' backend from Qiskit Aer.
simulator = Aer.get_backend('qasm_simulator')

# Transpile the circuit for the simulator. This optimizes the circuit for the backend.
compiled = transpile(qc, simulator)

# Run the compiled circuit on the simulator for 1024 shots.
# 'shots' determines how many times the circuit is run to gather statistics.
result = simulator.run(compiled, shots=1024).result()

# Get the measurement counts from the simulation result.
# 'counts' will be a dictionary, e.g., {'00': 510, '11': 514}.
counts = result.get_counts()

# STEP 6: Plot histogram
# Create a Matplotlib figure and axes explicitly for better control.
fig, ax = plt.subplots(figsize=(7,5))

# Plot the histogram using Qiskit's plot_histogram function.
# 'ax=ax' directs the plot to our specific axes.
# 'color='blue'' sets the bar color to blue.
# 'bar_labels=True' adds numerical labels on top of the bars.
plot_histogram(counts, ax=ax, color='blue', bar_labels=True)

# Set the title for the plot.
ax.set_title("Bell State Measurement Results")

# Add a grid to the plot for better readability.
ax.grid(True)

# Save the plot to a file. This is crucial for viewing the output
# if plt.show() doesn't work in your environment.
# The image will be saved as 'bell_state_histogram.png' in the same directory.
plt.savefig('bell_state_histogram.png')

# Display the plot. This will attempt to open an interactive plot window.
# If it doesn't appear, please check the 'bell_state_histogram.png' file.
plt.show()

# STEP 7: Print result
# Print the raw measurement counts to the console.
print("Measurement Counts:", counts)


````
## Interpretation and Connection to Light
This simulation provides strong support for our theoretical idea: light waves—specifically polarization states—can accurately represent quantum entanglement. The results align with experimental photonic entanglement, proving that photonic qubits behave according to quantum mechanical predictions.

##  Author
Muhammad Abrar




# How These Simulations Prove Light Can Be Used as Qubits
We ran two quantum simulations:

1 Superposition Simulation using a Hadamard gate

2 Entanglement Simulation (Bell Pair) using H + CNOT

Let’s understand how each of them reflects the behavior of light (EM waves) and how this supports your theory that light can represent qubits.

## Superposition Simulation & Light
###  Quantum Part:
You applied a Hadamard (H) gate, putting a qubit into:
|ψ⟩ = (1/√2) × (|H⟩ + |V⟩)
Measured output:
   {'0': 492, '1': 532}
###  Light-Wave Equivalent:
A photon can be polarized in different directions.

Superposition in light = Diagonal polarization (mix of horizontal + vertical).

Just like your simulation outputs both |0⟩ and |1⟩ randomly, a diagonally polarized photon will randomly be measured as H or V — just like your simulated qubit.
### Conclusion:
This proves a single photon's polarization behaves like a quantum qubit in superposition.

## Entanglement (Bell Pair) & Light
###  Quantum Part:
You created a Bell state:
|Φ⁺⟩ = (1/√2) × (|00⟩ + |11⟩)
Measured output:
{'00': 490, '11': 534}
Only outputs 00 or 11 — perfect entanglement.

###  Light-Wave Equivalent:
Two entangled photons (e.g., from SPDC — Spontaneous Parametric Down Conversion) are created with linked polarizations.

If one photon is measured as Horizontally polarized, the other is always Horizontal.

If one is Vertical, the other is too.

This is exactly what your simulation shows — both qubits measured as 0 or both as 1.

###  Conclusion:
 Simulation matches experimental photon entanglement behavior. This supports using polarization of light as qubit encoding.

 ## This proves:
  Light (photons) can simulate real qubit behavior
  Polarization, amplitude, and phase can encode quantum information
  Your simulation is a theoretical + visual proof that light can be used for quantum logic


  # GHZ State Simulation (Tripartite Entanglement)

In classical systems, it's impossible to link three particles in a way that all their values are always correlated without directly communicating. However, in quantum mechanics, this becomes possible through **GHZ states**.

A **GHZ (Greenberger–Horne–Zeilinger) state** is a special 3-qubit entangled state where all qubits behave as one — even when separated by large distances.

###  GHZ State Formula

 |GHZ⟩ = (1/√2) × (|000⟩ + |111⟩)
 
This formula means:
- The system is in a **superposition** of all three qubits being `0` or all being `1`
- If you measure one qubit, you instantly know the value of the others
- This is a **quantum-only** behavior — no classical system can do this

### Quantum Circuit Logic

To create a GHZ state, we apply:
- A **Hadamard (H)** gate to qubit 0 to create superposition
- Then two **CNOT** gates to entangle qubit 0 with qubit 1 and qubit 2

### Simulation Output

When simulated using Qiskit, the histogram will mostly show two states:

- `000` → all qubits measured as 0  
- `111` → all qubits measured as 1

This proves that the qubits are **entangled**, not behaving independently.

---

### Code Block (Qiskit GHZ Simulation)

```python
# This script simulates a 3-qubit GHZ (Greenberger–Horne–Zeilinger) state using Qiskit.
# It creates a GHZ state, measures all three qubits, and then plots the measurement results.
!pip install qiskit qiskit-aer --upgrade
# The GHZ state is a type of entangled quantum state involving three or more qubits,
# often represented as:
# $$
# |\psi\rangle = \frac{1}{\sqrt{2}} (|000\rangle + |111\rangle)
# $$
# This state demonstrates strong quantum correlations between all three qubits.

# STEP 1: Import necessary libraries
from qiskit import QuantumCircuit, transpile
from qiskit_aer import Aer
from qiskit.visualization import plot_histogram
from matplotlib import pyplot as plt

# STEP 2: Create a circuit with 3 qubits and 3 classical bits
# Qubits 0, 1, and 2 will be entangled to form the GHZ state.
# Classical bits 0, 1, and 2 will store their respective measurement results.
qc = QuantumCircuit(3, 3)

# STEP 3: Create entanglement (GHZ state)
# Put qubit 0 in superposition using a Hadamard gate.
# This creates a state like ( |0⟩ + |1⟩ ) / √2 for qubit 0.
qc.h(0)

# Entangle qubit 0 with qubit 1 using a Controlled-NOT (CNOT) gate.
# If qubit 0 is |0⟩, qubit 1 remains |0⟩. If qubit 0 is |1⟩, qubit 1 flips to |1⟩.
# The state becomes ( |00⟩ + |11⟩ ) / √2 for qubits 0 and 1.
qc.cx(0, 1)

# Entangle qubit 0 with qubit 2 using another CNOT gate.
# This extends the entanglement to qubit 2.
# The final state becomes the GHZ state: ( |000⟩ + |111⟩ ) / √2.
qc.cx(0, 2)

# STEP 4: Measure all qubits
# Measure all 3 qubits and map their results to their corresponding classical bits.
qc.measure([0, 1, 2], [0, 1, 2])

# STEP 5: Run simulation
# Get the 'qasm_simulator' backend from Qiskit Aer.
simulator = Aer.get_backend('qasm_simulator')

# Transpile the circuit for the simulator. This optimizes the circuit for the backend.
compiled = transpile(qc, simulator)

# Run the compiled circuit on the simulator for 1024 shots.
# 'shots' determines how many times the circuit is run to gather statistics.
result = simulator.run(compiled, shots=1024).result()

# Get the measurement counts from the simulation result.
# 'counts' will be a dictionary, e.g., {'000': 505, '111': 519}.
counts = result.get_counts()

# STEP 6: Plot histogram
# Create a Matplotlib figure and axes explicitly for better control over the plot.
fig, ax = plt.subplots(figsize=(8, 6)) # Increased figure size for 3 qubits

# Plot the histogram using Qiskit's plot_histogram function.
# 'ax=ax' directs the plot to our specific axes.
# 'color='blue'' sets the bar color to blue.
# 'bar_labels=True' adds numerical labels on top of the bars for clarity.
plot_histogram(counts, ax=ax, color='blue', bar_labels=True)

# Set the title for the plot.
ax.set_title("3-Qubit GHZ State: (|000⟩ + |111⟩) / √2")

# Add a grid to the plot for better readability.
ax.grid(True)

# Save the plot to a file. This is crucial for viewing the output
# if plt.show() doesn't work in your environment.
# The image will be saved as 'ghz_state_histogram.png' in the same directory.
plt.savefig('ghz_state_histogram.png')

# Display the plot. This will attempt to open an interactive plot window.
# If it doesn't appear, please check the 'ghz_state_histogram.png' file.
plt.show()

# STEP 7: Print result
# Print the raw measurement counts to the console.
print("Counts:", counts)
```
### Result 
![image](https://github.com/user-attachments/assets/956ef4f8-bf9b-4397-a5a5-9b0b6a9b79c4)

This experiment supports the core idea of this research — that quantum entanglement, such as in a GHZ state, can potentially be implemented using photonic systems (light waves), where coherence and synchronization can mimic multi-qubit behavior.


# Quantum Teleportation Simulation (3-Qubit Protocol)

Quantum teleportation is one of the most powerful demonstrations of quantum mechanics. It allows you to **transfer a quantum state** from one qubit to another — **without physically moving** the qubit itself.

This process uses:
- **Entanglement** between two qubits
- **Classical communication**
- **Quantum gates (CNOT, H)**

### Concept

A quantum state (like a superposition) can be "teleported" from one qubit (Alice) to another (Bob), using a third helper qubit and a Bell pair.

This is done using:
1. **Entangled pair**: Shared between Alice and Bob
2. **CNOT + H gates**: Applied by Alice to entangle her qubit with the entangled pair
3. **Measurements + classical communication**
4. **Conditional gates** on Bob’s side to reconstruct the original state

### 📎 Initial State

 |ψ⟩ = α|0⟩ + β|1⟩

 
This is the unknown state to be teleported.

After running the teleportation protocol, **qubit 2 (Bob)** ends up in the same quantum state as **qubit 0 (Alice)** had originally — even though the qubit wasn’t sent directly.

---

### ⚙️ Quantum Circuit Summary

- Qubit 0: The qubit to be teleported (prepared in superposition)
- Qubit 1 & 2: Entangled Bell pair
- Qubits 0 and 1 are measured
- Results are used to conditionally rotate qubit 2
- Final measurement confirms teleportation

---

### 🧪 Expected Result

After the circuit runs:
- The **state of qubit 0** will be recreated **on qubit 2**
- Qubit 0 and 1 are discarded after measurement
- **Qubit 2 holds the teleported state**

---

### Code Block (Qiskit Quantum Teleportation)

```python
# This script simulates a basic Quantum Teleportation protocol using Qiskit.
# It demonstrates how the state of one qubit (sender's) can be transferred
# to another qubit (receiver's) using entanglement and classical communication.

# The core idea of quantum teleportation is to transfer an unknown quantum state
# from a sender to a receiver, without physically moving the qubit itself.
# This relies on:
# 1. An entangled pair (Bell pair) shared between sender and receiver.
# 2. Classical communication of measurement results from sender to receiver.

# STEP 1: Import necessary libraries
from qiskit import QuantumCircuit, transpile
from qiskit_aer import Aer
from qiskit.visualization import plot_histogram # Removed plot_bloch_multivector as it's not used
# from qiskit.quantum_info import Statevector # Removed Statevector as it's not directly used for this simulation
from matplotlib import pyplot as plt

# Create a 3-qubit circuit with 3 classical bits for measurement
# Qubit 0: Sender's qubit (state to be teleported)
# Qubit 1: Sender's part of the Bell pair
# Qubit 2: Receiver's part of the Bell pair
qc = QuantumCircuit(3, 3)

# STEP 2: Prepare sender's qubit (qubit 0) in an arbitrary state.
# For demonstration, we'll put it in a superposition state using a Hadamard gate.
# This is the unknown state $|\psi\rangle$ that we want to teleport.
qc.h(0)
# You could also apply other gates here to set a different initial state, e.g.:
# qc.rx(theta, 0) # Rotate around X-axis
# qc.ry(phi, 0)   # Rotate around Y-axis

# STEP 3: Create Bell pair between qubit 1 and 2.
# This entangled pair is shared between the sender (qubit 1) and receiver (qubit 2).
qc.h(1)  # Put qubit 1 in superposition
qc.cx(1, 2) # Entangle qubit 1 with qubit 2 (Bell state: (|00⟩ + |11⟩) / √2)

# Add a barrier to separate preparation steps visually in the circuit diagram (optional)
qc.barrier()

# STEP 4: Entangle sender's qubit (0) with their part of the Bell pair (1).
qc.cx(0, 1) # CNOT gate with qubit 0 as control, qubit 1 as target
qc.h(0)   # Hadamard gate on qubit 0

# Add a barrier before measurement (optional)
qc.barrier()

# STEP 5: Measure qubit 0 and 1 (sender's qubits).
# The results of these measurements are classical bits that will be sent to the receiver.
qc.measure([0, 1], [0, 1])

# Add a barrier after sender's measurements (optional)
qc.barrier()

# STEP 6: Apply conditional gates to qubit 2 (receiver).
# The receiver applies gates to their qubit (qubit 2) based on the classical
# measurement results received from the sender.
# If classical bit 1 is 1, apply X gate to qubit 2.
qc.cx(1, 2) # CNOT with classical bit 1 as control, qubit 2 as target
# If classical bit 0 is 1, apply Z gate to qubit 2.
qc.cz(0, 2) # Controlled-Z with classical bit 0 as control, qubit 2 as target

# STEP 7: Measure final qubit (qubit 2) at the receiver's end.
# The state of qubit 2 should now be the teleported state from qubit 0.
qc.measure(2, 2)

# STEP 8: Simulate the quantum circuit.
sim = Aer.get_backend('qasm_simulator')
compiled = transpile(qc, sim)
result = sim.run(compiled, shots=1024).result()
counts = result.get_counts()

# STEP 9: Plot histogram of results.
# Create a Matplotlib figure and axes explicitly for better control.
fig, ax = plt.subplots(figsize=(8, 6))

# Plot the histogram using Qiskit's plot_histogram function.
# 'ax=ax' directs the plot to our specific axes.
# 'color='blue'' sets the bar color to blue.
# 'bar_labels=True' adds numerical labels on top of the bars for clarity.
plot_histogram(counts, ax=ax, color='blue', bar_labels=True)

# Set the title for the plot.
ax.set_title("Quantum Teleportation Output (Qubit 0 ➝ Qubit 2)")

# Add a grid to the plot for better readability.
ax.grid(True)

# Save the plot to a file. This is crucial for viewing the output
# if plt.show() doesn't work in your environment.
# The image will be saved as 'quantum_teleportation_histogram.png' in the same directory.
plt.savefig('quantum_teleportation_histogram.png')

# Display the plot. This will attempt to open an interactive plot window.
# If it doesn't appear, please check the 'quantum_teleportation_histogram.png' file.
plt.show()

# STEP 10: Print measurement counts.
print("Counts:", counts)

```

### Result 
This proves that quantum states can be transferred using entanglement and classical communication, even if the qubit itself is not transmitted.

In the context of photonic qubits, this protocol could be implemented using polarized photons and optical components like beam splitters and wave plates to achieve the same functionality over fiber-optic channels.

 ![image](https://github.com/user-attachments/assets/2feeb67f-8dc0-4733-b5f2-1ae6d6203cac)

### Verification Code: Comparing Initial vs. Teleported State

 Code:
   ```python
# This script verifies Quantum Teleportation by comparing the initial state
# of the sender's qubit (qubit 0) with the final state of the receiver's
# qubit (qubit 2) after the teleportation protocol.

# STEP 1: Import necessary libraries
from qiskit import QuantumCircuit, transpile
from qiskit_aer import Aer
from qiskit.visualization import plot_histogram
from matplotlib import pyplot as plt

# --- Part 1: Simulate the initial state of Qubit 0 directly for comparison ---

# Create a simple circuit with 1 qubit and 1 classical bit
qc_initial = QuantumCircuit(1, 1)
# Prepare qubit 0 in the same arbitrary state as in the teleportation protocol
# For this example, we use Hadamard to put it in superposition: (|0> + |1>) / sqrt(2)
qc_initial.h(0)
# Measure qubit 0
qc_initial.measure(0, 0)

# Simulate the initial qubit measurement
simulator = Aer.get_backend('qasm_simulator')
compiled_initial = transpile(qc_initial, simulator)
result_initial = simulator.run(compiled_initial, shots=1024).result()
counts_initial = result_initial.get_counts()

print("Initial Qubit 0 Measurement Counts (for comparison):", counts_initial)

# --- Part 2: Quantum Teleportation Protocol ---

# Create a 3-qubit circuit with 3 classical bits for measurement
# Qubit 0: Sender's qubit (state to be teleported)
# Qubit 1: Sender's part of the Bell pair
# Qubit 2: Receiver's part of the Bell pair
qc_teleport = QuantumCircuit(3, 3) # We still need 3 classical bits for intermediate measurements,
                                   # but we'll only plot the final qubit 2's result.

# Step 2.1: Prepare sender's qubit (qubit 0) in an arbitrary state.
# This must be the SAME state as qc_initial for a valid comparison.
qc_teleport.h(0)

# Step 2.2: Create Bell pair between qubit 1 and 2.
qc_teleport.h(1)  # Put qubit 1 in superposition
qc_teleport.cx(1, 2) # Entangle qubit 1 with qubit 2

qc_teleport.barrier() # Optional: Separator for visual clarity in circuit diagram

# Step 2.3: Entangle sender's qubit (0) with their part of the Bell pair (1).
qc_teleport.cx(0, 1) # CNOT gate with qubit 0 as control, qubit 1 as target
qc_teleport.h(0)   # Hadamard gate on qubit 0

qc_teleport.barrier() # Optional: Separator for visual clarity

# Step 2.4: Measure qubit 0 and 1 (sender's qubits).
# The results of these measurements (classical bits 0 and 1) are used
# to conditionally apply gates at the receiver's end.
qc_teleport.measure([0, 1], [0, 1])

qc_teleport.barrier() # Optional: Separator for visual clarity

# Step 2.5: Apply conditional gates to qubit 2 (receiver).
# The receiver applies gates to their qubit (qubit 2) based on the classical
# measurement results received from the sender.
# If classical bit 1 is 1, apply X gate to qubit 2.
qc_teleport.cx(1, 2) # CNOT with classical bit 1 as control, qubit 2 as target
# If classical bit 0 is 1, apply Z gate to qubit 2.
qc_teleport.cz(0, 2) # Controlled-Z with classical bit 0 as control, qubit 2 as target

qc_teleport.barrier() # Optional: Separator for visual clarity

# Step 2.6: Measure the final qubit (qubit 2) at the receiver's end.
# This is the crucial measurement to verify if the state was successfully teleported.
qc_teleport.measure(2, 2) # ONLY measure qubit 2 and store in classical bit 2

# STEP 3: Simulate the teleportation circuit.
compiled_teleport = transpile(qc_teleport, simulator)
result_teleport = simulator.run(compiled_teleport, shots=1024).result()

# Get the measurement counts for the teleported qubit (qubit 2).
# We need to process the counts to only show the result of classical bit 2.
# The counts will be like {'000', '001', ..., '111'}
# We are interested in the last bit, which corresponds to qubit 2.
teleported_counts = {}
raw_counts = result_teleport.get_counts()

for outcome, count in raw_counts.items():
    # The outcome string is like 'c2c1c0' (classical bit 2, classical bit 1, classical bit 0)
    # We want the result of classical bit 2, which is the first character.
    teleported_bit = outcome[0]
    teleported_counts[teleported_bit] = teleported_counts.get(teleported_bit, 0) + count

print("Teleported Qubit 2 Measurement Counts:", teleported_counts)

# STEP 4: Plot histograms for comparison.

# Create a figure with two subplots side-by-side
fig, (ax1, ax2) = plt.subplots(1, 2, figsize=(14, 6)) # Increased figure size

# Plot histogram for the initial qubit 0 measurement
plot_histogram(counts_initial, ax=ax1, color='green', bar_labels=True)
ax1.set_title("Initial Qubit 0 State (Direct Measurement)")
ax1.grid(True)
ax1.set_xlabel("Measurement Outcome")
ax1.set_ylabel("Count")

# Plot histogram for the teleported qubit 2 measurement
plot_histogram(teleported_counts, ax=ax2, color='purple', bar_labels=True)
ax2.set_title("Teleported Qubit 2 State (Final Measurement)")
ax2.grid(True)
ax2.set_xlabel("Measurement Outcome")
ax2.set_ylabel("Count")

plt.tight_layout() # Adjust layout to prevent overlapping titles/labels

# Save the combined plot to a file
plt.savefig('quantum_teleportation_verification.png')

# Display the plot
plt.show()

# Final conclusion based on counts
print("\n--- Verification Summary ---")
print(f"Expected counts for initial Qubit 0: {counts_initial}")
print(f"Observed counts for teleported Qubit 2: {teleported_counts}")

# Check if the distributions are similar
if abs(counts_initial.get('0', 0) - teleported_counts.get('0', 0)) < 50 and \
   abs(counts_initial.get('1', 0) - teleported_counts.get('1', 0)) < 50:
    print("\nConclusion: The measurement distributions are very similar, indicating successful quantum teleportation!")
else:
    print("\nConclusion: The measurement distributions show some differences. Teleportation may not be ideal.")

```
Diagram:
 ![image](https://github.com/user-attachments/assets/e322627f-20a6-40ce-9b5e-527fdcdcc048)


 # Simulating Decoherence (Noise in Photonic Qubits)

In real-world quantum systems, qubits are never perfect — they interact with their environment and **lose coherence** over time. This is called **decoherence** and it's one of the main challenges in building large-scale quantum computers.

Photonic qubits (like those based on polarization or phase of light) are less susceptible to certain types of noise, but **still face decoherence due to**:

- Photon scattering
- Phase noise in optical fibers
- Beam misalignment or absorption

###  What is Decoherence?

In quantum computing, decoherence causes a **loss of quantum information**, often degrading superposition and entanglement.

For example:
- A perfect GHZ state gives only `000` or `111`
- But with decoherence, you start seeing `001`, `010`, `101` due to error

---

### Simulating Noise with Qiskit

We can simulate noise by using Qiskit's **noise model API** to mimic:

- **Depolarizing error**: Photon scattering or polarization drift
- **Gate errors**: Imperfect wave plates or misaligned lenses
- **Measurement errors**: Detector inefficiency or misread signals

---

### Expected Output

You will notice:
- **More noisy measurement outcomes** in the histogram
- Less probability for pure `000` or `111` (GHZ state degrades)
- Insight into why real-world implementation needs **error correction or stable optics**

---

### 💻 Code Block (Qiskit GHZ with Noise Model)

```python
# This script simulates a 3-qubit GHZ (Greenberger–Horne–Zeilinger) state with a noise model.
# It creates a GHZ state, applies a basic noise model (depolarizing error),
# measures all three qubits, and then plots the measurement results.

# STEP 1: Import necessary libraries
from qiskit import QuantumCircuit, transpile
from qiskit_aer import AerSimulator
from qiskit.visualization import plot_histogram
from matplotlib import pyplot as plt

# Import noise model components
from qiskit_aer.noise import NoiseModel, depolarizing_error, thermal_relaxation_error

# STEP 2: Create the noise model
noise_model = NoiseModel()

# Add depolarizing error (2% chance) to all H, X, and CNOT gates
depol1_error = depolarizing_error(0.02, 1)  # 1-qubit gate
depol2_error = depolarizing_error(0.02, 2)  # 2-qubit gate

noise_model.add_all_qubit_quantum_error(depol1_error, ['h', 'x'])
noise_model.add_all_qubit_quantum_error(depol2_error, ['cx'])

# STEP 3: Create the GHZ state circuit (3 qubits)
qc = QuantumCircuit(3, 3)
qc.h(0)
qc.cx(0, 1)
qc.cx(0, 2)
qc.measure([0, 1, 2], [0, 1, 2])

# STEP 4: Simulate the circuit with noise
simulator = AerSimulator(noise_model=noise_model)
compiled = transpile(qc, simulator)
result = simulator.run(compiled, shots=1024).result()
counts = result.get_counts()

# STEP 5: Plot histogram
fig, ax = plt.subplots(figsize=(8, 6))
plot_histogram(counts, ax=ax, color='blue', bar_labels=True)
ax.set_title("GHZ State with Decoherence Noise")
ax.grid(True)
plt.savefig("ghz_noise_histogram.png")
plt.show()

# STEP 6: Show results
print("Measurement Counts:", counts)

```

## Result

![image](https://github.com/user-attachments/assets/be055fe0-3c11-4422-a114-034144665afe)


 





