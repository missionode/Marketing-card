Here is the detailed Product Requirement Document (PRD) and Technical Specification for your hard-mode Tic-Tac-Toe web application. This document outlines the complete scope, architecture, and mathematical constraints required to build a flawless, installable Progressive Web App (PWA).

---

# Product Requirement Document (PRD)

## Project Name: Perfect Zero (Hard-Mode Tic-Tac-Toe PWA)

### 1. Executive Summary & Objective

The objective is to create a hyper-minimalist, high-performance, single-player Tic-Tac-Toe game. The core mechanic relies on a deterministic AI powered by the Minimax algorithm, ensuring the human player can **never win**. The game alternates initial advantages using a random coin toss, offering exactly two final outcomes: an **AI Victory** or a **Stalemate (Tie)**. The app is delivered as an installable, offline-capable Progressive Web App (PWA) with a premium "Warm Minimalist" aesthetic.

### 2. Core User Flow & Screen Requirements

The application operates as a Single Page Application (SPA) transitioning across three distinct views based on reactive state management:

```
[ View 1: The Toss ] ──(Auto-Transition)──> [ View 2: Gameplay ] ──(3s Delay)──> [ View 3: Two Outcomes ]
  - Digital Coin Flip                        - 3x3 Grid Matrix                     - Screen A: AI Victory
  - Determines 1st Turn                      - Unbeatable Minimax AI               - Screen B: Stalemate

```

#### View 1: The Coin Toss Screen

* **Trigger:** Loads immediately upon application initialization or game reset.
* **Behavior:** A rapid, animated digital coin toss animation runs automatically for 1.5 seconds.
* **Outcome:** Randomly assigns the starting player ($50\%$ probability for AI, $50\%$ probability for Human).
* **UI Elements:** Displays a dynamic status banner reading either `"AI Plays First"` or `"Human Plays First"`.
* **Transition:** Automatically transitions to View 2 after a 1-second delay post-toss.

#### View 2: The Interactive Gameplay Board

* **Grid:** A highly responsive $3 \times 3$ grid layout optimized for both desktop viewports and 9:16 mobile form factors.
* **Turn Handling:**
* If **AI Plays First**: The AI immediately selects the mathematically optimal opening move.
* If **Human Plays First**: The grid unlocks, waiting for valid user input.


* **Interaction Constraints:** Cells already populated with a token (`X` or `O`) become pointer-insensitive. During the AI's computation phase, the entire grid layer is shielded to block accidental user taps.
* **Resolution:** The moment a terminal game state is detected (3 matching tokens in a row, column, or diagonal, or 9 tiles filled with no winner), the board freezes. The winner's name (`AI` or `Stalemate`) is displayed on a localized overlay for exactly 3 seconds before routing.

#### View 3: Dedicated Outcome Screens

The application switches to a full-screen, high-impact landing view matching the final game state:

* **Screen A (AI Victory):** A premium, dominant layout communicating the system's flawless performance. Features a call-to-action button to "Try Again".
* **Screen B (Stalemate / Draw):** A respectful "Absolute Defense" layout acknowledging the user's perfect execution for holding off a flawless engine. Features a call-to-action button to "Challenge Again".

---

## Technical Specifications & Architecture

### 1. Technology Stack & Dependencies

* **Core Structure:** Semantic HTML5, Vanilla ECMAScript 6+ JavaScript.
* **Styling Engine:** Tailwind CSS via the unified browser compilation script:
```html
<script src="https://cdn.jsdelivr.net/npm/@tailwindcss/browser@4"></script>

```



```
*   **Typography:** Managed via `@tailwindcss/typography` utilities for clean, structured layouts.
*   **Icons & Assets:** Vector-based inline SVG graphics to remove external HTTP image dependencies and guarantee instant load times.

### 2. PWA & Offline Requirements
To achieve a native standalone application experience, the architecture must support explicit PWA standards:
*   **Web App Manifest (`manifest.json`):** Must configure a standalone display mode, a `theme_color`, background colors matching the layout palette, and explicit icon arrays ($192\text{px}$ and $512\text{px}$).
*   **Service Worker (`sw.js`):** Implement a Cache-First network strategy. It must pre-cache all essential structural shells (`index.html`, manifest, locally declared configurations, and fonts) during the `install` event to allow immediate offline launch capability.

### 3. The AI Engine: Minimax Algorithm Math
The game's unbeatable behavior is driven by an un-pruned recursive Minimax evaluation function. The algorithm treats the game board as an array of 9 elements and assigns deterministic scoring matrix values to terminal states from the perspective of the AI:

$$\text{Score} = \begin{cases} +10 & \text{if AI wins} \\ -10 & \text{if Human wins (mathematically unreachable)} \\ 0 & \text{if Draw} \end{cases}$$

For every turn, the algorithm simulates all remaining permutations of the match, choosing the path that maximizes the AI's score when it is the AI's turn, and assumes the human player will select moves that minimize the AI's score.


```

```
   [Current Board State]
      /      |      \
 Move A    Move B   Move C
  (+10)     (0)      (-10)
    |

```

[AI Selects Move A]

```

### 4. Data Layer Architecture (JSON Configuration)
To maintain strict separation of concerns, no presentation text, header typography, or content messages are hardcoded inside the DOM nodes. All copy is managed via a centralized immutable configuration object:

```json
{
  "branding": {
    "title": "Perfect Zero",
    "tagline": "The Unbeatable Matrix"
  },
  "tossScreen": {
    "searchingText": "Flipping Coin...",
    "aiFirstText": "AI Wins Toss - Commencing Simulation",
    "humanFirstText": "You Win Toss - Make Your Move"
  },
  "outcomeScreens": {
    "victory": {
      "headline": "System Dominance Achieved",
      "subline": "The AI calculated every timeline. Your defeat was mathematically inevitable.",
      "buttonText": "Re-engage Matrix"
    },
    "draw": {
      "headline": "Flawless Stalemate",
      "subline": "Impressive. You executed perfect play to hold off an optimal engine.",
      "buttonText": "Test Your Focus Again"
    }
  }
}

```

---

## Visual Design & Aesthetics Specification

Following pair-programming design protocols, the interface aligns with premium, modern software trends:

* **Color Palette:** Warm Minimalism.
* Background Base: Slate-50 / Zinc-50 (Ultra-clean, soft light mode).
* Card & Elements: White with fine Slate-200 borders and subtle drop shadows (`shadow-sm`).
* Accent Colors: Sophisticated Indigo-600 / Emerald-600 for token symbols and interaction highlights.


* **Typography:** Large, high-contrast title scales utilizing Tailwind's modern sans-serif stack, tracking adjustments (`tracking-tight`), and heavy font weights for primary statuses.
* **Layout Safety:** All interactive elements maintain a minimum target size of $48 \times 48\text{px}$ to comply with mobile accessibility standards.

---

I have formulated the complete structural blueprint and algorithmic logic required for this application based on these exact specifications. **Please confirm if these specifications are fully aligned with your vision**, and I will generate the complete, single-shot script to build the entire workspace!