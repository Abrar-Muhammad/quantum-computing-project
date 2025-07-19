# BB84 Quantum Key Distribution (QKD) Simulation

This project simulates the **BB84 Protocol**, a foundational quantum cryptography technique that enables two parties — traditionally **Alice** and **Bob** — to generate a shared, secret key securely over a quantum channel. The protocol is resistant to eavesdropping due to the laws of quantum mechanics.

This simulation is built using **Qiskit** and represents qubits using **photon polarization** (horizontal = |0⟩, vertical = |1⟩, diagonal = |+⟩, anti-diagonal = |−⟩).

---

## 🔍 What Is BB84?

BB84 is the **first quantum cryptography protocol**, developed in 1984 by Bennett and Brassard. It allows:

- Secure key exchange over an insecure quantum channel.
- Detection of **eavesdropping (Eve)** by comparing a subset of measurement results.
- Quantum bits (qubits) are encoded in **random bases** (Z or X), and the receiver randomly chooses bases to measure.

Only when both Alice and Bob choose the **same basis** is the bit kept as part of the **sifted key**.

---

## Features Simulated

 Alice randomly generates bits and encodes them in Z or X basis  
 Bob randomly chooses measurement bases  
 Eve (optional) attempts to intercept and resend qubits  
 Basis sifting to build the shared key  
 Calculation of QBER (Quantum Bit Error Rate)  
 Histograms of Bob's measurement outcomes with and without Eve  

---

## Photon-Based Encoding

This simulation aligns with my broader research on using **photons as qubits**. The qubit states are encoded via photon **polarization**:

| Classical Bit | Basis | Qubit State (Photon Polarization) |
|---------------|-------|------------------------------------|
| 0             | Z     | |0⟩ (Horizontal)                   |
| 1             | Z     | |1⟩ (Vertical)                     |
| 0             | X     | |+⟩ = (|0⟩ + |1⟩)/√2 (Diagonal)     |
| 1             | X     | |−⟩ = (|0⟩ − |1⟩)/√2 (Anti-diagonal)|

This shows how **quantum optics** can encode and measure information securely.

---

# Results

 **Without Eve:**  
  - Low or zero QBER  
  - Alice and Bob's sifted keys closely match  
  - Secure key generation

<img width="796" height="712" alt="image" src="https://github.com/user-attachments/assets/e795be7e-91e9-4a03-a4aa-7780ea97b950" />



   **With Eve:**  
  - Increased QBER (Eve's incorrect basis choices introduce errors)  
  - Mismatches between Alice and Bob's sifted keys  
  - Eavesdropping detected



<img width="796" height="768" alt="image" src="https://github.com/user-attachments/assets/1c5dcf6e-ca3b-4dbb-96d7-fd5576f4c591" />


---

## Why This Matters

This experiment supports my **central hypothesis**:

> “It is feasible to construct quantum cryptographic protocols using photon polarization as a qubit encoding method, enabling secure communication and detection of eavesdropping without requiring cryogenic setups or complex quantum hardware.”

---

##  How to Run

Make sure you have `qiskit` installed:

```python
# This script simulates the BB84 Quantum Key Distribution (QKD) protocol
# using Qiskit in Python. It demonstrates how a shared secret key can be
# established between Alice and Bob, and how an eavesdropper (Eve)
# introduces detectable errors.

# Required imports for quantum circuit creation, simulation, and visualization
from qiskit import QuantumCircuit, transpile
from qiskit_aer import AerSimulator # For simulating quantum circuits
from qiskit.visualization import plot_histogram
import matplotlib.pyplot as plt
import random
import numpy as np # For numerical operations, especially for isclose

# --- Configuration ---
NUM_QUBITS = 100 # Number of qubits Alice sends to Bob
EAVESDROPPER_PRESENT = False # Set to True to simulate Eve's presence

# --- Helper Functions ---

def generate_random_bit():
    """Generates a random bit (0 or 1)."""
    return random.randint(0, 1)

def generate_random_basis():
    """Generates a random basis (0 for Z/Rectilinear, 1 for X/Diagonal)."""
    return random.randint(0, 1)

def encode_qubit(bit, basis):
    """
    Encodes a qubit in Qiskit based on the given bit and basis.
    Basis 0 (Z/Rectilinear): |0> or |1>
    Basis 1 (X/Diagonal): |+> or |->
    """
    qc = QuantumCircuit(1, 1) # 1 qubit, 1 classical bit
    if bit == 1:
        qc.x(0) # Apply X gate if bit is 1 (|0> -> |1>, |+> -> |->)
    if basis == 1:
        qc.h(0) # Apply H gate if basis is X (transforms Z to X basis)
    return qc

def measure_qubit(qc, basis):
    """
    Measures a qubit in Qiskit in the specified basis.
    Applies H gate before measurement if basis is X.
    """
    if basis == 1:
        qc.h(0) # Transform to Z basis for measurement if current basis is X
    qc.measure(0, 0) # Measure the qubit
    return qc

# --- BB84 Simulation Protocol ---

def simulate_bb84(num_qubits, eavesdropper_present):
    """
    Simulates the BB84 QKD protocol.
    Args:
        num_qubits (int): The total number of qubits exchanged.
        eavesdropper_present (bool): True if Eve is eavesdropping, False otherwise.
    Returns:
        dict: A dictionary containing simulation results.
    """
    print(f"--- BB84 Simulation Started (Qubits: {num_qubits}, Eve: {eavesdropper_present}) ---")

    alice_bits = []      # Alice's secret bits
    alice_bases = []     # Alice's chosen encoding bases
    bob_bases = []       # Bob's chosen measurement bases
    bob_measurements = []# Bob's measurement results

    # Initialize the AerSimulator for running quantum circuits
    simulator = AerSimulator()

    for i in range(num_qubits):
        # 1. Alice's Preparation
        bit = generate_random_bit()
        basis = generate_random_basis() # 0 for Z, 1 for X

        alice_bits.append(bit)
        alice_bases.append(basis)

        # Encode the qubit
        qc_alice = encode_qubit(bit, basis)

        # 2. Eve's Eavesdropping (if enabled)
        # Eve intercepts the qubit, measures it, and re-sends it.
        if eavesdropper_present:
            eve_basis = generate_random_basis() # Eve randomly chooses a basis
            qc_eve = measure_qubit(qc_alice.copy(), eve_basis) # Eve measures
            
            # Run Eve's measurement circuit
            compiled_eve = transpile(qc_eve, simulator)
            result_eve = simulator.run(compiled_eve, shots=1).result()
            counts_eve = result_eve.get_counts(qc_eve)
            eve_measurement = int(list(counts_eve.keys())[0], 2) # Eve's measured bit

            # Eve re-encodes the qubit based on her measurement for Bob
            # This is where the disturbance is introduced if eve_basis != alice_basis
            qc_for_bob = encode_qubit(eve_measurement, eve_basis)
        else:
            qc_for_bob = qc_alice # If no Eve, Bob receives Alice's original qubit

        # 3. Bob's Measurement
        bob_basis = generate_random_basis() # Bob randomly chooses a basis
        bob_bases.append(bob_basis)

        qc_bob = measure_qubit(qc_for_bob.copy(), bob_basis) # Bob measures

        # Run Bob's measurement circuit
        compiled_bob = transpile(qc_bob, simulator)
        result_bob = simulator.run(compiled_bob, shots=1).result()
        counts_bob = result_bob.get_counts(qc_bob)
        bob_measurement = int(list(counts_bob.keys())[0], 2) # Bob's measured bit
        bob_measurements.append(bob_measurement)

    # 4. Basis Sifting (Classical Communication)
    # Alice and Bob publicly compare their bases (but not their bits).
    # They keep only the bits where their bases matched.
    alice_sifted_key = []
    bob_sifted_key = []
    
    print("\n--- Basis Sifting ---")
    print(f"{'Qubit #':<9} {'Alice Bit':<10} {'Alice Basis':<13} {'Bob Basis':<10} {'Bob Meas.':<12} {'Basis Match':<12}")
    print("-" * 75)
    for i in range(num_qubits):
        alice_basis_str = 'Z' if alice_bases[i] == 0 else 'X'
        bob_basis_str = 'Z' if bob_bases[i] == 0 else 'X'
        basis_match_str = "Yes" if alice_bases[i] == bob_bases[i] else "No"
        
        print(f"{i:<9} {alice_bits[i]:<10} {alice_basis_str:<13} {bob_basis_str:<10} {bob_measurements[i]:<12} {basis_match_str:<12}")

        if alice_bases[i] == bob_bases[i]:
            alice_sifted_key.append(alice_bits[i])
            bob_sifted_key.append(bob_measurements[i])
    
    print("\nAlice's Sifted Key:", alice_sifted_key)
    print("Bob's Sifted Key:  ", bob_sifted_key)

    # 5. Key Agreement and Error Check (QBER)
    # Alice and Bob compare a small subset of their sifted keys to check for errors.
    errors = 0
    for i in range(len(alice_sifted_key)):
        if alice_sifted_key[i] != bob_sifted_key[i]:
            errors += 1

    key_agreement_rate = len(alice_sifted_key) / num_qubits if num_qubits > 0 else 0
    qber = errors / len(alice_sifted_key) if len(alice_sifted_key) > 0 else 0

    print(f"\n--- Key Agreement & Error Check ---")
    print(f"Total Qubits Sent: {num_qubits}")
    print(f"Sifted Key Length: {len(alice_sifted_key)}")
    print(f"Key Agreement Rate (Sifted Key Length / Total Qubits): {key_agreement_rate:.2f}")
    print(f"Errors in Sifted Key: {errors}")
    print(f"Quantum Bit Error Rate (QBER): {qber:.4f}")

    # Prepare data for histogram (overall Bob's measurements)
    bob_measurement_counts = {str(k): 0 for k in range(2)} # Initialize '0' and '1' counts
    for measurement in bob_measurements:
        bob_measurement_counts[str(measurement)] += 1

    return {
        "num_qubits": num_qubits,
        "eavesdropper_present": eavesdropper_present,
        "alice_bits": alice_bits,
        "alice_bases": alice_bases,
        "bob_bases": bob_bases,
        "bob_measurements": bob_measurements,
        "alice_sifted_key": alice_sifted_key,
        "bob_sifted_key": bob_sifted_key,
        "key_agreement_rate": key_agreement_rate,
        "qber": qber,
        "errors": errors,
        "sifted_key_length": len(alice_sifted_key),
        "bob_measurement_counts": bob_measurement_counts
    }

# --- Main Execution ---
if __name__ == "__main__":
    # --- Run Simulation without Eve ---
    print("--- SIMULATION WITHOUT EAVESDROPPER ---")
    results_no_eve = simulate_bb84(NUM_QUBITS, False)

    # Plot Bob's measurement outcomes without Eve
    fig1, ax1 = plt.subplots(figsize=(8, 6)) # Create figure and axes explicitly
    plot_histogram(results_no_eve["bob_measurement_counts"],
                   ax=ax1, # Pass the axes to plot_histogram
                   title=f"Bob's Measurements (No Eve, {NUM_QUBITS} Qubits)",
                   color=['#4CAF50', '#2196F3'], bar_labels=True)
    plt.tight_layout()
    plt.savefig("bob_measurements_no_eve.png") # Removed fig=fig1
    plt.show()
    plt.close(fig1)

    # --- Run Simulation with Eve ---
    print("\n--- SIMULATION WITH EAVESDROPPER ---")
    results_with_eve = simulate_bb84(NUM_QUBITS, True)

    # Plot Bob's measurement outcomes with Eve
    fig2, ax2 = plt.subplots(figsize=(8, 6)) # Create figure and axes explicitly
    plot_histogram(results_with_eve["bob_measurement_counts"],
                   ax=ax2, # Pass the axes to plot_histogram
                   title=f"Bob's Measurements (With Eve, {NUM_QUBITS} Qubits)",
                   color=['#FF5722', '#9C27B0'], bar_labels=True) # Different colors for Eve's presence
    plt.tight_layout()
    plt.savefig("bob_measurements_with_eve.png") # Removed fig=fig2
    plt.show()
    plt.close(fig2)

    print("\n--- Simulation Summary ---")
    print(f"No Eve: QBER = {results_no_eve['qber']:.4f}, Sifted Key Length = {results_no_eve['sifted_key_length']}")
    print(f"With Eve: QBER = {results_with_eve['qber']:.4f}, Sifted Key Length = {results_with_eve['sifted_key_length']}")
    print("\nCheck the generated 'bob_measurements_no_eve.png' and 'bob_measurements_with_eve.png' files for histograms.")
```


