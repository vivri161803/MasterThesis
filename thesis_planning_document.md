# Thesis Planning Document

**Revision of 2 September 2026.** Supersedes the previous planning document in
full. It is rewritten around the supervisor's review of the same date
(`prof_reviews.md`), which asks for changes to the draft rather than to the
plan: the chapter structure below is the previous one, corrected where the
review requires it.

Part 6 carries the implementation digests forward from the previous revision
unchanged in substance. They are the only written record of the
`dometria-bulk-insert` internals — `CLAUDE.md` documents ColdRAG alone — and
Chapter 3 cannot be expanded without them.

---

## Part 0 — Where the draft actually stands

| Ch. | File | Lines | State |
| --- | --- | --- | --- |
| 1 | `01_introduction.tex` | 128 | Drafted, restructured into shorter paragraphs, 5 figures |
| 2 | `02_background.tex` | 348 | Drafted, 10 sections + summary — the heaviest chapter |
| 3 | `03_systems.tex` | 152 | **Drafted thin.** Three sections; less than half of Chapter 2 |
| 4 | `04_results.tex` | 69 | **Written but not compiled** — no `\input` in `main.tex` |
| 5 | `05_conclusions.tex` | 321 | Drafted, 4 figures. Opens with a 186-line *Results and evaluation* section |
| A | `06_appendix.tex` | 81 | Drafted — AI use in preparing the thesis |

Two consequences to fix before anything else:

1. The results material lives in **two** places — a standalone chapter file
   that never compiles, and a section inside the conclusions.
2. Because `04_results` is not included, the compiled PDF numbers
   *Conclusions* as **Chapter 4**. The supervisor's "Capitolo 4" means the
   results chapter, not what currently prints under that number.

Bibliography: 292 entries in `refs.bib`, 148 cited. **28 cited entries are
arXiv preprints**; 8 of those already name a peer-reviewed venue in the entry
(DASFAA, ACL Findings, NeurIPS, WISE, EDBT, EMNLP ×2, ICLR) and roughly 20
carry no venue at all.

---

## Part 1 — The supervisor's review, 2 September 2026

Verbatim from `prof_reviews.md`, with what each point requires.

> *"la scrittura deve essere più omogenea: ora sembra un insieme di paragrafi,
> senza un filo conduttore"* — and, separately, *"cercare di rendere i concetti
> più omogenei tra loro (non è un problema del tono)"*

**D1 — Continuity.** The writing reads as a set of paragraphs with no thread
running through them. Explicitly *not* a tone problem: the register is fine,
the connective tissue between concepts is missing.

> *"occhio alle citazioni: a volte non è chiaro perchè citi alcuni articoli, ed
> alcuni articoli non sono mai stati pubblicati [...] evitare di [citare] i
> paper su arxiv, dato che non hanno subito un processo di peer review"* — and
> *"più che dividere la bibliografia, devi cercare di usare solo articoli
> pubblicati. Spesso quelli di arxiv hanno una versione pubblicata."*

**D2 — Citations.** Two distinct faults. Each citation must make its reason
for being there evident; and the bibliography must rest on peer-reviewed work.
Splitting the bibliography into sections is explicitly *not* the remedy —
finding the published version is.

> *"il Capitolo 3 deve essere un po' più espanso: entra nei dettagli di cosa
> hai implementato, che tecnologie/librerie hai utilizzato, che scelte
> implementative hai fatto"*

**D3 — Chapter 3.** Expand: what was implemented, which technologies and
libraries, which implementation choices were made and why.

> *"il Capitolo 4 è un po' debole: capisco che non ci sia un benchmark, e che
> non era obiettivo di tesi, ma almeno degli esempi qualitativi di esecuzione
> vanno messi (anche mostrando i limiti di quello che hai realizzato)"* — and
> *"io metterei degli esempi di esecuzione. Ad esempio, un'estrazione di
> feature dal testo, un matching, etc.. puoi anche mettere più esempi per
> componente sviluppato, magari facendo vedere anche i limiti dell'approccio"*

**D4 — Chapter 4.** The absence of a benchmark is accepted and is not held
against the thesis. What is missing is qualitative execution examples — a
feature extraction from a real text, a matching run — more than one per
component, and deliberately including examples that show where the approach
fails.

> *"sul capitolo 4, più che un'idea su come testare (quello è un future work da
> mettere nelle conclusioni)"*

**D5 — Placement.** A proposed evaluation methodology is future work and
belongs in the conclusions. Chapter 4 shows what the systems did, not what one
could someday measure.

---

## Part 2 — Work plan

Ordered by dependency. Each item states what "done" means.

### W1 — Restore Chapter 4 as a chapter *(prerequisite for D4, D5)*

Move the *Results and evaluation* section out of `05_conclusions.tex` into
`04_results.tex`, merge it with what that file already holds, and add
`\input{04_results}` to `main.tex` between `03_systems` and `05_conclusions`.
The prospective-benchmark passage now closing that section moves to
§5.4 Future work per D5.

*Done when:* the PDF has five numbered chapters, the conclusions no longer
report results, and no `\ref` is left dangling.

### W2 — Qualitative execution examples *(D4)*

The substance of the revision. Two or more worked examples per component,
each showing a real input, the actual output, and a reading of what it
demonstrates:

| Component | Example to show |
| --- | --- |
| bulk-insert — Block 2 | one document → contract classification, with the lv1 call and the weighted cosine vote that picks the lv3 leaf |
| bulk-insert — Block 3 | one document → extracted fields with their verbatim evidence quotes; one case where a mandatory field lands in `review_queue` |
| bulk-insert — normalization | an Italian date and numeric string before and after Stage 4b; an `OUT_OF_VOCAB` resolution |
| ColdRAG — ingestion | one product document → extracted entities, an NED merge that fired, and a governance rejection |
| ColdRAG — retrieval | one query → hop-0 frontier, an edge kept and an edge pruned at γ, the final ranking with its justification |
| ColdRAG — HITL | one conversation → the missing mandatory field, the follow-up question, the final payload |
| **Limits** | at least one example per system where the output is wrong or unusable, with a reading of why |

Every figure in these examples must come from a run whose output is on hand.
Where a number is not, `\todo{}` it and ask — a default from `CLAUDE.md` is
not an experimental result (see Part 4).

### W3 — Expand Chapter 3 *(D3)*

Chapter 3 is 152 lines against Chapter 2's 348. Target: the implementation
detail in the Part 6 digests, written out — not a re-listing of the stack, but
the choices and their reasons. The decisions worth a paragraph each:

- the synchronous FastAPI endpoint, and why the async Celery/Redis/Postgres
  design was dropped;
- the knowledge-graph engine removed from Block 2 as over-engineered for a
  three-level, 97-leaf tree;
- runtime Pydantic model generation from a field tree unioned offline;
- the paired evidence quote per field, the `NOT_PRESENT` abstention, and the
  validator that forces an Instructor retry;
- transcribe-then-derive: arithmetic in Python, never asked of the model;
- agglomerative clustering over greedy nearest-representative for topic
  consolidation, and the `superfici` hub effect that decided it;
- ColdRAG: NED immunity, conservative governance, edge grouping as prompt
  compression, γ pruning, ε-DP before exposure.

*Done when:* a reader can reconstruct what was built and why each choice was
made, without opening either repository.

### W4 — Citations *(D2)*

Two passes, in order:

1. **Published versions.** Work through the 28 cited arXiv entries. Where a
   peer-reviewed version exists, the entry must cite it. The 8 that already
   name a venue need the entry fixed so the printed reference shows the venue
   rather than the preprint. I will produce the list with the published
   reference for each, for you to fold into `bib.md` — I do not edit `bib.md`.
2. **Genuine preprints.** What remains is mostly model reports (Llama, Qwen,
   DeepSeek, Mistral) and scaling-law papers with no peer-reviewed version.
   For each: drop the citation, or keep it and say in the text why a technical
   report is the right source for that claim.
3. **Purpose.** For every remaining citation, the sentence must make clear
   what the reference is doing there. A citation that cannot be justified in
   its own sentence comes out.

### W5 — Continuity pass *(D1)*

Last, once the content is settled. Per chapter: an opening that states what
the chapter establishes and how it follows from the previous one; explicit
links where a concept returns; and removal of the paragraph-level isolation —
including the `\vspace{0.3cm}` breaks now standing in for transitions in
Chapters 1 and 5, which visually reinforce exactly the fragmentation the
review names.

*Done when:* each chapter reads as an argument, and the through-line from
document → structured asset → match is visible without being asserted.

---

## Part 3 — Revised table of contents

Changes against the previous revision are marked **[new]** or **[changed]**.

### Chapter 1 — Introduction
1.1 Application context · 1.2 The two problems addressed · 1.3 Objectives and
contributions · 1.4 Dometria AI · 1.5 Structure of the thesis

### Chapter 2 — Background and State of the Art
2.1 Foundations of ML and LLMs · 2.2 Retrieval augmentation and GraphRAG ·
2.3 The cold-start problem · 2.4 Knowledge graph construction · 2.5
Self-consistency and validation via LLMs · 2.6 Vector search and embeddings ·
2.7 Human-in-the-loop data acquisition · 2.8 Differential privacy · 2.9 Domain
context: valuation and the off-market sector · 2.10 Summary

Structurally complete. W4 and W5 apply here more than anywhere else — this is
where the citations are.

### Chapter 3 — Systems Developed **[changed — expanded per D3]**

3.1 Common overview — shared stack; the transcribe-then-derive principle

3.2 Part A — `dometria-bulk-insert`
: 3.2.1 Service contract and the synchronous architecture **[new: the pivot away from the async design]**
: 3.2.2 Block 1 — preprocessing: segmentation, chunking, combined relevance + coreference call
: 3.2.3 Block 2 — contract determination: constrained lv1 classification, weighted cosine vote over (lv2, lv3) **[new: why the KG engine was removed]**
: 3.2.4 Block 3 — tree-driven, evidence-grounded extraction **[new: runtime schema generation, the quote validator, topic partitioning, self-consistency]**
: 3.2.5 Post-extraction finishing: normalization, `OUT_OF_VOCAB` resolution, count/aggregate **[new]**
: 3.2.6 Offline metadata compilation **[new]**
: 3.2.7 Topic consolidation: agglomerative clustering and the hub effect **[new]**
: 3.2.8 Error model and hardening **[new]**
: 3.2.9 Containerization

3.3 Part B — ColdRAG
: 3.3.1 The three modules
: 3.3.2 Ingestion — the adapted DIAL-KG pipeline **[new: NED immunity, governance adjudication]**
: 3.3.3 Inference engine — hybrid routing, the multi-hop loop, γ pruning, blind-match ranking **[new: edge grouping as prompt compression]**
: 3.3.4 Privacy layer — ε-DP over exposed metadata
: 3.3.5 HITL conversational completion — workflow, semantic router, runtime Pydantic generation
: 3.3.6 Stack and configuration
: 3.3.7 Exposed API

### Chapter 4 — Results and Evaluation **[changed — restored as a chapter, rebuilt per D4/D5]**

4.1 Methodological premise: no benchmark, and what is reported instead
4.2 `dometria-bulk-insert` in execution **[new]** — worked examples per W2,
    then the evaluation tooling and quality gates
4.3 ColdRAG in execution **[new]** — worked examples per W2, then
    `PerformanceTracker` and the test suite
4.4 Where the approaches fail **[new]** — the negative examples, read honestly
4.5 What this evaluation establishes, and what it does not

The prospective-benchmark discussion is **removed** from this chapter; it
belongs to §5.4.

### Chapter 5 — Conclusions **[changed]**
5.1 Objectives and how they were met · 5.2 Cross-project synthesis: the two
halves of the Dometria data pipeline · 5.3 Limitations · 5.4 Future work —
**now including the evaluation methodology** moved out of Chapter 4 per D5:
reference sets, annotation protocol, Recall@k/NDCG for ColdRAG, field-level
accuracy for bulk-insert

### Appendix A — Use of AI in the preparation of this thesis
Unchanged.

---

## Part 4 — Constraints that do not change

From `CLAUDE.md`, restated because W2 is where they bite hardest:

- Any figure or number in the thesis comes from `CLAUDE.md` or `bib.md`. The
  hyperparameter defaults are **documented defaults, not measured results** —
  a default may never be presented as an experimental setting. If a worked
  example needs the value actually used in a run, ask.
- `bib.md` is the source of truth for what may be cited and is maintained by
  the author, not by me. I own `tex/refs.bib` and generate it from `bib.md`.
- No invented citation, number, or result. Missing source → `\todo{cite}`.
- Citation keys are stable once used; never rename a key already in the text.
- Figures go in `images/<chapter>/`; `\graphicspath` is `{../images/}`, so a
  path in the text is `3/name.png`.
- One component at a time, small reviewable diffs, build after every set of
  edits.

---

## Part 5 — Order of work

| # | Work | Why here |
| --- | --- | --- |
| 1 | **W1** restore Chapter 4 | Everything else in Chapters 4–5 depends on the split being right |
| 2 | **W3** expand Chapter 3 | W2's examples reference the components Chapter 3 describes |
| 3 | **W2** execution examples | The heaviest item; needs real run outputs, so start collecting them now |
| 4 | **W4** citations | Independent of the above; can proceed in parallel when blocked on run data |
| 5 | **W5** continuity pass | Last — it operates on settled text |

Send each chapter to the supervisor as it is finished, per his standing
request. I will draft the email when a chapter is ready; nothing is sent
without confirmation.

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
