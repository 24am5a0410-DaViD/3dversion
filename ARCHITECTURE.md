# 🏗️ Architecture Design & Specification

## 1. Architectural Philosophy: Strict Separation of Concerns

The application adheres to a strict 5-layer decoupled design:

```
[Layer 4: UI & Learning Interface] (React, KaTeX, Tailwind)
         │
[Layer 3: Orchestration & State] (Zustand, Camera Director)
    ┌────┴──────────────────────────┐
    ▼                               ▼
[Layer 2: 3D WebGL2 Engine]   [Layer 1: Physics & Protocol Core]
(Three.js, GLSL, Bloom)       (Pure TS, 0 DOM/GL, Vitest)
```

### Layer 1: Physics & Protocol Core (`src/core/`)
* **Strict Constraints:** Zero DOM, WebGL, or Three.js imports. Fully deterministic with unit-tested identities.
* **Algebraic Foundation:**
  * `Complex`: Complex arithmetic primitives.
  * `Matrix2x2`: 2×2 complex operators, Pauli matrices, commutator bracket $[A, B] = AB - BA$, trace, dagger (Hermitian adjoint).
  * `Vector2`: Jones vectors and Bloch sphere coordinates.
* **Optics Calculus:**
  * Linear Polarizers $J_{\text{pol}}(\theta)$
  * Wave Plates (HWP, QWP) $J_{\text{HWP}}(\theta) = \begin{pmatrix} \cos 2\theta & \sin 2\theta \\ \sin 2\theta & -\cos 2\theta \end{pmatrix}$
  * Phase Modulators $J_{\text{PM}}(\phi)$
  * Attenuators $J_{\text{AM}}(T)$ down to mean photon numbers $\mu \approx 0.5$.
  * Polarizing Beam Splitters ($PBS$) and SPAD detectors with Poisson photon statistics and Geiger-mode avalanche probabilities.
* **BB84 Protocol Engine:**
  * Encoding, quantum channel, Bob's projective measurement.
  * Classical sifting over basis comparison.
  * Quantum Bit Error Rate ($\text{QBER}$) calculation and abort threshold detection ($\text{QBER} > 11\%$).
  * Error correction syndrome leakage and privacy amplification universal hashing.

### Layer 2: 3D Scene Layer (`src/scenes/` & `src/render/`)
* **Scene A (`BB84BenchScene.ts`):** Exact reproduction of Reference Image 2:
  * Alice: 4 gold source blocks ($H, A, D, V$), beam splitters, filters, $AM \rightarrow PM \rightarrow AM$ chain.
  * Bob: HWP basis rotator, PBS prism, SPAD detectors.
  * Traveling photon pulse shader following the beam path.
* **Scene B (`SatelliteScene.ts`):** Nature-style Jinan-1 architecture from Reference Image 1:
  * Panels a–d with hierarchical camera zooming: Earth Orbit $\leftrightarrow$ Payload $\leftrightarrow$ Fiber Module $\leftrightarrow$ Ground Station.
  * Multi-wavelength laser beam rendering ($850\text{ nm}$ Quantum, $812\text{ nm}$ Downlink, $1538\text{ nm}$ Uplink, $532/785\text{ nm}$ Beacons).
* **Scene C (`BlochSphereScene.ts`):** Unit sphere with wireframe meridians and glowing state vector.

### Layer 3: Orchestration & State (`src/state/`)
* Single source of truth managed with Zustand.
* Synchronizes simulation ticks, telemetry metrics, and user interactions to 3D scenes.

### Layer 4: UI & Dual-Depth Learning Interface (`src/ui/`)
* **Dual Depth:** Every lesson offers "Explain Like I'm 12" (accessible analogies) and "Show Me The Math" (rigorous derivations).
* **Live KaTeX Math Rendering:** Non-commuting commutator proof $[M_+, M_0] \neq 0$ from Reference Image 2.
* **HUD Telemetry:** Real-time QBER meters, sifted bit counts, key rate, and distilled key hex string.
