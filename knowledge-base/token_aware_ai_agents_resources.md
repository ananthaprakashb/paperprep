# Knowledge Base: Token-Aware AI Agents for Secure Transaction Orchestration

Version: 1.0 | 2026-11-01 | Purpose: a source-linked, progression-based research library. Priority: official standards, specifications, primary project documentation and selected foundational literature. Bibliographic information should be checked against the specific version and publication before submission.

## Terminology and scope
- **EMV payment token**: payment credential surrogate usable under defined domain constraints; *not* an OAuth access token.
- **Vault or PSP token**: token/alias issued by a payment-service provider or internal vault; portability and domain restrictions are provider-specific.
- **OAuth access token**: delegated API authorization artifact, subject to audience/scope/lifetime and sender constraints.
- **Workload identity token/SVID**: machine/service identity attestation. Authentication is not payment authorization.
- **Capability token**: application-specific narrowly bounded proof of authority; design proposal, not an automatic PCI exemption.
- **LLM tokens**: model input/output units; cannot replace security identity or financial entitlements.

## Level 1 — Financial transactions and payment tokenization
| ID | Primary resource | Focus |
|---|---|---|
| P01 | [EMVCo Payment Tokenisation](https://www.emvco.com/emv-technologies/payment-tokenisation/) | Token roles, domain restriction, token requestor and ecosystem; technical framework v2.4 dated July 9, 2026 |
| P02 | [PCI SSC document library](https://www.pcisecuritystandards.org/document_library/) | PCI DSS and tokenization guidance: check exact current documents and scoping |
| P03 | [PCI DSS overview](https://www.pcisecuritystandards.org/standards/pci-dss/) | Account-data security controls; tokenization does not automatically remove compliance obligations |
| P04 | [ISO 20022](https://www.iso20022.org/) | Financial messaging semantics across rails |
| P05 | [BIS CPMI-IOSCO PFMI](https://www.bis.org/committees/cpmi/pfmi/overview) | Settlement, operational risk and financial market infrastructure principles |
| P06 | [EMVCo 3-D Secure](https://www.emvco.com/emv-technologies/3-d-secure/) | Card-not-present authentication and separate authentication/authorization responsibilities |
| P07 | [Stripe Idempotent Requests](https://docs.stripe.com/api/idempotent_requests) | PSP-specific idempotency behavior; not a universal exactly-once guarantee |
| P08 | [Adyen API idempotency](https://docs.adyen.com/development-resources/api-idempotency/) | Provider-specific retry behavior and token scope |

**Read-first:** P01, P02, P07. Research risk: payment token lifecycle, merchant/domain restrictions, card-on-file and account updates, cryptograms, lost contextual authorization and failures after payment effects.

## Level 2 — Delegation, identity, and cryptographic authorization
| ID | Primary resource | Focus |
|---|---|---|
| I01 | [RFC 6749: OAuth 2.0](https://www.rfc-editor.org/rfc/rfc6749) | Framework and grants |
| I02 | [RFC 9700: OAuth 2.0 Security Best Current Practice](https://www.rfc-editor.org/rfc/rfc9700) | Modern OAuth threat mitigation |
| I03 | [RFC 8693: OAuth 2.0 Token Exchange](https://www.rfc-editor.org/rfc/rfc8693) | Subject/actor delegation and exchanging scoped tokens |
| I04 | [RFC 8707: Resource Indicators](https://www.rfc-editor.org/rfc/rfc8707) | Audience/resource-bound tokens |
| I05 | [RFC 8705: OAuth Mutual-TLS](https://www.rfc-editor.org/rfc/rfc8705) | Certificate-bound access tokens |
| I06 | [RFC 9449: OAuth DPoP](https://www.rfc-editor.org/rfc/rfc9449) | Sender-constrained access tokens and proof of possession |
| I07 | [RFC 7519: JWT](https://www.rfc-editor.org/rfc/rfc7519) | Token claims and validation |
| I08 | [RFC 7517: JSON Web Key](https://www.rfc-editor.org/rfc/rfc7517) | Public-key representation and rotation |
| I09 | [RFC 7662: Token Introspection](https://www.rfc-editor.org/rfc/rfc7662) | Authorization-state checks |
| I10 | [RFC 7009: Token Revocation](https://www.rfc-editor.org/rfc/rfc7009) | Revocation model limitations |
| I11 | [NIST SP 800-207 Zero Trust Architecture](https://csrc.nist.gov/pubs/sp/800/207/final) | Identity- and resource-centered security |
| I12 | [NIST SP 800-57 Part 1](https://csrc.nist.gov/pubs/sp/800/57/pt1/r5/final) | Key-management lifecycle |

**Design note:** identify issuer, audience, authorized actor, subject, credential binding, permissible operation, amount/currency/merchant constraints, expiration, replay protection and revocation checks; do not assume generic OAuth scope alone encodes all financial constraints.

## Level 3 — Agent protocols, AI security and machine authority
| ID | Primary resource | Focus |
|---|---|---|
| A01 | [Model Context Protocol specification](https://modelcontextprotocol.io/specification/2025-11-25) | Agent-to-tool interoperability |
| A02 | [MCP authorization](https://modelcontextprotocol.io/specification/2025-11-25/basic/authorization) | OAuth resource/audience validation for HTTP transport |
| A03 | [MCP security best practices](https://modelcontextprotocol.io/specification/2025-11-25/basic/security_best_practices) | Token passthrough, confused deputy and misuse |
| A04 | [OWASP Top 10 for LLM Applications](https://genai.owasp.org/llm-top-10/) | Prompt injection and excessive agency |
| A05 | [OWASP Agentic AI Security](https://genai.owasp.org/) | Agent-specific emerging risks; validate publication/version |
| A06 | [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) | Governance, evaluation and accountability |
| A07 | [Open Policy Agent](https://www.openpolicyagent.org/docs) | Externalized deterministic policy evaluation |
| A08 | [Cedar policy language](https://docs.cedarpolicy.com/) | Verified policy language and evaluation model |
| A09 | [Google Zanzibar paper](https://research.google/pubs/zanzibar-googles-consistent-global-authorization-system/) | Distributed authorization design at scale |

**Research gap:** MCP transport authorization is necessary but insufficient to validate an agent's *economic authority* for a specific amount, merchant, instrument, beneficiary and point in the transaction state machine.

## Level 4 — Hybrid-cloud identity, isolation, credentials
| ID | Primary resource | Focus |
|---|---|---|
| H01 | [SPIFFE concepts](https://spiffe.io/docs/latest/spiffe-about/overview/) | Portable service identities |
| H02 | [SPIRE documentation](https://spiffe.io/docs/latest/spire-about/) | Attestation, workload identities and federation |
| H03 | [SPIRE scaling guide](https://spiffe.io/docs/latest/planning/scaling_spire/) | Federation and availability at scale |
| H04 | [AWS IAM Roles Anywhere](https://docs.aws.amazon.com/rolesanywhere/latest/userguide/introduction.html) | On-prem identities accessing AWS |
| H05 | [Google Cloud Workload Identity Federation](https://cloud.google.com/iam/docs/workload-identity-federation) | Credential-free external workload access |
| H06 | [Microsoft Entra SPIFFE/SPIRE federation](https://learn.microsoft.com/en-us/entra/workload-id/workload-identity-federation-spiffe-spire) | Cross-cloud identity federation |
| H07 | [HashiCorp Vault Transit secrets engine](https://developer.hashicorp.com/vault/docs/secrets/transit) | Cryptographic operations without disclosing keys |
| H08 | [Kubernetes Secrets](https://kubernetes.io/docs/concepts/configuration/secret/) | Runtime secret handling and limitations |
| H09 | [NIST SP 800-190 Container Security](https://csrc.nist.gov/pubs/sp/800/190/final) | Containerized workload security |
| H10 | [OpenTelemetry specification](https://opentelemetry.io/docs/specs/otel/) | Hybrid telemetry and audit-context propagation |

**Architecture requirement:** cross-cloud identity federation must not silently extend financial permissions. Identity federation, token exchange and payment tokenization must be separate trust operations.

## Level 5 — Transaction correctness, operational safety and compliance
| ID | Reference | Focus |
|---|---|---|
| T01 | [Gray & Reuter, Transaction Processing: Concepts and Techniques](https://www.elsevier.com/books/transaction-processing-concepts-and-techniques/gray/978-1-55860-190-1) | Transactional principles; bibliographic edition should be checked |
| T02 | [Garcia-Molina & Salem, Sagas](https://doi.org/10.1145/38713.38742) | Compensating transactions; not universal undo |
| T03 | [AWS Builders' Library: Retry/Backoff/Jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/) | Failure amplification and retries |
| T04 | [Google SRE Workbook](https://sre.google/workbook/table-of-contents/) | Operational SLOs, error budgets and incidents |
| T05 | [W3C Trace Context](https://www.w3.org/TR/trace-context/) | End-to-end request correlation |
| T06 | [NIST SP 800-53](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) | Security and auditing controls |
| T07 | [EU Digital Operational Resilience Act](https://eur-lex.europa.eu/eli/reg/2022/2554/oj) | Operational risk requirements where applicable |
| T08 | [CloudEvents](https://cloudevents.io/) | Structured event envelopes, not a payment finality guarantee |

## Reading roadmap
- **Weeks 1–2:** payment tokenization, PCI boundaries, authorization/capture/settlement and idempotency.
- **Weeks 3–4:** OAuth token exchange, audience binding, DPoP/mTLS, revocation and SPIFFE identities.
- **Weeks 5–6:** MCP trust boundaries, threat modeling, policy engines and prompt-injection defense.
- **Weeks 7–8:** multi-cloud federation and credential/key lifecycle.
- **Weeks 9–10:** transaction state, ambiguous outcomes, compensation, receipts and reconciliation.
- **Weeks 11–12:** build reproducible threat tests, latency baselines and a publication-ready evidence register.

## Source quality caveats
Official standards often specify a protocol, **not** complete compliance or financial correctness. Different token classes must never be conflated. No research finding or prior-art novelty has been established by this library alone. Confirm exact specifications, URLs, revisions, and jurisdictional applicability before publication. Avoid logging financial credentials or keys.
