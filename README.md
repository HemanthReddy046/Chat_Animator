# Chat-to-Video

Turn your conversations into stories — while keeping your conversations yours.

Chat-to-Video parses an exported chat log, detects plans and events discussed in it, and
generates a short animated video of two customizable 3D characters acting the moment out —
with voiceover in the user's own language.

This repository is being built in **10 phases** per `docs/PROJECT_BLUEPRINT.md` (see the
planning PDF shared alongside this repo). We are currently in **Phase 1: Foundations —
Legal, Privacy & Architecture Design**.

## Non-negotiable design rules (read before contributing)

1. **Local-first.** Raw chat text is parsed and PII-scanned on-device. It never leaves the
   device unless explicitly stated otherwise in `docs/DATA_FLOW.md`.
2. **Redacted-only external calls.** The only things ever sent to an external service are
   (a) a redacted scene summary for intent extraction, and (b) plain dialogue text (no
   names/PII) for text-to-speech.
3. **Stylized avatars, not deepfakes.** No photoreal likeness generation of real people
   without their own explicit consent step.
4. **Consent and deletion are first-class screens**, not settings buried in a menu.
5. **Every generated video carries a burned-in AI-generated watermark.**

See `docs/DATA_FLOW.md`, `docs/PRIVACY_POLICY.md`, `docs/CONSENT_FLOW.md`,
`docs/RETENTION_POLICY.md`, and `docs/PLATFORM_STRATEGY.md` for the full detail behind each rule.

## Platform

Chat-to-Video is one web app (React + Three.js), shipped to desktop via **Tauri** and to
iOS/Android via **Capacitor** — see `docs/PLATFORM_STRATEGY.md` for why, and what that means
for every later phase. No feature ships if it
violates one of these five rules — that is the actual definition of done for this project,
not just the visual output.

## Repository structure

```
chat-to-video/
├── docs/                    Phase 1 deliverables: legal/privacy/architecture docs
├── src/
│   ├── parsing/             Phase 2 — on-device chat export parsing
│   ├── redaction/           Phase 3 — PII detection & redaction
│   ├── consent/             Phase 4 — consent & user control UI
│   ├── intent/              Phase 5 — intent/scene extraction
│   ├── avatar/              Phase 6 — character avatar system
│   ├── animation/           Phase 7 — animation system
│   ├── voice/                Phase 8 — text-to-speech layer
│   ├── render/               Phase 9 — video assembly & watermarking
│   └── lifecycle/            Phase 10 — data lifecycle & abuse prevention
├── public/
└── .github/workflows/       CI pipeline
```

Each `src/` subfolder stays empty (with a `.gitkeep` and a short README) until its phase
begins — we are not writing feature code before the privacy/legal foundation in Phase 1 is
signed off.

## Status

- [x] Phase 1 — Foundations (in progress)
- [ ] Phase 2 — Chat Ingestion & On-Device Parsing
- [ ] Phase 3 — PII Detection & Redaction Layer
- [ ] Phase 4 — Consent & User Control Interface
- [ ] Phase 5 — Intent & Scene Extraction
- [ ] Phase 6 — Character Avatar System
- [ ] Phase 7 — Animation System
- [ ] Phase 8 — Voice Layer
- [ ] Phase 9 — Video Assembly, AI Labeling & Rendering
- [ ] Phase 10 — Data Lifecycle, Abuse Prevention, Testing & Launch
# Chat_Animator
# Chat_Animator_007
