# Data Flow Specification

Status: **Binding spec** — no code stage may violate this document. Any change to what leaves
the device requires updating this file first, in its own commit, with a stated reason.

## Trust boundary

The trust boundary is the user's device. Everything on the left of the line below runs
on-device; only the two rows marked "external" ever cross it, and only with the payload
described.

| # | Stage | Runs where | Data touched | Leaves device? | Payload sent externally |
|---|-------|-----------|--------------|-----------------|--------------------------|
| 1 | Chat file import | On-device | Raw export (.txt/.zip/.json) | No | — |
| 2 | Parsing to structured messages | On-device | sender, message, timestamp | No | — |
| 3 | PII detection & redaction | On-device (Presidio/DataFog) | phone numbers, addresses, financial info, IDs | No | — |
| 4 | User review / edit / consent | On-device | redacted preview | No | — |
| 5 | Intent / scene extraction | **External** (Gemini free tier) | — | **Yes** | Redacted scene summary JSON only: `{intent, participants (first name/alias only), time, tone}` — never raw message text |
| 6 | Avatar & animation rendering | On-device (WebGL/Three.js) | avatar model, animation clips | No | — |
| 7 | Voice synthesis | **External** (edge-tts) | — | **Yes** | Generated dialogue text only — no sender real names, no metadata |
| 8 | Video assembly & watermarking | On-device | rendered video | No | — |

## Rules that follow from this table

1. **No raw message text ever appears in an outbound network request.** This must be
   verifiable by inspecting the network tab during a real generation run, not just by code
   review — add this as an automated test in Phase 5 (mock the network layer and assert on
   payload contents).
2. **Participant identifiers sent to the LLM are aliases, not real names**, unless the user
   has explicitly opted to use real names in the output (a separate, explicit toggle — off by
   default).
3. **Nothing is cached server-side.** If a caching layer is ever introduced for performance,
   it must cache on-device (e.g. IndexedDB), not on a server the team operates.
4. **Any new stage added in a later phase must be added to this table before it ships**, with
   an explicit "leaves device?" answer.

## Open questions to resolve before Phase 5

- Exact JSON schema for the redacted scene summary (finalize in Phase 5 planning).
- Whether the free-tier LLM provider's own data-retention policy is acceptable — review
  Gemini API's data usage terms before Phase 5 begins, since "free tier" does not
  automatically mean "does not log requests."
