# Plan: The Magical Reveal (Pledge & Turn)

## Concept Insights
The success of this "magic trick" depends on **Synchronicity** and **Contrast**.
1.  **Pattern Interrupt:** The "Snap" (Turn) must be loud and crisp to break the prospect's trance from the "Glow" (Pledge).
2.  **Stealth Trigger:** Since detecting an actual snap via microphone is unreliable in noisy marketing environments, we will implement a **Full-Screen Stealth Tap**. Any touch on the screen triggers the Turn.
3.  **Visual Contrast:** The Pledge should feel "organic" (blurred, moving gradients), while the Prestige (the Card) should feel "digital and structured."

---

## Phase 1: The Pledge (The Glowing Mesh)
**Goal:** Create a mesmerizing, high-end mesh gradient that looks "expensive" and high-tech.

### Technical Implementation:
*   **Method:** CSS-only animated gradients or a lightweight Canvas script (e.g., `Gradient.js`).
*   **Aesthetics:** 
    *   Colors derived from `Marketing card.png`: Deep Purple (#6366f1), Electric Pink (#ec4899), and Cyan (#06b6d4).
    *   `filter: blur(60px)` to create the "glow" effect.
    *   Slow, non-repeating movement to keep the eye moving.
*   **Fullscreen Mode:** Use the Web Manifest `display: fullscreen` and a JS `requestFullscreen` toggle to hide the address bar.

---

## Phase 2: The Turn (The Snap & Transition)
**Goal:** Create an instant, visceral transition triggered by the marketer.

### Technical Implementation:
*   **The Trigger:** A `pointerdown` listener on the `window`.
*   **The Audio:** 
    *   Pre-load a high-quality "Digital Snap" or "Magic Whoosh" sound.
    *   Use the **Web Audio API** instead of standard `<audio>` tags to ensure zero-latency playback.
*   **The Visual Shift:**
    *   Instantly remove the `blur` filter and mesh animation.
    *   Trigger a "Flash" effect (white overlay at 0.1s duration) to mask the swap between the gradient and the image.
    *   Reveal `Marketing card.png` with a slight "pop" scale animation (0.95 -> 1.05 -> 1.0).

---

## Implementation Steps

### 1. PWA & Shell
*   [ ] Create `manifest.json` with `display: fullscreen` and `orientation: portrait`.
*   [ ] Set up a basic `index.html` with a `#stage` container.

### 2. The Pledge (Gradient)
*   [ ] Implement the mesh gradient using CSS `@keyframes`.
*   [ ] Add a "Glow" overlay using `backdrop-filter`.

### 3. The Turn (Interaction & Audio)
*   [ ] Integrate Web Audio API for the "Snap" sound.
*   [ ] Implement the "Stealth Tap" logic to transition states.
*   [ ] Add the "Flash" mask and "Scale Pop" animation for the Prestige reveal.

---

## Verification & Polish
*   **Latency Check:** Measure time between tap and audio play (must be < 50ms).
*   **Safe Areas:** Ensure the card content doesn't hit the notch or home indicator on iOS/Android.
*   **Offline Support:** Configure Service Worker to cache the sound and the card image for 100% reliability without internet.
