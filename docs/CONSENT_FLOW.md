# Consent Flow — Screen-by-Screen Spec

Status: Draft for Phase 4 implementation. Defined now, in Phase 1, so downstream phases build
toward it rather than bolting consent on afterward.

## Principle

The user cannot reach the generation step without passing through every screen below, in
order. None of these are dismissible with a single "accept all" — each requires a distinct,
affirmative action.

## Screen 1 — Rights confirmation (before any file is even opened)

> "Before you upload, please confirm: this is a conversation you were personally part of, or
> you have permission from everyone involved to use it here."

- Checkbox (required, unchecked by default): *"I confirm I have the right to use this
  conversation."*
- No pre-checked boxes, anywhere, ever.

## Screen 2 — Sensitive data review (after on-device parsing + PII scan)

> "We found the following in your conversation. Review each one — you can remove or keep
  it."

- Each detected PII span (phone number, address, financial detail, etc.) shown with
  surrounding context, an individual **Remove** / **Keep** toggle, defaulting to **Remove**
  for financial account numbers, passwords, and government ID numbers specifically (these
  require an explicit extra confirmation step to keep).

## Screen 3 — Message-level edit

> "Edit or exclude anything before we continue — nothing beyond this point can include a
  message you've removed here."

- Full message list, delete/edit per line, exclude-speaker option.

## Screen 4 — Character assignment

> "Choose a look for each person in this conversation."

- Stylized avatar picker only (Ready Player Me stylized presets) — no upload-a-photo-and-
  auto-generate-a-realistic-face path exists in this product.

## Screen 5 — Final confirmation before generation

> "Here's what will be used to generate your video: [redacted scene summary shown in plain
  language]. This is what we'll send to generate your video — nothing else from your
  conversation leaves this device."

- Explicit **Generate** button; no auto-proceed.

## Deletion — always reachable

Every screen and every completed project has a visible, one-step **Delete this
conversation** action — not buried in settings. See `RETENTION_POLICY.md` for what deletion
actually removes.
