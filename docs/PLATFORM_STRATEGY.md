# Platform Strategy — Mobile & Desktop Compatibility

Status: **Binding decision.** Recorded in Phase 1 so Phase 2 onward is built against a single
target, not retrofitted for multiple platforms later.

## Decision

Chat-to-Video is built as **one web application** (React + Three.js / React Three Fiber),
shipped to every platform via a thin native shell rather than rewritten per-platform.

| Target | Shell | Notes |
|--------|-------|-------|
| Desktop (browser) | None — the web app itself | Primary development target |
| Desktop (installed app) | [Tauri](https://github.com/tauri-apps/tauri) — free, open-source, Rust-based | Wraps the web build into a native binary (.exe/.dmg/.AppImage); far lighter than Electron |
| iOS / Android | [Capacitor](https://github.com/ionic-team/capacitor) — free, open-source (Ionic) | Wraps the same web build into an installable native app; provides native API bridges (file system, share sheet) only where actually needed |

## Why not React Native + expo-gl for the 3D rendering

React Three Fiber does support React Native via `expo-gl`, but as of this decision:

- Apple has deprecated OpenGL on iOS, which `expo-gl` depends on — native iOS rendering is
  actively breaking on modern devices.
- There are current version-mismatch issues between `@react-three/fiber` and Expo SDK's
  `expo-gl` releases that break native builds.

Fighting this stack would mean maintaining a second, platform-specific rendering
implementation for the single hardest part of the product (Phase 7's avatar/animation
system) — directly against the "reuse, don't fork" spirit of the rest of this plan. The
web-shell approach avoids this entirely: the exact same WebGL code runs in the browser, in
Tauri's webview, and in Capacitor's webview.

## Consequences for later phases

- **Phase 2 (parsing) and Phase 3 (redaction)** run identically across all shells — no
  platform-specific code needed.
- **Phase 6/7 (avatar & animation)** are built once, against standard browser WebGL, and
  never touch native rendering APIs.
- **Phase 9 (video rendering/export)** should be tested specifically inside both Tauri and
  Capacitor webviews, not just desktop Chrome — canvas capture / `MediaRecorder` API support
  can differ by webview engine.
- Native file-system access for saving/deleting projects (Phase 10) will use Capacitor's/
  Tauri's filesystem plugins where the browser's own storage APIs aren't sufficient — this
  is the only place platform-specific code is expected to appear.

## Trade-off accepted

Capacitor-wrapped apps are heavier and can render 3D noticeably slower than a fully native
app on older/low-end Android devices. Accepted for the MVP in exchange for a single codebase
across desktop, iOS, and Android, and for keeping the privacy architecture in `DATA_FLOW.md`
identical on every platform. Revisit only if performance testing in Phase 7/9 shows this is
unacceptable on the team's actual target devices.
