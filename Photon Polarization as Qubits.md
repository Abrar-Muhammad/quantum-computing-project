## Photon Polarization as Qubits

In photonic quantum computing:

- `|0⟩` = Horizontal polarization  
- `|1⟩` = Vertical polarization  
- `|ψ⟩ = α|0⟩ + β|1⟩` = Superposition (e.g., diagonal or circular)


These states are manipulated using optical components:

- **Wave Plates**: Rotate polarization (simulate gates like X, Z, H)
- **Beam Splitters**: Create superpositions or entanglements
- **Phase Shifters**: Introduce quantum phase (φ)
- **Polarizers**: Measure and collapse quantum states

### Example Gate Simulation:
A half-wave plate at 45° acts as an X gate:

- Input: `|H⟩` → Output: `|V⟩`
- Input: `|V⟩` → Output: `|H⟩`

A quarter-wave plate introduces a phase shift:

- Input: `|H⟩` → Output: Circular polarization
- This corresponds to adding a phase `φ = π/2`

### Entanglement:
Two photons can be entangled using beam splitters and non-linear crystals, creating states like:

## 🔗 Entangling Photons Using Polarization

In photonic quantum computing, entanglement is achieved by manipulating the polarization of photons using beam splitters and nonlinear crystals.

### 🧪 1. Photon Pair Generation – SPDC

A high-energy laser beam (like UV light) is passed through a **nonlinear crystal** (e.g., BBO – beta barium borate).  
This initiates a quantum optical process called **Spontaneous Parametric Down-Conversion (SPDC)**, producing two entangled photons:

- One laser photon ➡️ Two lower-energy photons
- These two photons are created in an **entangled polarization state**

### 🔄 2. Entanglement via Beam Splitters

The entangled photons are directed into a **beam splitter**, which allows their paths to overlap and interfere.  
Due to quantum interference, the final state becomes a **Bell state** — a maximally entangled quantum state.

### 📐 3. Resulting Bell State:

####|ψ⟩ = 1/√2 (|H⟩|V⟩ + |V⟩|H⟩)

- If one photon is measured as **horizontal** (`|H⟩`), the other must be **vertical** (`|V⟩`), and vice versa.
- The two photons are now **inseparable** — their polarizations are **entangled** even across large distances.

### 🔐 4. Applications of Entangled Photons

| Area                    | Use Case                                      |
|-------------------------|-----------------------------------------------|
| Quantum Teleportation   | Transferring quantum states across distances  |
| Quantum Cryptography    | Secure key exchange (e.g., BB84 protocol)     |
| Quantum Communication   | Entanglement-based quantum networking         |

Entangling photon polarization is a core component in building scalable and secure quantum systems.
