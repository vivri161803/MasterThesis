# Thesis plan and working reference

**Revision of 15 September 2026.** Supersedes `thesis_planning_document.md` and
`prof_reviews.md`, both removed in the same commit and recoverable from git
history at `57b63b3`. This file is the authoritative outline referred to by
`CLAUDE.md`.

---

## Part 0 — The supervisor's review, and what remains of it

The review of 2 September 2026 made five demands. Their current state:

| # | Demand | State |
| --- | --- | --- |
| D1 | Writing must read as one argument, not a set of paragraphs. Explicitly not a tone problem | Partly done — `\vspace` transition breaks removed throughout; chapter openings in place for Ch. 2, 3, 4 |
| D2 | Cite only peer-reviewed work; every citation must justify itself. Splitting the bibliography is *not* the remedy | Mostly done — see Part 3 |
| D3 | Expand Chapter 3: what was implemented, which technologies, which choices and why | Done — and corrected against the source, see Part 2 |
| D4 | Chapter 4 needs qualitative execution examples, more than one per component, including where the approach fails | Done — Chapter 4 written, see Part 1 |
| D5 | Proposed evaluation methodology is future work and belongs in the conclusions | Done before this revision |

## Part 1 — Document structure as it now stands

| Ch. | File | State |
| --- | --- | --- |
| 1 | `01_introduction.tex` | Final — do not edit without the author's instruction |
| 2 | `02_background.tex` | Open |
| 3 | `03_systems.tex` | Open |
| 4 | `04_examples.tex` | Worked examples — written 15 Sep 2026 |
| 5 | `05_results.tex` | Final |
| 6 | `06_conclusions.tex` | Final |
| A | `07_appendix.tex` | Final |

Chapter 4 contains: a heterogeneous source profile for Property A
(immobiliare.it 132426520, Magliana Nuova, Rome); a full extraction trace on
the repository's own `src/bulk_insert/test.txt` villa, chosen because
`ground_truth.txt` ships with it and plants two deliberate traps; a retrieval
trace; an end-to-end pass on Property B (immobiliare.it 131520968, Segrate
Village); and a failure section. Every trace is **constructed from the code**
and labelled as such in the chapter's opening section — no run was executed.

## Part 2 — Corrections applied to Chapter 3 from reading the source

Both repositories were cloned and read on 15 September 2026. Chapter 3 was
corrected, not rewritten. What changed, and why it matters:

1. **A missing stage.** After extraction there is a batched LLM-as-judge
   grounding gate returning a per-field pass/fail on whether the quote entails
   the value; failures are nulled and flagged `ungrounded`. Chapter 3 described
   only the quote validator, which checks that a quote exists. New §3.2.6,
   including `confidence = grounding pass-rate × mandatory completeness`.
2. **ε-DP does not hold as defined.** `laplace_noise` defaults sensitivity to
   10% of the value being released, not Δf over neighbouring datasets, so the
   noise scale is a function of the protected quantity and Eq. 2.11 does not
   follow. §3.3.3 now claims calibrated obfuscation and explicitly not a
   privacy proof. **This walks back a claim still made in Ch. 1 and Ch. 6.**
3. **Derivation is inert.** All 1083 fields in the shipped sidecar carry
   `derivation: null`, so `computed`/`judged` never fire. The 175 `aggregate`
   count rules are seeded separately and do fire.
4. **Topic consolidation is partial.** 64 topics over 1083 fields, with
   `superfici` holding 335 of them — the hub effect is reduced, not removed.
5. **NED's `Hierarchy` verdict is never acted on;** only `Merge` changes what
   is written, so the three-way decision is binary in practice.
6. Governance's "reject only on contradiction" is verbatim in the prompt, but
   the surrounding code is fail-closed and caches verdicts by fact hash.
7. Block 2's chunk filter (`CONTRACT_MIN_SCORE`, `CONTRACT_TOP_K`) and its
   max-similarity tie-break were absent and are now stated.
8. DIAL-KG's *dual-track extraction* is now named where Ch. 2 promises it is.
9. Two pipeline figure briefs added (`images/3/` was empty).

Verified and found **correct** as written: the 3/12/97 category tree, the
97 contract files, NED immunity, the SHA-256 product identifier.

## Part 3 — Citation state

147 distinct keys cited. Of the 28 arXiv entries that were cited before this
revision:

- **8 already render with their venue.** `bao2026dial` (DASFAA 2026),
  `chen2024m3` (Findings of ACL 2024), `gutierrez2024hipporag` (NeurIPS 2024),
  `lairgi2024itext2kg` (WISE 2024), `peeters2025entity` (EDBT 2025),
  `shrimal2025parse` (EMNLP 2025 Industry), `sun2024think` (ICLR 2024),
  `tam2024let` (EMNLP 2024 Industry). These are `@inproceedings` with a
  `booktitle`; `plainnat` ignores the vestigial `eprint` field. No action.
- **3 repointed at published versions** in `refs.bib` on 15 Sep 2026.
  **These three still need the same correction in `bib.md`, which the author
  maintains:**

  | Key | Published as |
  | --- | --- |
  | `hoffmann2022training` | Advances in Neural Information Processing Systems 35 (NeurIPS 2022) |
  | `huang2023survey` | ACM Transactions on Information Systems 43(2), 2025 — doi 10.1145/3703155 |
  | `dong2024xgrammar` | Proceedings of Machine Learning and Systems 7 (MLSys 2025) |

- **4 dropped as uncited.** `touvron2023llamab`, `grattafiori2024llama`,
  `jiang2023mistral`, `bai2023qwen` — vendor technical reports with no
  peer-reviewed version, cited only by a roll-call sentence in §2.1.3 that has
  been cut.
- **13 remain genuine preprints,** searched on 15 Sep 2026 with no published
  version found: `carta2023iterative`, `edge2024local`, `gao2023retrieval`,
  `geng2025jsonschemabench`, `gu2024survey`, `kadavath2022language`,
  `kaplan2020scaling`, `le2023large`, `peng2024graph`, `willard2023efficient`,
  `yang2025adaptive`, `zhang2025cold`, and `deepseekai2024deepseek`.
  `yang2025adaptive` is the ColdRAG paper and is load-bearing;
  `deepseekai2024deepseek` is now cited with an explicit in-text justification
  for why a vendor report is the right source for that claim.

## Part 4 — Outstanding

1. **Three `bib.md` entries are missing** and block the three `\todo{cite}`
   markers in §2.1.1: Hochreiter & Schmidhuber (1997) on LSTM, Sutskever et al.
   (2014) on sequence-to-sequence, Bahdanau et al. (2015) on additive
   attention. All peer-reviewed; the author must add them.
2. **An ASR source** for the audio front-end paragraph in §4.1 — one
   `\todo{cite}` in `04_examples.tex`.
3. **Figures.** All are `\figplaceholder` briefs awaiting artwork: four in
   Chapter 2 (`images/2/` empty), two in Chapter 3 (`images/3/` empty), and
   Chapter 4 has none yet.
4. **Chapters 1 and 6 assert the ε-DP guarantee** that Chapter 3 and §4.5 now
   qualify. Both are final chapters; reconciling them needs the author's
   decision.
5. **Deeper continuity work on the final chapters.** Removing `\vspace` was
   typographic only. Joining the resulting short paragraphs into arguments
   would edit final prose and has not been done.

## Part 5 — Standing constraints

From `CLAUDE.md`, restated because they bind hardest on Chapter 4:

- Any figure or number comes from `CLAUDE.md`, `bib.md`, or the repositories as
  read. Hyperparameters are documented defaults, never experimental results.
- `bib.md` is the author's; `tex/refs.bib` is generated from it.
- No invented citation, number, or result. Missing source → `\todo{cite}`.
- Citation keys are stable once used, even when the year no longer matches the
  published version.
- Figures go in `images/<chapter>/`; `\graphicspath` is `{../images/}`.
- Build after every set of edits; one component at a time; small diffs.

---

## Part 6 — Implementation digests

*Carried forward from the previous revision. Sourced from the `/specs` folders
of both repositories as read in July 2026, and consistent with the reference
summary in `CLAUDE.md`. These are the working reference for W3 and W2 — they
record implementation facts only. Both repositories are documented in Italian;
terminology is translated consistently and Italian phrasing does not cross
into the thesis.*

### A. `dometria-bulk-insert`

**Mission.** Stateless synchronous extraction microservice. `{id, text}` →
`{id, asset, confidence, completeness, _models}`. One container handles one
document per request; scaling is horizontal. An original async design (Celery
+ Redis + Postgres + `202 Accepted`) was deliberately dropped in favour of
pushing queueing, retries and parallelism to the deployment platform.

**Stack.** Python 3.13, `uv`. FastAPI + Uvicorn with a single **synchronous**
`def` endpoint — deliberate, so blocking Instructor/spaCy/sentence-transformers
calls run in FastAPI's threadpool rather than blocking the event loop; per
container concurrency is capped. spaCy blank pipeline + sentencizer only, for
sentence segmentation; coreference resolution folded into the Block 1 LLM call
because Python 3.13 / spaCy 3.8 had no `coreferee` support. Embeddings:
`paraphrase-multilingual-MiniLM-L12-v2` (384-dim) via sentence-transformers,
lazy-loaded through `@lru_cache`, baked into the image (~470 MB) for a
network-free cold start. LLM gateway: OpenRouter through the `openai` SDK,
structured output via `instructor` + Pydantic v2. Models: lightweight
`openai/gpt-4o-mini` (Block 1 scoring/coref, Block 2 lv1), heavy
`openai/gpt-4o` (Block 3 extraction, voting, judging). `LLM_TEMPERATURE=0.0`,
optional `LLM_SEED`. No persistence — Postgres/SQLAlchemy/Alembic dropped.
Quality gates: `pytest`, `ruff`, `mypy --strict` under `pre-commit`. Logging:
stdlib `logging`, JSON lines via `python-json-logger`. One multi-stage Docker
image with the embedding model and `contracts/` baked in; only
`OPENROUTER_API_KEY` injected at runtime.

**API.** `POST /process` → `200 {id, asset, confidence, completeness,
_models}`; `asset` carries `contract_id`, `data`, `confidence`,
`completeness`, `evidence` (per-field verbatim quote), `flags`,
`review_queue` (unfilled mandatory fields). A `200` can still require human
review — low confidence plus a non-empty `review_queue` is not an error.
`GET /health` (liveness), `GET /ready` (503 until spaCy, the embedding model
and the offline artifacts are warm). `GET /config/models`,
`POST /config/model` — ephemeral per-replica override of `MODEL_HEAVY` /
`MODEL_LIGHTWEIGHT`, gated by `RUNTIME_MODEL_OVERRIDE_ENABLED`. Errors:
`PipelineError{stage, category, message}` mapped as `bad_input`→400,
`unprocessable`→422 (no contract above `CONTRACT_MIN_SCORE`),
`retryable`→502, `server`→500; FastAPI's own validation 422 is distinct and
keeps FastAPI's envelope.

**Block 1 — preprocessing.** spaCy sentence segmentation → sliding-window
chunking with overlap → one Instructor call per chunk to the lightweight model
producing `ChunkAnalysis`: relevance score 1–10 and coreference-resolved text,
in a single combined call.

**Block 2 — contract determination.** Stage 1: constrained lightweight-LLM
call → one of 3 lv1 macro-categories. Stage 2: cosine similarity between chunk
embeddings and candidate `(lv2, lv3)` label embeddings, weighted by each
chunk's relevance score; majority vote selects the leaf. The category tree
(3 roots → 12 lv2 → 97 lv3 leaves) is a plain nested dict — the knowledge-graph
engine originally planned here was removed as over-engineered for the shape.

**Block 3 — tree-driven, evidence-grounded extraction.** Offline, the 97
contracts are unioned once into `field_tree.json` + `product_manifests.json`.
At runtime the `(lv1/lv2/lv3)` path selects the product's fields;
`pydantic.create_model` builds a per-product schema; every field gets a paired
`{name}_quote` evidence field; every closed enum gets a `NOT_PRESENT`
abstention value; a `@model_validator` rejects a populated field with no quote
and triggers an Instructor retry. Fields partition by a `topic` tag into
**sequential** extraction groups, consistent with the synchronous container
model; `priority` decides which groups get self-consistency voting
(`SELF_CONSISTENCY_N`), not execution order. Derivation: arithmetic and
cross-field values are computed in Python (`computed`), never asked of the
model; rare reasoning-derived fields (`judged`) get an isolated second pass
over primitives and quotes only, never the raw document. Field metadata lives
in an editable `field_metadata.yaml`; until compiled, `pending` enums are
treated as free text. No DAG engine by design — field selection replaces
conditional skipping, topic partitioning replaces dependency ordering.

**Post-extraction finishing (Phase 6.10).** Stage 4b normalization
(`normalize.py`, deterministic, no LLM): a type-driven registry — dates to ISO
`YYYY-MM-DD`, Italian numeric strings to `float`/`int`, text tidied; it cleans
in place, never fabricates, and keeps and flags what it cannot parse; switch
`NORMALIZE_ENABLED`. Stage 4c `OUT_OF_VOCAB` resolution (`resolve.py`, opt-in,
quote-bounded): a third enum sentinel for "present but no listed value fits",
always carrying a quote; a scoped judge remaps it to a listed value or emits
faithful free text using only the field description and that quote — never the
raw document — and produces an OOV-rate signal; switch `OOV_ENABLED`.
Count/aggregate: a `numero_X` field whose source enumerates rather than totals
gets a companion `{field}__items: list[{value, quote}]` transcription, and the
scalar becomes a code-computed count over it.

**Offline metadata compile (Phase 6.8).** `field_metadata.yaml` is seeded with
stubs by ingest and filled offline by `blocks/extraction/compile.py` /
`scripts/compile_metadata.py` — build-time, never in the request path. Batched
Instructor calls (`COMPILE_BATCH_SIZE`) produce, in Italian, a field
`description`, a proposed `topic`, and for closed-vocabulary fields a refined
enum `values` list plus an `applicable` decision; each field carries an
`unsure` self-flag. Topic names are deduplicated by exact string match into
`artifacts/topics.yaml`. CLI defaults to `--dry-run`; `--write` applies;
`--field` scopes; idempotent unless `--force`.

**Topic consolidation (Phase 6.9).** Exact-string dedup left 236 topics over
1083 fields against a target of ~30–40, because naming was batch-local and
product-coupled. The fix is an offline, no-LLM step reusing the Block 2
embedding model with **agglomerative clustering** (scikit-learn, cosine,
`average` linkage). A greedy nearest-representative pass was tried first and
rejected: the generic short name `superfici` acted as a magnet and formed a
56-member hub cluster. Representative name per cluster is the most-used member
(ties broken by shorter, then alphabetical). Knobs:
`TOPIC_CLUSTER_ENABLED` (True), `TOPIC_CLUSTER_THRESHOLD` (0.6),
`TOPIC_CLUSTER_LINKAGE` (`average`). Observed sweep: 0.55 → 50 clusters
(largest 56); 0.62 → 74 (largest 25); 0.68 → 95 (largest 17). Ids are
explicitly derived, not stable across reruns.

**Contracts.** `contracts/` holds 97 JSON files (`{id}_{lv3}.json`), one per
lv3 leaf. Field types: `text`, `integer`, `decimal`/`currency`,
`boolean`/`select`, `foreign_id`, `decimal_pair` — the last two excluded from
extraction.

**Evaluation tooling.** `scripts/eval_extraction.py` (per-field variance and
evaluation, OOV-rate signal); `scripts/measure_variance.py` (N repeated runs,
reporting schema-level agreement — does Block 2 flip contracts — against
field-level value drift); `scripts/build_artifacts.py`;
`scripts/compile_metadata.py`. No measured accuracy benchmark exists. The
`confidence: 0.82` / `completeness: 0.75` in the mission document are
explicitly illustrative, not aggregate results, and must not be presented as
measurements.

### B. ColdRAG

**Documentation.** The `info/` folder (Italian) is the authoritative
current-state documentation and explicitly replaces legacy references — the
old stack was Flask + Google-GenAI, the current one FastAPI + OpenRouter
(v3.3). Seven documents: `architettura.md`, `kg_pipeline.md`,
`motore_inferenza.md`, `conversational_completion.md`, `infrastruttura.md`,
`api_frontend.md`, `data_pipeline.md`.

**Ingestion.** Adapted from DIAL-KG. Deterministic Product node (SHA-256 of
the text) → LLM extraction of leaf entities and `product_title` → embeddings
(`BAAI/bge-m3`, 1024-dim) → coreference alignment / NED via Neo4j vector search
plus an LLM judge, with **NED immunity** so item and product nodes are never
merged into each other → governance adjudication (evidence check + logical
check, conservative: it rejects only on outright contradiction) →
transactional `MERGE` via batched `UNWIND` → Meta-Knowledge Base auto-save.

**Retrieval.** The query is analysed by an LLM into `concetti_chiave`, a
`needs_reasoning` flag and a cumulative 1024-dim embedding. A hybrid router
chooses direct vector search or multi-hop. The multi-hop loop: hop-0 frontier
of 5 nodes from the Neo4j native vector index → fan-out Cypher, one query per
hop → edge grouping (~60% prompt compression) → LLM edge scoring 0–10 →
pruning below γ → iterate to `MAX_HOPS` until enough candidates → final LLM
blind-match ranking with justified ordering. Candidates stream to the frontend
over SSE. Numeric metadata is anonymized with the Laplace mechanism (ε-DP)
before exposure.

**HITL.** `ConversationalCompletion/`: a LlamaIndex Workflows event-driven
state machine (`workflow.py`, `events.py`); a deterministic semantic router
over the `rules.yaml` taxonomy; runtime Pydantic model generation
(`models.py`, RuleParser); an LLM judge doing structured extraction and asking
targeted follow-up questions for missing mandatory fields; Redis-backed
session context, 30-minute TTL.

**Infrastructure.** Neo4j is the single source of truth — nodes, edges, vector
embeddings, singleton MKB. Redis ≥7.x for session state. `metrics.py` defines
`PerformanceTracker`: latency, estimated tokens (heuristic `len(text)//4`),
API cost (configurable $/M, defaults $0.30 in / $2.50 out), throughput and
per-item latency; `print_report()` returns `{elapsed_time,
total_tokens_estimated, cost_dollars, tps}`.

**API and frontend.** `/api/search` (multi-hop, SSE), `/api/ingest_product`,
`/ws/hitl/{session_id}`, `/api/taxonomy`, `/api/graph/overview`,
`/api/db_stats`, `/api/config`, `/api/mkb`, `/api/subgraph`,
`/api/egonet/{entity_id}`. Frontend: vanilla JS + vis-network.js SPA.

**Configuration.** `COLDRAG_TARGET_CANDIDATES=20`,
`COLDRAG_SCORE_THRESHOLD=7.0` (γ), `COLDRAG_TOP_K=5`, `COLDRAG_MAX_HOPS=5`,
`COLDRAG_HOP0_FRONTIER=5`, `COLDRAG_NED_TOP_K=10`,
`COLDRAG_NED_THRESHOLD=0.75`, `COLDRAG_DP_EPSILON=1.0`,
`COLDRAG_SESSION_TTL=1800`, `COLDRAG_SLIDING_WINDOW=4`. **Documented
defaults, not measured settings.**

**Stack.** OpenRouter (OpenAI-compatible) + `instructor` in JSON mode with
multi-model fallback (default `deepseek/deepseek-chat`); `BAAI/bge-m3`
embeddings; Neo4j ≥5.x with the native vector index (`entity_embeddings`);
FastAPI + Uvicorn (WebSocket + SSE); Redis ≥7.x; `uv`; Python ≥3.13; native
`asyncio`.

**Testing.** Pytest: `test_models.py` (RuleParser, FinalPayload, product-ID
generation), `test_workflow.py` (events, session TTL, workflow steps).

**Theory.** `specs/Teoria/` holds the source PDFs for both foundational
papers: ColdRAG (Yang et al.) and DIAL-KG (Bao et al.). Both are cited
distinctly in Chapter 2, and Dometria's ColdRAG is flagged as an
implementation adaptation, not the paper authors' original code.

**Confirmed absence of benchmarks.** As with bulk-insert, no Recall/NDCG/HR or
other recommendation-quality metric appears in `specs/` or `info/`. The only
numeric figures are configuration defaults and one illustrative infrastructure
sample (17.50 s, 5 items, ~1200 tokens, $0.00102, 68.57 TPS, 3.50 s/item) —
illustrative, and to be labelled as such wherever it appears.
