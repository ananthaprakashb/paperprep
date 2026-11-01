# Autonomous Reliability — Source-Linked Knowledge Base

Updated 2026-11-01. Source types: **Official** = standards or maintainer documentation; **Engineering** = practitioner literature; **Research** = published research; **Tool** = maintained implementations or datasets. This is a curated starting collection, not an exhaustive systematic literature review.

## 1. SRE and error budget fundamentals

| ID | Authentic source | Type | Application |
|---|---|---|---|
| S01 | [Google SRE Book](https://sre.google/sre-book/table-of-contents/) | Engineering | Monitoring, risk, overload, cascading failures |
| S02 | [Google SRE Workbook](https://sre.google/workbook/table-of-contents/) | Engineering | Practical SLO and incident operations |
| S03 | [Implementing SLOs](https://sre.google/workbook/implementing-slos/) | Engineering | Good-event, total-event definitions; budgets |
| S04 | [Alerting on SLOs](https://sre.google/workbook/alerting-on-slos/) | Engineering | **Mandatory baseline:** multi-window multi-burn alerts |
| S05 | [Error Budget Policy](https://sre.google/workbook/error-budget-policy/) | Engineering | Change restrictions and accountability |
| S06 | [Service Best Practices](https://sre.google/sre-book/service-best-practices/) | Engineering | Reliability targets and tradeoffs |

Start with S03-S05. Distinguish user-facing business SLIs from request-level and infrastructure health. Avoid claiming new SLO frameworks merely because a risk score is forecast.

## 2. Instrumentation, event semantics and measurement

| ID | Source | Type | Application |
|---|---|---|---|
| O01 | [OpenTelemetry core specification](https://opentelemetry.io/docs/specs/otel/) | Official | Traces, metrics, logs and context |
| O02 | [OpenTelemetry semantic conventions](https://opentelemetry.io/docs/specs/semconv/) | Official | Consistent cross-service signals |
| O03 | [HTTP semantic conventions](https://opentelemetry.io/docs/specs/semconv/http/) | Official | Transport metrics; separate from payment success |
| O04 | [Messaging semantic conventions](https://opentelemetry.io/docs/specs/semconv/messaging/) | Official | Queue/consumer delay |
| O05 | [Prometheus metric data model](https://prometheus.io/docs/concepts/data_model/) | Official | Counters, gauges and cardinality |
| O06 | [Prometheus histograms and summaries](https://prometheus.io/docs/practices/histograms/) | Official | Tail-latency measurement and quantile pitfalls |
| O07 | [Prometheus recording rules](https://prometheus.io/docs/prometheus/latest/configuration/recording_rules/) | Official | Efficient SLI aggregation |
| O08 | [Prometheus alerting rules](https://prometheus.io/docs/prometheus/latest/configuration/alerting_rules/) | Official | Alert baseline |
| O09 | [W3C Trace Context](https://www.w3.org/TR/trace-context/) | Official | Distributed trace propagation |

**Proposed payment-domain instrumentation:** qualified user-intended operation, processor decision, timeout-unknown, idempotency outcome, settlement completion, ledger reconciliation delay and reversal. Document denominators and windows; remove PAN, credentials and sensitive payloads. Never equate HTTP 200 with financially correct completion.

## 3. Cloud-native controllers, overload and resilience

| ID | Source | Type | Application |
|---|---|---|---|
| C01 | [Kubernetes Autoscaling](https://kubernetes.io/docs/concepts/workloads/autoscaling/) | Official | HPA/VPA scaling limits |
| C02 | [HorizontalPodAutoscaler walkthrough](https://kubernetes.io/docs/tasks/run-application/horizontal-pod-autoscale-walkthrough/) | Official | Control baseline |
| C03 | [Kubernetes liveness/readiness/startup probes](https://kubernetes.io/docs/concepts/configuration/liveness-readiness-startup-probes/) | Official | Health probes, avoiding harmful restarts |
| C04 | [Pod disruption budgets](https://kubernetes.io/docs/tasks/run-application/configure-pdb/) | Official | Change safety |
| C05 | [Argo Rollouts](https://argo-rollouts.readthedocs.io/en/stable/) | Tool | Progressive rollout and rollback |
| C06 | [Istio traffic management](https://istio.io/latest/docs/concepts/traffic-management/) | Tool | Routing and traffic control |
| C07 | [AWS Builders' Library: Timeouts, retries and jitter](https://aws.amazon.com/builders-library/timeouts-retries-and-backoff-with-jitter/) | Engineering | Retry amplification and backoff |
| C08 | [AWS Builders' Library: Load shedding](https://aws.amazon.com/builders-library/using-load-shedding-to-avoid-overload/) | Engineering | Controlled overload responses |
| C09 | [Chaos Mesh](https://chaos-mesh.org/docs/) | Tool | Fault injection |
| C10 | [LitmusChaos](https://docs.litmuschaos.io/) | Tool | Controlled chaos experiments |

## 4. Prediction, statistical evidence and benchmark datasets

| ID | Source | Type | Research role |
|---|---|---|---|
| R01 | [Forecasting: Principles and Practice](https://otexts.com/fpp3/) | Engineering | Time series, seasonality and rolling forecast validation |
| R02 | [NIST Engineering Statistics Handbook](https://www.itl.nist.gov/div898/handbook/) | Official | Statistical evaluation and calibration |
| R03 | [Google cluster data](https://github.com/google/cluster-data) | Dataset | Workload dynamics, not payment outcomes |
| R04 | [Alibaba clusterdata](https://github.com/alibaba/clusterdata) | Dataset | Capacity and workload traces |
| R05 | [PRESAGE: Uncertainty-Aware Predictive Elastic Scheduling](https://doi.org/10.1109/ACCESS.2026.3734498) | Research | 2026 related uncertainty-aware scheduling; verify paper methods and applicability |
| R06 | [Google TimesFM](https://github.com/google-research/timesfm) | Tool | Time-series model comparator |
| R07 | [Amazon Chronos](https://github.com/amazon-science/chronos-forecasting) | Tool | Probabilistic forecast comparator |
| R08 | [Darts](https://unit8co.github.io/darts/) | Tool | Time-forward backtesting |
| R09 | [PyOD](https://pyod.readthedocs.io/en/latest/) | Tool | Anomaly detection comparators |
| R10 | [NetMan AIOps research repositories](https://github.com/NetManAIOps) | Dataset | Discover datasets and RCA benchmarks, check specific licensing |

Train/validate/test chronologically. Compare seasonal naive, exponentially weighted trends, SLO burn rates, and calibrated forecasting before complex neural models. Measure false action rates, not prediction accuracy alone.

## 5. Financial-sector operational risk and audit governance

| ID | Source | Type | Relevance |
|---|---|---|---|
| F01 | [BIS CPMI-IOSCO Principles for Financial Market Infrastructures](https://www.bis.org/committees/cpmi/pfmi/overview) | Official | Operational risk, capacity and recovery; applicability depends on institution/system |
| F02 | [PCI Security Standards Council document library](https://www.pcisecuritystandards.org/document_library/) | Official | Payment data security, scope-dependent |
| F03 | [NIST SP 800-53](https://csrc.nist.gov/pubs/sp/800/53/r5/upd1/final) | Official | Access, operations, control evidence |
| F04 | [NIST SP 800-61 Rev.3](https://csrc.nist.gov/pubs/sp/800/61/r3/final) | Official | Incident response |
| F05 | [NIST AI Risk Management Framework](https://www.nist.gov/itl/ai-risk-management-framework) | Official | ML risk governance |
| F06 | [EU Digital Operational Resilience Act](https://eur-lex.europa.eu/eli/reg/2022/2554/oj) | Official | ICT resilience where applicable |
| F07 | [ISO 20022](https://www.iso20022.org/) | Official | Payment semantics, not an SLO methodology |

## 6. Research gaps to investigate, not presupposed discoveries

1. Burn-rate alerts capture historical consumption; forecasted exhaustion might improve usable warning lead time, **if sufficiently calibrated**.
2. Transaction-state-aware SLIs may capture customer harm absent from generic HTTP availability.
3. Automated scaling, rollback and routing can create oscillation or cascading failures; safety envelopes need independent evaluation.
4. Forecasting during demand spikes, processor incidents, sparse data and telemetry loss can be uncertain. Abstention is a first-class behavior.
5. An auditable, deterministic action gate can separate recommendation from execution.

## Citation hygiene

Record author, year, title, version/date, publisher, stable URL/DOI and exact supported claim; recheck source validity prior to manuscript submission. Do not describe new hypotheses as proven research outcomes. Benchmark data from public cloud traces does **not** provide real payment correctness ground truth.
