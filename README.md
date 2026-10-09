# Mamadou Bassirou Diallo

MSBA + AI at UT Dallas, graduating 2027. I build AI systems and the data platforms under them, end to end, and I run the evaluation that could kill my own favourite feature before I ship it. Several of the repos below changed their production default because of what that eval found.

Every project here is complete: tests, CI, a Docker image, a section on what broke while building it, and a section on what it cannot do yet.

---

## AI engineering

| Project | What it is | What actually happened |
|---|---|---|
| [**chainpilot**](https://github.com/bass990/chainpilot) | Supply-chain disruption agent: detects a stock-out or supplier delay, runs ten tool calls, has specialists argue when confidence is low, drafts RFQs and a Slack alert, and stops at a human-approval gate above a trust threshold that moves with rated outcomes. | 204-run eval. Plain direct synthesis scored 0.735 strict accuracy against 0.382 with always-on deliberation, and my conditional gate was the least stable branch (its trigger flipped on 12 of 34 scenarios). Direct synthesis is the default; the gate is a flag. |
| [**triageiq**](https://github.com/bass990/triageiq) | ER triage decision support: a symptom specialist flags red flags, a senior-nurse synthesizer assigns the ESI level, care area and action checklist. Nurse override with a required reason, print report, hash-chained audit log. | 270-run eval. A single prompt scored 100% ESI accuracy and produced no report at all on 12 of 99 attempts, all on ambiguous cases; the lean pipeline scored 98.9% and never failed to produce one. That completeness row is why lean is the default. Zero critical misses on both. |
| [**clauseguard**](https://github.com/bass990/clauseguard) | Contract-conflict agent: extracts clauses from two PDFs, finds and ranks every conflict, drafts a redline brief, and has a second model review each suggested resolution. Live tool-call feed over SSE, React UI, Docker. | 450-run eval on Sonnet 5. The agentic loop beat the single prompt by 5.4 F1 points, outside the run-to-run noise, so it became the default. Inlining the negotiation playbook into the prompt cost 14 points; exposing it as a tool was neutral. The router I had built did not earn its place and is now an opt-in cost lever. |

## Data engineering

| Project | What it is | What actually happened |
|---|---|---|
| [**sec-filings-lakehouse**](https://github.com/bass990/sec-filings-lakehouse) | Apache Iceberg lakehouse on real SEC EDGAR filings: 7.07M point-in-time financial facts (every restated version kept, "what did we know on date D" is one predicate), dbt with an enforced contract, 10-K/10-Q text chunked and embedded into pgvector as immutable index versions behind a retrieval-eval gate, FastAPI RAG with citations, Dagster. Docker Compose locally; Terraform applied and the pipeline verified on AWS, Azure and GCP. | The gate rejected two of my three embedding indexes and was right both times: one was a retrieval problem (fixed with hybrid search), one was two bugs of mine in the chunker and the eval. 17,977 restated facts in two quarters is why the point-in-time model exists. |
| [**gharchive-streaming-lakehouse**](https://github.com/bass990/gharchive-streaming-lakehouse) | Kafka (Redpanda) with Avro and a schema registry, Spark Structured Streaming writing exactly-once into Iceberg, Debezium CDC folded into an SCD2 dimension, replay and backfill, Prometheus + Grafana, and a FinOps model that prices three AWS designs. Verified on AWS, Azure and GCP. | 169,753 events landed with 169,753 distinct ids after a full-hour replay wrote zero duplicates. The first run put every event in 1970; a freshness gauge caught it, consumer lag did not. The README lists the five things that broke. |
| [**stackoverflow-causal-retention**](https://github.com/bass990/stackoverflow-causal-retention) | Causal inference on 1.77M Stack Overflow users: does a fast first answer make new contributors stay? BigQuery pipeline, 44 GB scanned for $0.22. | Four estimators agree on about +7.7 points of 30-day retention. The instrumental-variable estimate came out at -20 points, which says the exclusion restriction does not hold, and the README reports it as a failure instead of dropping it. |

## Machine learning

| Project | What it is | What actually happened |
|---|---|---|
| [**sba-loan-default-prediction**](https://github.com/bass990/sba-loan-default-prediction) | XGBoost default-risk model on 890K SBA loans, AUCPR 0.567 against an 18% base rate, with a FastAPI service, PSI drift monitoring, golden-prediction tests, and a [scoring app on Hugging Face](https://huggingface.co/spaces/bass990/SBA-Loan-Default-Prediction). | The ensemble weight search picked one model (1.0, 0.0) and the metadata says so. The cost-weighted threshold analysis found 0.35 lowers expected loss 22% versus the F1-optimal 0.66; the app now offers both. Calibration error is 0.21, and the app says that too. |
| [**NBA-Contract-Value-Analyzer**](https://github.com/bass990/NBA-Contract-Value-Analyzer) | LightGBM salary model with a leakage-safe time split, empirical 80% intervals, a staleness flag, drift monitoring, a static site, and a [Streamlit dashboard on Hugging Face](https://huggingface.co/spaces/bass990/NBA-Contract-Value-Analyzer). | The notebook's R² of 0.741 was early-stopping on the test season. The honest retrain is 0.733, and a determinism test keeps it there. Real salary data covers about 75 players because the salary sites sit behind Cloudflare; the synthetic fallback is disclosed on every page and in the API. |

---

## How I work

- I write the evaluation before I trust the feature, and I keep the report that changed my mind in the repo.
- Every README has a "what went wrong" section. The bugs were real, the fixes are in the code, and I would rather you read them there than find them in an interview.
- Local first, then cloud: each system runs on a laptop with Docker Compose, and the cloud modules are applied and verified, not just written.

## Stack

Python · SQL · Apache Iceberg · Spark Structured Streaming · Kafka / Redpanda · Debezium · dbt · Dagster · DuckDB · Terraform (AWS, Azure, GCP) · Prometheus / Grafana · FastAPI · React · Anthropic API · pgvector · XGBoost / LightGBM · scikit-learn · BigQuery · Docker · GitHub Actions

## Education

- M.S. Business Analytics and AI, The University of Texas at Dallas, 2027 (expected)
- B.S. double major in AI Engineering and Management Information Systems, Sahmyook University, Seoul. Taught in Korean.

## Languages

English · French (native) · Korean · basic Spanish

## Contact

bassiroudiallo1305@gmail.com · [LinkedIn](https://linkedin.com/in/mamadou9905)

Open to AI engineering internships and full-time roles from 2027, new-grad or early-career, with data engineering as a close second. Based in Dallas-Fort Worth, open to relocation.

