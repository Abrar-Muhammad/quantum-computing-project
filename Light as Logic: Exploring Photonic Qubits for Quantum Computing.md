# 🌟 Light as Logic: Exploring Photonic Qubits for Quantum Computing

## 📄 Abstract
Quantum computing relies on qubits, which unlike classical bits, can exist in superposition and have measurable phase relationships. While various physical systems have been proposed and implemented for qubit realization, this paper explores the potential of electromagnetic (EM) wave-based qubits, specifically in photonic quantum computing. Photons, with their controllable amplitude, phase, and polarization, provide a promising medium for qubit encoding. This research investigates how EM wave properties can represent qubit states, simulate quantum gates using optics, and compares photonic qubits with other leading qubit technologies.

---

## 1. Introduction
Quantum computing is fundamentally changing the landscape of computation, enabling solutions to problems that are infeasible for classical computers. At its core lies the qubit, a quantum unit of information. While superconducting circuits and trapped ions are popular implementations, photons offer unique advantages such as low decoherence and natural mobility. This paper investigates the feasibility and design of photonic qubits based on electromagnetic wave properties and explores how they may contribute to scalable, high-speed quantum systems.

---

## 2. Qubits and EM Waves: Theoretical Overlap

A classical bit is binary — either 0 or 1. A quantum bit (qubit), however, is described as a linear combination:

## |ψ⟩ = α|0⟩ + β|1⟩

Where `|α|² + |β|² = 1`, and α, β are complex numbers encoding amplitude and phase.

### 📡 Electromagnetic Waves

EM waves have similar descriptors:
- **Amplitude** → corresponds to the magnitude of probability.
- **Phase** → analogous to quantum phase.
- **Polarization** → maps naturally to qubit basis states (e.g., horizontal = `|0⟩`, vertical = `|1⟩`).

This overlap motivates the use of light (photons) to implement quantum logic.

---

## 3. Encoding Qubits with Light

Photonic quantum computing uses photons to encode and process quantum information. The two primary methods of encoding are:

### 3.1 Polarization Encoding
- `|0⟩` = Horizontally polarized photon  
- `|1⟩` = Vertically polarized photon  
- Superpositions: Diagonal, circular, and elliptical polarizations

### 3.2 Path Encoding
- A single photon travels along two paths simultaneously, representing `|0⟩` and `|1⟩`.

### 🔧 Tools
- **Wave plates** → act as qubit gates  
- **Beam splitters** → act like Hadamard gates  
- **Phase shifters** → modify the qubit’s phase  
- **Interferometers** → enable measurement and interference logic

---

## 4. Simulating Photonic Quantum Gates

Using platforms like [Quirk](https://algassert.com/quirk) and [Strawberry Fields](https://strawberryfields.ai), we simulated basic quantum operations using optical analogs.

### 4.1 Beam Splitter as Hadamard Gate

A 50/50 beam splitter can create a superposition of path states:

## |0⟩ → (1/√2)(|0⟩ + |1⟩)

### 4.2 Mach-Zehnder Interferometer

By adjusting the phase in one arm, we demonstrate constructive or destructive interference, mimicking logic operations like CNOT and phase gates.

---

## 5. Comparison with Other Qubit Technologies

| Feature        | Photonic Qubits                  | Superconducting Qubits     | Trapped Ions          |
|----------------|----------------------------------|-----------------------------|------------------------|
| **Decoherence** | Low (photons don’t interact easily) | Medium                      | Low                    |
| **Scalability** | Challenging (hard to entangle)  | Improving                   | Complex                |
| **Interaction** | Weak (needs nonlinear optics)   | Strong                      | Strong                 |
| **Temperature** | Room temp possible              | Needs cryogenics            | Room temp              |
| **Speed**       | Extremely fast (speed of light) | Fast                        | Slow-medium            |

Photonic qubits are excellent for communication and linear operations but currently face difficulty with multi-qubit interaction and scaling logic gates.

---

## 6. Future Directions

To overcome current limitations in photonic quantum computing:
- Use **nonlinear crystals** or **quantum dots** to mediate photon interactions  
- Develop **hybrid systems** combining photons for transmission and other qubits (e.g., superconducting) for logic  
- Improve **photon source stability** and **detector sensitivity**

---

## 7. Conclusion

This paper demonstrates that the properties of electromagnetic waves closely mirror those of qubit systems, especially in terms of superposition and phase. By simulating photonic gates and studying polarization-based encoding, we confirm that EM waves can be a powerful medium for quantum information. While not yet superior for general-purpose quantum computing, photonic qubits offer immense promise, particularly in secure communication and quantum networking.

---

## 🔗 References

1. Nielsen & Chuang, *Quantum Computation and Quantum Information*  
2. Xanadu AI - [https://www.xanadu.ai](https://www.xanadu.ai)  
3. IBM Quantum Lab - [https://quantum-computing.ibm.com](https://quantum-computing.ibm.com)  
4. Quirk Quantum Simulator - [https://algassert.com/quirk](https://algassert.com/quirk)  
5. Strawberry Fields - [https://strawberryfields.ai](https://strawberryfields.ai)

---

*Written by: Muhammad Abrar*  



