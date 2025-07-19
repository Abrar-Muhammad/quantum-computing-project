# Quantum Cryptography (BB84)

## What Is BB84?

**BB84** is the first and most famous **quantum key distribution (QKD)** protocol, introduced by **Charles Bennett** and **Gilles Brassard** in 1984.

It uses **quantum properties of photons** to securely exchange a secret cryptographic key between two parties (**Alice and Bob**) — such that any **eavesdropper (Eve)** will be detected due to quantum measurement disturbance.

---

## My Approach: Light as Qubits

In this research, I simulate BB84 using **photon-based qubits**, where:

- `|0⟩` → Horizontally polarized photon (→)
- `|1⟩` → Vertically polarized photon (↑)
- `|+⟩` → Diagonally polarized photon (/)
- `|−⟩` → Anti-diagonally polarized photon (\)

These four states correspond to two **polarization bases**:
- **Rectilinear (Z-basis)**: `|0⟩`, `|1⟩`
- **Diagonal (X-basis)**: `|+⟩`, `|−⟩`

---

## What I’m Simulating

I will implement the following BB84 protocol steps using **Qiskit** to simulate **polarization-based qubits**:

1. **Alice** randomly chooses bits and bases, then encodes each bit in a corresponding polarization.
2. **Alice sends** the photons (qubits) to **Bob**.
3. **Bob** randomly chooses a basis for each photon to measure.
4. **They compare** the basis choices publicly (not the bit values).
5. **Matching basis measurements** are kept to form a shared **secret key**.
6. **Check for eavesdropping** by comparing a subset of the key.
   - If no eavesdropper: secure key is used.
   - If an eavesdropper is detected: discard the key.

---

## Why This Matters

- **Eavesdropping is detectable** due to quantum no-cloning and collapse of wavefunction.
- Simulating BB84 with **photons as qubits** supports the vision that **quantum light** is not just a medium for data, but for **security infrastructure**.
- This experiment connects **quantum optics and cryptography** — proving the **real-world relevance of photonic quantum computing**.



