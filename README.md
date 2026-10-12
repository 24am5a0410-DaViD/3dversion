# ⚛️ Quantum Key Distribution (QKD) | 3D Interactive Explorable

A production-quality, WebGL2/Three.js interactive 3D learning platform that teaches Quantum Key Distribution (QKD) from tabletop BB84 optics to satellite-to-ground quantum communications.

![QKD Explorable](https://img.shields.io/badge/WebGL2-Three.js-blue)
![TypeScript](https://img.shields.io/badge/TypeScript-Strict-green)
![Tests](https://img.shields.io/badge/Vitest-Passing-brightgreen)
![License](https://img.shields.io/badge/License-MIT-purple)

---

## 🌟 Interactive 3D Scenes Rebuilt from Reference Imagery

### Scene A: Tabletop BB84 Bench (Reference Image 2)
* **Alice's Transmitter:** 4 laser/polarizer sources ($H$, $A$, $D$, $V$), beam splitters, spatial filters, and the $AM \rightarrow PM \rightarrow AM$ electro-optic modulation chain attenuating pulses down to mean photon number $\mu \approx 0.5$.
* **Bob's Receiver:** Half-Wave Plate ($HWP$) for basis selection ($Z$ rectilinear vs $X$ diagonal), Polarizing Beam Splitter ($PBS$), and dual Single-Photon Avalanche Detectors ($SPADs$).
* **Blue Math Card:** Full mathematical and algebraic proof of the non-commuting measurement commutator:
  $$[M_+, M_0] = |+\rangle\langle+| |0\rangle\langle0| - |0\rangle\langle0| |+\rangle\langle+| = \frac{1}{2}\begin{pmatrix} 0 & -1 \\ 1 & 0 \end{pmatrix} \neq 0$$
  explaining why measuring in one basis disturbs the other, providing the mathematical foundation of QKD security.

### Scene B: Jinan-1 Satellite-to-Ground Bidirectional Optical Link (Reference Image 1, Panels a–d)
* **Panel a (Earth Orbit View):** Low-Earth-Orbit (LEO) satellite link budget at $550\text{ km}$ altitude with multiplexed optical beams:
  * $850\text{ nm}$ Quantum Channel (downlink single-photon pulses)
  * $812\text{ nm}$ Classical Downlink (basis announcement and synchronization)
  * $1,538\text{ nm}$ Classical Uplink (error correction and acknowledgement)
  * $532\text{ nm}$ Green Beacon Laser (satellite pointing reference)
  * $785\text{ nm}$ NIR Beacon Laser (ground tracking reference)
* **Panel b (Fibre Optics Module):** $850\text{ nm}$ QLD, Optical Isolator, Phase Modulators (PM1, PM2), Circulator (PCIR), and WDM multiplexing.
* **Panel c (Satellite Payload Optics):** $180\text{ mm}$ Cassegrain transmitter telescope, Fast Steering Mirror (FSM1), tracking cameras (CAM1, CAM2), dichroic mirrors (DM1, DM2).
* **Panel d (Ground Station Receiver):** $1\text{ meter}$ optical receiver antenna, Beam Expander (BE), Fast Steering Mirror (FSM2), tracking cameras (CAM3, CAM4), bandpass daylight suppression filters (F4–F6), HWP, PBS, and SPAD detectors (ports III, IV, V).

### Scene C: 3D Bloch Sphere
* Real-time geometric visualization of qubit states:
  * North Pole $|0\rangle = |H\rangle$, South Pole $|1\rangle = |V\rangle$
  * Equator states $|+\rangle = |D\rangle$, $|-\rangle = |A\rangle$, $|R\rangle$, $|L\rangle$
  * Real-time state vector rotation synchronized with Alice and Bob's optical adjustments.

---

## 🚀 Quickstart & Local Host

### 1. Install & Build
```bash
npm install
npm run build
npm test
```

### 2. Run Localhost Server
```bash
# Development mode
npm run dev

# Or production preview
npm run preview
```
Open [http://localhost:5173](http://localhost:5173) in your browser.

---

## 📐 Architecture & Layers

```
src/
├── core/                  # Pure TypeScript, zero rendering imports, fully tested
│   ├── math/              # Complex numbers, Matrix2x2, commutators, Vector2 Jones states
│   ├── optics/            # Polarizers, Waveplates (HWP/QWP), PBS, BS, AM, PM, SPADs
│   ├── protocol/          # BB84 protocol engine, sifting, Cascade EC, privacy amplification
│   ├── attacks/           # Intercept-resend (25% QBER), PNS vulnerability, decoy states
│   ├── channels/          # Free-space satellite link budget vs exponential fiber loss
│   └── rng.ts             # Deterministic Mulberry32 PRNG
├── scenes/                # Three.js 3D WebGL2 scene graphs & camera directors
│   ├── BB84BenchScene.ts  # Scene A: Tabletop optical bench
│   ├── SatelliteScene.ts  # Scene B: Jinan-1 panels a-d with zoom hierarchy
│   ├── BlochSphereScene.ts# Scene C: Interactive Bloch sphere
│   └── SceneManager.ts    # WebGL2 renderer, UnrealBloomPass, raycaster hit-testing
├── components3d/          # Procedural optical hardware factories (lasers, mounts, telescopes)
├── render/                # Custom GLSL shaders (traveling laser pulses, glow)
├── lessons/               # 10 Progressive learning modules (0 to 9) with dual-depth content
├── state/                 # Zustand global reactive store
└── ui/                    # React UI overlays, HUD, KaTeX MathPanel, Sandbox, Quizzes
```

---

## 🧪 Scientific References

1. **BB84 Protocol:** Bennett, C. H., & Brassard, G. (1984). *Quantum cryptography: Public key distribution and coin tossing*. IEEE International Conference on Computers, Systems and Signal Processing.
2. **No-Cloning Theorem:** Wootters, W. K., & Zurek, W. H. (1982). *A single quantum cannot be cloned*. Nature, 299(5886), 802–803.
3. **Decoy-State Method:** Lo, H.-K., Ma, X., & Chen, K. (2005). *Decoy State Quantum Key Distribution*. Physical Review Letters, 94(23), 230501.
4. **Jinan-1 Satellite Link:** Research Team (2022). *Real-time key distillation for satellite-to-ground quantum key distribution with micro-satellite Jinan-1*. Nature / Nature Photonics.
