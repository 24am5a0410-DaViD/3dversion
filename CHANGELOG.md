# 📝 Changelog

## [1.0.0] - 2026-10-02

### Added
- **Core Linear Algebra & Physics Engine:**
  - Complex number calculus, Matrix2x2 algebraic operators, commutator $[A, B]$, trace, and dagger.
  - Jones state vectors, normalization, Born rule measurement projections, and Bloch sphere coordinate mapping.
  - Optical element operators: Polarizers (H, V, D, A), Half-Wave Plate (HWP), Quarter-Wave Plate (QWP), Phase Modulators (PM), Amplitude Modulators / Attenuators (AM), 50:50 Beam Splitters (BS), Polarizing Beam Splitters (PBS), and Single-Photon Avalanche Detectors (SPADs).
  - Full BB84 protocol simulation: pulse preparation, quantum channel transit, Bob detection, basis sifting, QBER estimation, Cascade-like error correction leakage, privacy amplification, and hex distilled secret key.
  - Attack models: Intercept-resend (converging to ~25% QBER), photon-number-splitting (PNS) vulnerability, and decoy-state analysis.
  - Physical channel models: Free-space diffraction link budget (Jinan-1 specs) vs exponential terrestrial optical fiber attenuation (220 dB / 100 km).
- **Interactive 3D WebGL2 Scenes:**
  - **Scene A (BB84 Tabletop Bench):** Reconstructed from Reference Image 2 with Alice's H/A/D/V laser sources, beam splitters, AM-PM-AM modulation chain, channel Eve tap, Bob's HWP, PBS, and SPAD detectors.
  - **Scene B (Satellite-to-Ground Link):** Reconstructed from Reference Image 1 (panels a-d) with Earth orbit view, satellite Cassegrain telescope, ground station 1-meter receiver, Fast Steering Mirrors (FSM1, FSM2), tracking cameras (CAM1-CAM4), and multiplexed wavelengths (850, 812, 1538, 532, 785 nm).
  - **Scene C (Bloch Sphere):** Unit sphere showing $|0\rangle$, $|1\rangle$, $|+\rangle$, $|-\rangle$ basis vectors and dynamic state vector rotation.
- **Visuals & Shaders:**
  - Custom GLSL traveling laser wavepacket shader.
  - Multi-pass postprocessing with UnrealBloomPass for authentic laser glow.
  - Interactive 3D component hit-testing and raycasting.
- **UI & Learning Interface:**
  - Exact Blue Math Panel reproducing the non-commuting measurement commutator proof:
    $[M_+, M_0] = 1/2 [[0, -1], [1, 0]] \neq 0$ with the "Important for QKD" ribbon.
  - Live Telemetry HUD: Real-time QBER indicator, security limit alert, sifted bit rate, distilled hex key, and live pulse sifting table.
  - 10 Progressive Modules (0 to 9) with dual-depth learning: "Explain Like I'm 12" intuition vs "Show Me The Math" derivations with KaTeX.
  - Interactive knowledge quizzes for each module with instant feedback and explanations.
  - Interactive Sandbox & Attack Lab with Alice/Bob state encoders, Eve intercept slider, and channel loss controls.
- **Verification & Testing:**
  - Vitest test suite with 7 comprehensive unit tests verifying physics identities, the commutator proof from Image 2, and protocol metrics.
