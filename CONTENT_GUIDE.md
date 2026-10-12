# 📚 Content & Curriculum Authoring Guide

## How to Author New Lessons

All lessons are defined in `src/lessons/curriculum.ts` conforming to the `LessonModule` interface:

```typescript
export interface LessonModule {
  id: number;                          // Sequential index (0 to 9)
  title: string;                       // Primary module heading
  subtitle: string;                    // Educational scope
  sceneId: 'bb84' | 'satellite' | 'bloch';
  satelliteView?: 'orbit' | 'payload' | 'fiber' | 'ground';
  learningObjectives: string[];        // 3 actionable student goals
  eli12Intuition: string;              // "Explain like I'm 12" analogy
  formalMathTitle: string;             // Math heading
  formalMathLatex: string;             // KaTeX equation string
  formalMathDerivation: string[];      // Step-by-step mathematical derivation
  interactiveGoal: string;             // Hands-on mission prompt
  quiz: QuizQuestion[];                // Multiple-choice questions with explanations
  references: { title: string; citation: string; year: number }[];
}
```

## Adding Optical Components

To register a new optical lab or spacecraft element:
1. Define procedural geometry and material in `src/components3d/opticalComponents.ts` using `OpticalComponentFactory`.
2. Attach `userData` conforming to `OpticalObjectUserData`:
   * `id`: Unique identifier
   * `name`: Display title
   * `formulaLatex`: Mathematical transformation operator
   * `eli12`: Intuitive description
   * `description`: Rigorous engineering specification
3. Add the component to `BB84BenchScene.ts` or `SatelliteScene.ts` and append to `interactiveObjects` to enable click-to-inspect.
