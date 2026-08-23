# PRD: Identity Conflict Intake Flow

## Problem Statement
Chatbot-driven intake for identity conflicts often either over-automates (auto-resolving cases that need human judgment) or fails unsafely (generic fallback messages when it can't resolve something). Neither protects the user or the business.

## Goal
Design an intake flow that resolves low-risk formatting or clerical conflicts directly, while guaranteeing that any conflict touching identity or account ownership reaches a human reviewer with clean, complete context, no repeated questions for the user.

## Non-Goals
- This does not attempt to increase the percentage of cases the bot resolves automatically. That's not the success metric.
- This does not propose confidence-threshold tuning as a substitute for a hard category rule. Confidence scores are not used to override the human-handoff requirement under any circumstance.
- This does not cover the human review process itself, only the handoff into it.

## Requirements
- Every intake must be classified into one of two categories before any resolution attempt: identity/ownership-related, or clerical/non-identity.
- Identity/ownership cases route to a human automatically, with full conversation context attached, no re-entry required from the user.
- Clerical cases may be resolved directly by the bot, but every auto-resolution is logged for periodic spot-check review.
- Fallback messaging must always state what happens next (e.g. "this has been sent to a specialist") rather than a generic retry prompt.

## Edge Cases
- A conflict starts as clerical but reveals identity risk mid-conversation (e.g. a name correction that also involves a mismatched ID number).
- User provides conflicting information across multiple messages.
- High-volume periods where human review queues back up, does the user get a status update, and how often.

## Success Metrics
- Zero identity/ownership cases auto-resolved without human review.
- Reduction in user-reported "stuck in a loop" incidents on clerical cases.
- Time from conflict reported to human handoff, for identity cases specifically.
