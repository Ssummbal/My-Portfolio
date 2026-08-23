# PRD: Number-Reuse Verification Flow

## Problem Statement
When a carrier reissues a phone number, downstream services (social, financial, or otherwise) have no reliable way to distinguish the new legitimate owner from a still-active old account. This creates silent lockouts with no resolution path.

## Goal
Give new number owners a clear, low-friction way to verify legitimate use, while ensuring any identity- or finance-adjacent account change still requires human confirmation.

## Non-Goals
- This does not attempt to solve carrier-side number reissuance policy.
- This does not propose removing human review from any financial or identity-verification step, regardless of AI confidence level.
- This does not cover disputes where both parties claim legitimate ownership; that's an escalation case, not a resolution the system should attempt to close on its own.

## Requirements
- System must classify account type by risk tier (low: social/non-financial, high: identity/financial) before applying any automated resolution path.
- Low-risk flows may use AI-assisted re-verification (backup email, ID prompts).
- High-risk flows must route to a human reviewer before any account state changes.
- Carrier-side number-reuse status should be checked at signup, not only at login.
- User-facing error messaging must explain *why* access was blocked, not just that it was.

## Edge Cases
- Old account is dormant but not deleted, no clear signal of abandonment.
- User attempts signup on multiple services simultaneously, creating parallel verification requests.
- Old owner disputes the reassignment after a new account has already been verified.

## Success Metrics
- Reduction in unresolved, silent lockouts on reused numbers.
- No increase in unauthorized access to high-risk (identity/financial) accounts.
- Time-to-resolution for low-risk cases, measured from first block to verified access.
