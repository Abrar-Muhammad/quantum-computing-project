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

## Entangling Photons Using Polarization

In photonic quantum computing, entanglement is achieved by manipulating the polarization of photons using beam splitters and nonlinear crystals.

### 1. Photon Pair Generation – SPDC

A high-energy laser beam (like UV light) is passed through a **nonlinear crystal** (e.g., BBO – beta barium borate).  
This initiates a quantum optical process called **Spontaneous Parametric Down-Conversion (SPDC)**, producing two entangled photons:

- One laser photon ➡️ Two lower-energy photons
- These two photons are created in an **entangled polarization state**

### 2. Entanglement via Beam Splitters

The entangled photons are directed into a **beam splitter**, which allows their paths to overlap and interfere.  
Due to quantum interference, the final state becomes a **Bell state** — a maximally entangled quantum state.

### 3. Resulting Bell State:

####|ψ⟩ = 1/√2 (|H⟩|V⟩ + |V⟩|H⟩)

- If one photon is measured as **horizontal** (`|H⟩`), the other must be **vertical** (`|V⟩`), and vice versa.
- The two photons are now **inseparable** — their polarizations are **entangled** even across large distances.

### 4. Applications of Entangled Photons

| Area                    | Use Case                                      |
|-------------------------|-----------------------------------------------|
| Quantum Teleportation   | Transferring quantum states across distances  |
| Quantum Cryptography    | Secure key exchange (e.g., BB84 protocol)     |
| Quantum Communication   | Entanglement-based quantum networking         |

Entangling photon polarization is a core component in building scalable and secure quantum systems.

## 5. Polarization as an Alternative to Phase in Qubits

While phase is a fundamental aspect of quantum state manipulation, **photon polarization** offers a practical and often simpler alternative for encoding qubit states. In photonic quantum computing, qubit states can be defined by the orientation of the electric field vector of a photon.

### 5.1 Mapping Qubit States to Polarization

| Qubit State         | Photon Polarization                      |
|---------------------|-------------------------------------------|
| \|0⟩                | Horizontal (H)                            |
| \|1⟩                | Vertical (V)                              |
| α\|0⟩ + β\|1⟩       | Diagonal, Circular, or Elliptical (superposition) |

This means that instead of encoding quantum state information using complex phase amplitudes, we can **use the angle and type of polarization** to represent qubits.

For example:
- A **45° linear polarization** represents a diagonal superposition state.
- A **right or left circular polarization** corresponds to specific complex superpositions.

### 5.2 Benefits of Polarization-Based Encoding

- ✅ **Easier physical implementation:** Polarization is easier to control and measure using wave plates, polarizing beam splitters (PBS), and polarizers.
- ✅ **Natural superposition:** Light inherently supports combinations of polarization states.
- ✅ **Less decoherence:** Photons do not interact easily with their environment, keeping their polarization stable over long distances.
- ✅ **No cryogenics:** Unlike superconducting qubits, polarization qubits work at room temperature.

### 8.3 Research Extension Idea

This leads to a novel direction:  
**“Can we build all fundamental quantum logic gates using polarization-only transformations, minimizing or eliminating the need for phase manipulation?”**

Such a model would use:
- Wave plates to implement X, Y, and Z gates via rotation
- Polarizers and beam splitters for measurements
- Interferometers for gate chaining and entanglement

This could simplify future **quantum optical processors** for scalable and room-temperature quantum computing.

