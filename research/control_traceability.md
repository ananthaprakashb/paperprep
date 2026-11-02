# Control-to-Reference Traceability

| Proposed control | Primary foundation | Verification / evidence |
|---|---|---|
| Payment token domain restriction | EMVCo Payment Tokenisation (P01), PCI SSC (P02) | Reject instrument use outside permitted merchant/device/domain |
| Agent delegation provenance | RFC 8693 (I03) | Preserve subject vs actor across exchanges |
| Audience binding | RFC 8707 (I04), MCP authorization (A02) | Reject token issued for another MCP server |
| Proof of possession | RFC 9449 (I06), RFC 8705 (I05) | Reject token theft/replay in appropriate transport models |
| Narrow economic authority | OPA (A07), Cedar (A08), proposed policy contract | Evaluate amount, merchant, currency, beneficiary and payment stage |
| Portable workload identity | SPIFFE (H01), SPIRE (H02) | Cross-cloud identity with constrained federation |
| Credential lifecycle | NIST SP 800-57 (I12), Vault Transit (H07) | Rotation, key custody and revocation |
| No token passthrough | MCP security best practices (A03) | Tool receives only its own intended credentials |
| Payment retry safety | Stripe (P07), Adyen (P08), AWS retry guidance (T03) | Timeout-unknown and reconciliation before renewed side effect |
| Durable decision evidence | NIST SP 800-53 (T06), W3C Trace Context (T05) | Correlate agent intent, policy decision and PSP result |
| Human oversight of irreversible operations | NIST AI RMF (A06), SRE Workbook (T04) | Explicit approval and complete action provenance |

IDs refer to the [knowledge base](../knowledge-base/token_aware_ai_agents_resources.md). The matrix distinguishes external foundations from application-specific design decisions; none of the standards alone establishes end-to-end financial correctness.
