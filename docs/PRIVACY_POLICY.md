# Privacy Policy (Draft — Phase 1)

Status: **Draft.** Must be reviewed by a qualified lawyer before public launch. This draft
exists so the engineering team builds against real commitments from day one, not so it can be
published as-is.

## What this product does with your data

Chat-to-Video turns a conversation you upload into a short animated video. Here is exactly
what happens to your data, matching `DATA_FLOW.md`:

- Your chat file is read and parsed **on your device**. It is not uploaded anywhere in this
  step.
- We scan the parsed messages **on your device** for sensitive information (phone numbers,
  addresses, financial details, ID numbers) and show you what was found before anything else
  happens.
- You review, edit, or remove any message or sensitive detail before continuing.
- A **redacted summary** of the plans/events in your conversation (not your original
  messages) is sent to our AI provider to figure out what scene to animate.
- The dialogue text for your video's voiceover is sent to a text-to-speech provider — this
  text contains no names or personal details beyond what you've written into the dialogue
  itself.
- Your video is rendered and watermarked **on your device**.

## What we do not do

- We do not store your raw chat export on our servers.
- We do not generate a photorealistic likeness of a real, named person without that person
  providing their own consent.
- We do not use your conversations to train any AI model.
- We do not sell or share your data with advertisers.

## Your rights

Consistent with India's Digital Personal Data Protection Act, 2023:

- **Consent** — you control what is uploaded and must affirmatively confirm you have the
  right to use the conversation before generation begins.
- **Access & correction** — you can review and edit the redacted preview before it's used.
- **Erasure** — you can delete your uploaded chat and any generated video at any time; see
  `RETENTION_POLICY.md` for exactly what "delete" removes.
- **Grievance contact** — [to be filled in before launch: support email / grievance officer
  contact, as required under the DPDP Act].

## Data retention

By default, nothing is retained after your session ends unless you explicitly save a
project. See `RETENTION_POLICY.md` for the full detail.

## Changes to this policy

We will not change what data leaves your device (per `DATA_FLOW.md`) without updating this
policy and notifying users first.

---
*This draft has not yet been reviewed by legal counsel. Do not publish externally until it
has been.*
