---
title: "Cogleaf"
date: 2026-04-15
date_display: "2026"
description: "An offline-first cognitive exercise application exploring attention training, working memory tasks, and sensory accessibility."
status: "active prototype"
domain: "Human-Computer Interaction & Cognitive Systems"
technologies:
  - "React 19"
  - "TypeScript"
  - "Vite"
  - "Three.js"
  - "Capacitor"
  - "Web Audio API"
  - "Tailwind CSS"
github: ""
demo: ""
featured: true
weight: 10
---

## Overview

**Cogleaf** is an offline-first cognitive exercise application and mindful software suite built with React 19, TypeScript, Three.js, and Capacitor. It provides an accessible, non-punitive digital environment for structured cognitive tasks—spanning visual attention, working memory updating, inhibitory control, and executive planning.

Designed as an independent product engineering project, Cogleaf investigates how computerized cognitive testing paradigms can be translated into calm, patient-friendly interfaces that prioritize sensory accessibility, client-side data privacy, and deterministic offline performance.

*(Note: The core application source code is maintained in a private repository. This document serves as the public technical architecture and design case study.)*

---

## The Problem: Friction in Cognitive Exercise Software

Computerized cognitive assessment and training tools often suffer from two extremes:
1. **Clinical / Academic Tools**: Often rely on outdated desktop runtimes, uninviting legacy UIs, and rigid visual stimuli that produce high cognitive fatigue and anxiety.
2. **Commercial "Brain Training" Apps**: Heavily gamified with bright flashing animations, high-pressure countdown timers, aggressive push notifications, and mandatory cloud tracking that monetizes user biometric and behavioral data.

Cogleaf was conceived to explore an alternative design space: **supportive, non-stigmatizing cognitive exercise software** that runs completely client-side without internet access, tracking beacons, or sensory overstimulation.

---

## Cognitive Exercise Architecture & Task Paradigms

```
                      [Cogleaf Game Hub]
                              │
         ┌────────────────────┼────────────────────┐
         ▼                    ▼                    ▼
  [Visual Attention]    [Working Memory]     [Executive Function]
   - Butterfly Safari    - N-Back Task        - Tower Planner
   - Picture Match                            - Card Sorter (WCST)
                                              - Stroop Task
                              │
                              ▼
        [Client-Side Behavioral Telemetry Engine]
        - Reaction time distributions (ms)
        - Accuracy, omission, and commission errors
        - LocalStorage schema hydration (Zero Network Transmission)
```

Cogleaf adapts six classical cognitive and neuropsychological paradigms into lightweight interactive components:

### 1. Butterfly Safari (Visual Search & Attention Tracking)
- **Cognitive Mechanism**: Selective visual attention, feature-based scanning, and distractor suppression.
- **Task Dynamics**: The user scans a dynamic, procedurally animated botanical field to identify target butterfly species defined by specific visual morphology (wing patterns, hues). The interface introduces fluttering distractor species with overlapping visual characteristics, exercising the user's ability to maintain focus amidst visual noise.
- **Scoring**: Measures identification latency, target detection rate, and false-alarm commission errors under variable distractor density.

### 2. Stroop Interference Task
- **Cognitive Mechanism**: Inhibitory control and selective attention (the Stroop effect).
- **Task Dynamics**: The user is presented with color names printed in congruent or incongruent font colors (e.g. the word "blue" printed in red ink). The user must report the ink color while suppressing the automatic reading reflex.

### 3. N-Back Working Memory Updating
- **Cognitive Mechanism**: Continuous working memory maintenance, temporal sequencing, and updating.
- **Task Dynamics**: A continuous sequence of visual stimuli is presented. The user must indicate when the current stimulus matches the one displayed $N$ steps previously ($N=1, 2$), challenging continuous buffer updating without external note-taking.

### 4. Tower Planner (Tower of London Analogue)
- **Cognitive Mechanism**: Visuospatial planning, goal-hierarchy management, and executive function.
- **Task Dynamics**: The user must rearrange a set of colored tokens across pegs to replicate a target goal configuration while respecting peg capacity rules, encouraging forward mental planning in the minimum number of transitions.

### 5. Card Sorter (Set-Shifting & Cognitive Flexibility)
- **Cognitive Mechanism**: Rule induction, perseveration suppression, and cognitive flexibility (analogue of the Wisconsin Card Sorting Test).
- **Task Dynamics**: Cards must be matched to reference decks according to implicit rules (color, geometric shape, or element count). Periodically, the sorting rule silently shifts based on user performance, evaluating how quickly the user adapts to rule changes versus perseverating on expired rules.

### 6. Picture Match (Paired-Association Memory)
- **Cognitive Mechanism**: Short-term visual recognition and spatial location memory.

---

## Technical Stack & Offline-First Implementation

- **Frontend Core**: React 19, TypeScript, Vite.
- **State & Telemetry**: React Context + custom Hooks with strict typing schemas (`types/clinical.ts`, `types/games.ts`).
- **3D Environmental Rendering**: Three.js integration across ambient interactive scenes (*Lotus Pond*, *Calm River*, *Starlight Garden*).
- **Audio Synthesizer**: Custom Web Audio API procedural sound engine (`audioSynthesizer.ts`) generating harmonic binaural drones and chime notes without loading external audio assets.
- **Cross-Platform Container**: Capacitor runtime for offline native packaging on Android and desktop environments.
- **Styling**: Tailwind CSS + Motion (Framer Motion) for fluid, physics-based transitions.

### Data Persistence & Privacy
All session data—including task trials, reaction time timestamps, accuracy percentages, and daily pacing counters—is serialized directly into `localStorage`. The application makes zero outgoing network calls during exercise execution. No telemetry or user identification leaves the local device sandbox.

---

## Sensory Accessibility & Neuro-Inclusive Design

To support users experiencing cognitive fatigue, sensory processing sensitivity, or motor coordination challenges:
1. **Pacing Controls**: Three selectable interaction speeds (`relaxed`, `balanced`, `flow`) allow users to eliminate countdown timers and engage with tasks at their own processing tempo.
2. **Reduced Motion Mode**: A global accessibility toggle disables Three.js procedural camera movements, particle emitters, and CSS transforms for users susceptible to vestibular discomfort.
3. **High-Contrast Palette**: Optimized WCAG AAA color profiles ensuring visual distinction across chromatic stimuli (especially vital during the Stroop task).
4. **Gentle Session Throttling**: A built-in daily limit module (`DailyLimitLockModal.tsx`) provides compassionate friction against compulsive over-use, gently locking sessions after predetermined time caps.

---

## Scientific Framing & Methodological Distinction

> **Important Scientific Boundary**:
> Cogleaf is an educational software engineering prototype and digital cognitive wellness exercise suite. It has **not** been clinically validated in randomized controlled trials (RCTs). It does **not** diagnose, treat, prevent, or cure any neurological, psychiatric, or psychological disorder (such as schizophrenia, ADHD, or mild cognitive impairment). 
> 
> Claims regarding cognitive tasks refer solely to the computerized implementation of established psychological paradigms, not clinically proven therapeutic outcomes.

---

## Engineering Takeaways & Future Directions

- **Canvas Memory Management**: Managing WebGL contexts within React component lifecycles required strict resource disposal (`renderer.dispose()`, geometry cleanup) to prevent memory leaks during rapid scene switching on mobile hardware.
- **Web Audio Threading**: Procedural synthesis via the Web Audio API allowed rich, reactive soundscapes while keeping bundle sizes under 1.5 MB without binary audio assets.
- **Future Roadmap**:
  - Longitudinal reporting with statistical distribution curves (e.g. tracking reaction time variability across multiple sessions).
  - WebRTC peer-to-peer data synchronization for clinician review without centralized database hosting.
