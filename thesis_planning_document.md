# Thesis Planning Document
### Working title, revised index, condensed spec digests, and writing roadmap

---

## Part 0 — Working title

**Proposed title:**

> **"From Documents to Matches: Evidence-Grounded Extraction and GraphRAG Cold-Start Recommendation for Real-Estate Off-Market Intermediation"**

*(Sottotitolo italiano, se richiesto: "Estrazione evidence-grounded e raccomandazione cold-start basata su GraphRAG per l'intermediazione immobiliare off-market")*

Alternative, shorter option:

> **"Structuring the Unstructured: Two LLM-Based R&D Systems for Real-Estate Asset Extraction and Cold-Start Matching at Dometria AI"**

The title foregrounds the two systems as a single pipeline ("supply" of structured assets → "demand"-side matching), which is the unifying thread the professor's feedback also points toward (shared background, shared methodological philosophy).

---

## Part 1 — Revised Table of Contents (Indice)

Revisions applied per professor's feedback:
1. **Cap. 2**: added a dedicated ML/LLM foundations section *before* RAG/GraphRAG, since RAG is presented as a technique built on top of LLMs, not an independent starting point.
2. **Cap. 3**: stripped of anything "explanatory"/background in nature (problem statement, theoretical framing, paper citations). Chapter 3 is now strictly *what was built*: models used, how they were combined/orchestrated, pre-processing choices, libraries, configuration. Everything needed to *understand* Chapter 3 was moved up into Chapter 2.
3. Kept the "Part A / Part B" split (bulk-insert / ColdRAG) inside Chapter 3, since the two systems remain distinct engineering contributions even though they share one background chapter.
4. Suggested writing order noted per section (Cap. 2/3 first, then 4, then 1/5 last).

---

### Capitolo 1 — Introduzione
*(scritto per ultimo)*

1.1 Contesto applicativo: frammentazione, opacità e onerosità del processo di valutazione e incontro domanda/offerta nel settore immobiliare, specialmente off-market
1.2 Dometria AI: origine dal progetto REAL (Scuola Superiore Sant'Anna, Pisa), il "doppio core tecnologico" Value + Connect
1.3 I due problemi affrontati dalla tesi:
   - trasformare documenti eterogenei in asset strutturati e confrontabili (bulk-insert)
   - raccomandare/abbinare item nuovi o a bassa interazione storica (ColdRAG, cold-start)
1.4 Obiettivi della tesi e contributi
1.5 Struttura della tesi

---

### Capitolo 2 — Background e Stato dell'Arte
*(da scrivere per primo — contiene tutto ciò che serve per capire il Capitolo 3)*

**2.1 Fondamenti di Machine Learning e Large Language Models** *(nuova sezione, richiesta dal relatore, prima del RAG)*
   - 2.1.1 Dai modelli statistici classici ai modelli neurali linguistici: cenni essenziali
   - 2.1.2 Architettura Transformer e modelli autoregressivi (cenni)
   - 2.1.3 LLM general-purpose vs instruction-tuned; prompting, few-shot, zero-shot
   - 2.1.4 Structured/constrained output da un LLM: perché serve, function calling, JSON schema, librerie come Instructor + Pydantic (concetti generali; l'uso concreto va in Cap. 3)
   - 2.1.5 Limiti noti degli LLM rilevanti per la tesi: allucinazione, non-determinismo, variance run-to-run, necessità di grounding

**2.2 Retrieval-Augmented Generation e GraphRAG**
   - 2.2.1 RAG: motivazione, architettura base, limiti (retrieval flat, mancanza di struttura relazionale)
   - 2.2.2 GraphRAG (Microsoft Research): knowledge graph generati da LLM, community detection (Leiden), retrieval graph-guided, ragionamento "globale" multi-hop, provenance/grounding

**2.3 Il problema del cold-start nei sistemi di raccomandazione**
   - 2.3.1 Collaborative filtering, content-based, ibridi
   - 2.3.2 Cold-start di item vs utente
   - 2.3.3 Raccomandatori LLM zero-shot (PromptRec, TaxRec, KALM4Rec)
   - 2.3.4 Il paper ColdRAG (Yang et al., arXiv 2505.20773): framework di retrieval-augmented con costruzione dinamica del KG e ragionamento multi-hop guidato da LLM; posizionamento rispetto al lavoro di tesi (adattamento implementativo per il dominio Dometria, non il codice originale)

**2.4 Costruzione di Knowledge Graph**
   - 2.4.1 Approcci rule-based, supervisionati, LLM-based
   - 2.4.2 Knowledge Graph Construction schema-free/incrementale
   - 2.4.3 Il framework DIAL-KG (Bao et al.): Meta-Knowledge Base, dual-track extraction, ciclo di adattamento incrementale
   - 2.4.4 Named Entity Disambiguation, coreference resolution, entity linking

**2.5 Auto-consistenza e validazione tramite LLM**
   - 2.5.1 Self-consistency / majority voting: Wang et al., "Self-Consistency Improves Chain of Thought Reasoning in Language Models," ICLR 2023 — risultati riportati (GSM8K +17.9%, SVAMP +11.0%, AQuA +12.2%, StrategyQA +6.4%, ARC-challenge +3.9%)
   - 2.5.2 LLM-as-judge ed entailment gating come meccanismo di verifica di grounding

**2.6 Ricerca vettoriale ed embedding**
   - 2.6.1 Modelli di embedding (bge-m3, MiniLM) e similarità coseno
   - 2.6.2 Indici vettoriali nativi e ANN (Neo4j vector index, HNSW/Lucene)

**2.7 Acquisizione dati Human-in-the-Loop**
   - 2.7.1 Validazione strutturata, gate di approvazione, routing basato su confidenza
   - 2.7.2 LlamaIndex Workflows: orchestrazione event-driven, step tipizzati, eventi Pydantic, Context persistente

**2.8 Privacy differenziale**
   - 2.8.1 Definizione di ε-differential privacy, meccanismo di Laplace, sensitivity, privacy budget

**2.9 Contesto di dominio: valutazione immobiliare e mercato off-market**
   - 2.9.1 Standard di valutazione (RICS/IVS/EVS)
   - 2.9.2 Matching "blind"/confidenziale, deal-flow riservato, VDR e NDA

---

### Capitolo 3 — Sistemi Sviluppati
*(strettamente: cosa è stato implementato — niente definizioni teoriche, niente problem statement esteso; solo riferimenti puntuali al Cap. 2 dove serve)*

**3.1 Panoramica comune**
   - 3.1.1 Stack condiviso: Python 3.13, `uv`, OpenRouter come gateway LLM-agnostico, Instructor + Pydantic per output strutturato, FastAPI
   - 3.1.2 Principio metodologico condiviso: "transcribe-then-derive" / evidence-grounded (quote verbatim, derivazione lato codice, gating LLM-as-judge)

**3.2 Parte A — dometria-bulk-insert**
   - 3.2.1 Interfaccia e contratto di servizio: endpoint `POST /process` sincrono, stateless, scaling orizzontale; endpoint di health/readiness; motivazione dell'architettura sincrona (thread pool FastAPI) rispetto al design originario async (Celery/Redis/Postgres, pivot del 2026-06-25)
   - 3.2.2 Blocco 1 — Preprocessing: segmentazione spaCy (sentencizer, nessun modello scaricato), chunking con overlap, singola chiamata LLM lightweight (`gpt-4o-mini`) per relevance scoring + risoluzione coreference
   - 3.2.3 Blocco 2 — Contract Determination: classificazione lv1 vincolata via LLM lightweight; selezione (lv2, lv3) tramite similarità coseno pesata (embedding `paraphrase-multilingual-MiniLM-L12-v2`, 384-dim) e voto di maggioranza; albero delle categorie a 3 livelli (3 radici, 12 nodi lv2, 97 foglie lv3) attraversato per lookup — nota di design: la knowledge graph originariamente prevista è stata rimossa in quanto over-engineered
   - 3.2.4 Blocco 3 — Asset Extraction (tree-driven, evidence-grounded):
       - field tree statico costruito offline dall'unione dei 97 contratti; generazione di un modello Pydantic per-prodotto a runtime (`pydantic.create_model`)
       - ogni campo abbinato a una quota di evidenza verbatim; ogni vocabolario chiuso include l'opzione di astensione `NOT_PRESENT`; validatore che rifiuta campi non nulli privi di quota (retry Instructor)
       - partizionamento dei campi per `topic`, estrazione sequenziale; self-consistency voting sui gruppi mandatory/high-priority
       - derivazione: valori aritmetici/incrociati calcolati in codice, mai richiesti al modello; casi di reasoning isolato eseguiti in una seconda chiamata LLM solo su primitive + quote
   - 3.2.5 Rifinitura post-estrazione (Fase 6.10): normalizzazione deterministica (date → ISO, numeri italiani → float/int, pulizia testo); risoluzione `OUT_OF_VOCAB` opzionale (LLM vincolato alla quota, segnale di OOV-rate); meccanismo count/aggregate (trascrivi-poi-deriva applicato al livello di singolo campo)
   - 3.2.6 Compilazione offline dei metadati (Fase 6.8): generazione di descrizioni, topic e vocabolari enum in italiano via chiamate Instructor batch; flag `unsure`; CLI dry-run/--write
   - 3.2.7 Consolidamento dei topic (Fase 6.9): clustering agglomerativo (coseno, linkage medio) sui nomi di topic proposti dal modello per ridurre la frammentazione (236 → ~50–95 cluster a seconda della soglia); motivazione della scelta agglomerativa rispetto a un approccio greedy (effetto "hub")
   - 3.2.8 Gestione errori e hardening: `PipelineError` con categorie (`bad_input`, `unprocessable`, `retryable`, `server`) mappate a codici HTTP; autenticazione API-key, guardie sul payload, backoff con `Retry-After`, graceful shutdown, logging strutturato JSON
   - 3.2.9 Containerizzazione: immagine Docker unica (~2.5 GB, CPU-only), modello di embedding e contratti incorporati nell'immagine

**3.3 Parte B — ColdRAG**
   - 3.3.1 Panoramica dei tre moduli: ingestion (KG construction), motore di inferenza (retrieval), completamento conversazionale (HITL)
   - 3.3.2 Ingestion — pipeline DIAL-KG adattata (`kg_builder.py`, `ingest.py`): creazione deterministica del nodo Product (SHA-256), estrazione LLM di entità foglia + titolo prodotto, generazione embedding (`BAAI/bge-m3`, 1024-dim), allineamento di coreference/NED (ricerca vettoriale Neo4j + LLM Judge, con "NED immunity" per i nodi prodotto), adjudication di governance (evidence check + logical check, conservativa), MERGE transazionale via batch UNWIND, auto-save della Meta-Knowledge Base
   - 3.3.3 Motore di inferenza (`coldrag_engine.py`): analisi della query in `concetti_chiave` + flag `needs_reasoning` + embedding cumulativo; Hybrid Router (ricerca vettoriale diretta vs multi-hop); loop multi-hop (frontiera hop-0, fan-out Cypher, edge grouping, scoring LLM 0–10, pruning a soglia γ, iterazione fino a `MAX_HOPS`); ranking finale "blind match"; streaming progressivo via SSE
   - 3.3.4 Livello di privacy: anonimizzazione dei metadati numerici con meccanismo di Laplace (ε-differential privacy) prima dell'esposizione
   - 3.3.5 Completamento conversazionale HITL (`ConversationalCompletion/`): state machine event-driven basata su LlamaIndex Workflows (`workflow.py`, `events.py`); router semantico deterministico su tassonomia (`rules.yaml`); generazione dinamica di modelli Pydantic a runtime (`models.py`, RuleParser); LLM Judge per estrazione strutturata e domande di follow-up sui campi mandatory mancanti; contesto di sessione su Redis (TTL 30 min)
   - 3.3.6 Stack tecnico e configurazione: OpenRouter + Instructor (fallback multi-modello, default `deepseek/deepseek-chat`); Neo4j ≥5.x con indice vettoriale nativo; FastAPI + Uvicorn (WebSocket per HITL, SSE per la ricerca); Redis ≥7.x; frontend SPA vanilla JS + vis-network.js; iperparametri principali (`COLDRAG_TARGET_CANDIDATES`, `COLDRAG_SCORE_THRESHOLD`, `COLDRAG_TOP_K`, `COLDRAG_MAX_HOPS`, `COLDRAG_HOP0_FRONTIER`, `COLDRAG_NED_TOP_K`, `COLDRAG_NED_THRESHOLD`, `COLDRAG_DP_EPSILON`, `COLDRAG_SESSION_TTL`)
   - 3.3.7 API esposte: `/api/search`, `/api/ingest_product`, `/ws/hitl/{session_id}`, `/api/taxonomy`, `/api/graph/overview`, `/api/db_stats`, `/api/config`, `/api/mkb`, `/api/subgraph`, `/api/egonet/{entity_id}`

---

### Capitolo 4 — Risultati e Valutazione

4.1 Premessa metodologica: nessuno dei due repository pubblica benchmark quantitativi di accuratezza; il capitolo si concentra su validazione architetturale, comportamento osservato e strumenti di valutazione realizzati
4.2 dometria-bulk-insert:
   - strumenti di valutazione (`scripts/eval_extraction.py`, `scripts/measure_variance.py`) e cosa misurano (variance a livello di schema vs a livello di valore di campo, segnale di OOV-rate)
   - quality gate (`ruff`, `mypy --strict`, `pytest` in pre-commit)
   - esempi illustrativi di risposta (`confidence`, `completeness`) — esplicitamente segnalati come illustrativi, non misure aggregate
4.3 ColdRAG:
   - `PerformanceTracker` (`metrics.py`): latenza, token stimati, costo, throughput
   - suite Pytest (`test_models.py`, `test_workflow.py`)
   - run illustrativa end-to-end (esempio infrastrutturale: 17.50 s, 5 item, ~1200 token, $0.00102, 68.57 TPS)
4.4 Sintesi comparativa e limiti della valutazione attuale
4.5 Nota esplicita sull'assenza di benchmark formali come limitazione riconosciuta

---

### Capitolo 5 — Conclusioni
*(scritto per ultimo)*

5.1 Riepilogo degli obiettivi e di come sono stati raggiunti
5.2 Sintesi cross-progetto: le due metà (offerta/domanda) della pipeline dati Dometria; filosofia comune evidence-grounded
5.3 Limitazioni
5.4 Sviluppi futuri: benchmark formale contro baseline, ingestione dinamica da DB relazionale, gestione della deprecazione dei prodotti, incorporazione di segnali collaborativi nel grafo

---

## Part 2 — Condensed Spec Digests (for compiling Chapter 3)

*Sourced directly from the `/specs` folders of both repositories (cloned and read directly, July 2026 state). These digests are written to be pasted into Cowork as ready reference material while drafting Chapter 3 — they intentionally omit background/theory (already isolated into Chapter 2) and focus on concrete implementation facts: models, libraries, configuration, pipeline steps.*

### A. dometria-bulk-insert — condensed spec digest

**Mission (`specs/mission.md`).** Stateless synchronous extraction microservice. Input `{id, text}` → output `{id, asset, confidence, completeness, _models}`. One container = one document per request; scaling is horizontal (more replicas), not in-app concurrency. Deliberately dropped an original async design (Celery + Redis + Postgres + `202 Accepted`) in favor of pushing queueing/retries/parallelism to the deployment platform.

**Tech stack (`specs/tech-stack.md`).**
- Python 3.13, `uv` for deps/venv.
- FastAPI + Uvicorn, single **synchronous** `def` endpoint (not `async def`) — deliberate, so blocking Instructor/spaCy/sentence-transformers calls run in FastAPI's threadpool without blocking the event loop; per-container concurrency capped.
- spaCy: blank pipeline + sentencizer only (no downloaded model) — used only for sentence segmentation.
- Coreference resolution folded into the Block 1 LLM scoring call (no separate NLP library — Python 3.13/spaCy 3.8 lacked `coreferee` support).
- Embeddings: `sentence-transformers`, `paraphrase-multilingual-MiniLM-L12-v2` (384-dim), lazy-loaded via `@lru_cache`, baked into the Docker image (~470 MB) for network-free cold start.
- Removed dependency: a knowledge-graph engine originally planned for lv2/lv3 matching — replaced with a plain nested-dict tree traversal (3 lv1 roots → 12 lv2 → 97 lv3 leaves).
- LLM gateway: OpenRouter via the `openai` SDK; structured output via `instructor` + Pydantic v2.
- Models: lightweight = `openai/gpt-4o-mini` (Block 1 scoring/coref, Block 2 lv1 classification); heavy = `openai/gpt-4o` (Block 3 extraction, voting, judging).
- Sampling: `LLM_TEMPERATURE=0.0`, optional `LLM_SEED`, applied to every LLM call.
- Orchestration: single `process_document(id, text, cfg)` function chaining Block 1 → 2 → 3 in-process; no broker, no worker.
- Persistence: none — service is fully stateless; PostgreSQL/SQLAlchemy/asyncpg/Alembic explicitly dropped.
- Testing/quality: `pytest` (unit mocks Instructor client; integration gated behind `-m integration`, needs `OPENROUTER_API_KEY`), `ruff`, `mypy --strict`, all run via `pre-commit`.
- Observability: stdlib `logging`, JSON lines via `python-json-logger`.
- Deployment: one Docker image (multi-stage), embedding model + `contracts/` baked in; only `OPENROUTER_API_KEY` injected at runtime; N stateless replicas behind a load balancer/autoscaler (topology owned by the systems engineer).

**API contract (`specs/mission.md`, `specs/2026-07-07-fastapi-service.md`).**
- `POST /process` — `{id, text}` → `200 {id, asset, confidence, completeness, _models}`; `asset` carries `contract_id`, `data`, `confidence`, `completeness`, `evidence` (per-field verbatim quote), `flags` (agreement/grounding/normalization notes), `review_queue` (unfilled mandatory fields). A `200` response can still need human review (low confidence + non-empty `review_queue` are *not* errors).
- `GET /health` (liveness, always 200), `GET /ready` (503 until spaCy + embedding model + offline artifacts warm).
- `GET /config/models` / `POST /config/model` — runtime, per-replica, ephemeral override of `MODEL_HEAVY`/`MODEL_LIGHTWEIGHT` (embedding excluded, baked in); gated by `RUNTIME_MODEL_OVERRIDE_ENABLED`.
- Error model: `PipelineError{stage, category, message}`; `_STATUS_MAP` — `bad_input`→400 (whitespace-only text), `unprocessable`→422 (no contract match above `CONTRACT_MIN_SCORE`), `retryable`→502 (transient upstream failure, safe to resubmit), `server`→500 (missing/malformed schema or uncaught error). FastAPI's own request-validation 422 (e.g. empty string failing `min_length=1`) is distinct and carries FastAPI's default envelope, not `PipelineError`.

**Block 1 — Preprocessing.** spaCy sentence segmentation → sliding-window chunking with overlap → one Instructor call per chunk to the lightweight LLM producing `ChunkAnalysis` (relevance score 1–10 + coreference-resolved text) in a single combined call.

**Block 2 — Contract Determination.** Stage 1: constrained lightweight-LLM call → one of 3 lv1 macro-categories (`Level1Prediction`, `Level1Literal`). Stage 2: cosine similarity between chunk embeddings and candidate `(lv2, lv3)` label embeddings, weighted by each chunk's relevance score, majority vote selects the leaf. Category tree: `CATEGORY_TREE`/`CATEGORY_NAMES`/`CATEGORY_ANCESTRY` — a plain nested dict, no graph engine (explicitly removed as over-engineered relative to a 3-level, 3-root structure).

**Block 3 — Asset Extraction (tree-driven, evidence-grounded — `specs/2026-07-03-tree-driven-extraction.md`).**
- Offline: 97 contracts unioned once into `field_tree.json` + `product_manifests.json` (`artifacts/`), built by an ingest step, not per-request.
- Runtime: Block 2's `(lv1/lv2/lv3)` path selects the product's fields; `pydantic.create_model` builds a per-product schema; every field gets a paired `{name}_quote` evidence field; every closed enum gets a `NOT_PRESENT` abstention value; a `@model_validator` rejects populated fields lacking a quote (triggers Instructor retry).
- Fields partition by a `topic` tag into **sequential** extraction groups (no `asyncio` fan-out, consistent with the synchronous-container model); `priority` gates which groups get self-consistency voting (`SELF_CONSISTENCY_N`), not execution order/dependency.
- Derivation: arithmetic/cross-field values computed in Python (`computed`), never asked of the model; rare reasoning-derived fields (`judged`) get an isolated second LLM pass over primitives + quotes only (never the raw document).
- Field metadata (enum vocabularies, descriptions, topics, priorities, derivations) lives in an editable `field_metadata.yaml` sidecar, populated offline (see compile step below); until compiled, `pending` enums are treated as free text.
- No DAG/workflow engine by design — field selection replaces conditional skipping; topic partition replaces dependency ordering.

**Post-extraction record finishing — Phase 6.10 (`specs/2026-07-07-normalization.md`).**
- Stage 4b Normalization (`normalize.py`, deterministic, no LLM): type-driven registry — dates → ISO `YYYY-MM-DD`, Italian numeric strings → `float`/`int`, text tidied; cleans in place, never fabricates, keeps+flags unparseable values; off-switch `NORMALIZE_ENABLED`.
- Stage 4c `OUT_OF_VOCAB` resolution (`resolve.py`, opt-in, quote-bounded LLM): a third enum sentinel (besides `NOT_PRESENT`) for "present but no listed value fits," always carrying a quote; a scoped judge remaps to a listed value or emits faithful free text using only the field description + its own quote (never the raw document); produces an OOV-rate signal surfaced in `eval_extraction.py`; off-switch `OOV_ENABLED`.
- Count/aggregate mechanism: a `numero_X` field whose source enumerates items rather than stating a total gets a synthesized companion `{field}__items: list[{value, quote}]` (plain transcription); the scalar becomes a code-computed `count` over it — deterministic, grounded, mandatory-satisfiable.

**Offline metadata compile — Phase 6.8 (`specs/mission.md` §Offline metadata compile).**
- `field_metadata.yaml` seeded with stubs by ingest, filled offline by `blocks/extraction/compile.py` / `scripts/compile_metadata.py` — a one-off, build-time, LLM-using tool, not part of the runtime request path.
- Batched Instructor calls (batch size `COMPILE_BATCH_SIZE`) produce, in Italian: field `description`, a proposed `topic` name, and (for closed-vocab fields) a refined enum `values` list plus an `applicable` decision; each field gets an `unsure` self-flag.
- Topic names deduped by exact string match into `artifacts/topics.yaml` (`topic → id`); `metadata.py` resolves id → name at runtime.
- CLI defaults to `--dry-run`; `--write` applies; `--field <name>` scopes to one field; idempotent (skips already-compiled fields unless `--force`).

**Topic Consolidation — Phase 6.9 (`specs/2026-07-07-topic-consolidation.md`, new addition not previously logged).**
- Problem: exact-string dedup in Phase 6.8 produced 236 topics for 1083 fields (target: ~30–40 genuinely distinct groupings), due to batch-local naming, no fuzzy dedup, and product-coupled topic names.
- Solution: an **offline, no-LLM** post-compile step using the Block 2 embedding model (`paraphrase-multilingual-MiniLM-L12-v2`) with **agglomerative clustering** (scikit-learn, cosine metric, `average` linkage default) — chosen over a greedy nearest-representative pass, which was tried first and rejected because a generic short word (`superfici`) acted as a magnet, forming a 56-member hub cluster.
- Representative name per cluster = most-used member (ties → shorter, then alphabetical); fresh integer ids assigned by cluster size.
- Config knobs: `TOPIC_CLUSTER_ENABLED` (default True), `TOPIC_CLUSTER_THRESHOLD` (default 0.6), `TOPIC_CLUSTER_LINKAGE` (default `average`), all CLI-overridable.
- Observed sweep: threshold 0.55 → 50 clusters (largest 56); 0.62 → 74 clusters (largest 25); 0.68 → 95 clusters (largest 17). Runs on both dry-run and `--write`.
- Downstream wiring unchanged: `topics.yaml` still `name → integer id`; `metadata.py` and `extract.partition_by_topic` unaffected — ids are now explicitly documented as *derived, not stable* across reruns.

**Roadmap status (`specs/roadmap.md`).** Phases 0 through 9 are all marked complete (✅): scaffolding, Pydantic models/config, Block 1, Block 2, (Block 3 — tree-driven rework), FastAPI service, runtime model override, and Phase 9 hardening (structured logging, graceful shutdown, SDK-level rate-limit backoff, API-key auth + payload guards, OpenAPI docs + `docs/RUNBOOK.md`). No phase is currently marked pending (⬜) in the retrieved roadmap.

**Contracts.** `contracts/` holds 97 JSON files (`{id}_{lv3}.json`), one per lv3 leaf; field types: `text`, `integer`, `decimal`/`currency`, `boolean`/`select`, `foreign_id`, `decimal_pair` (the last two excluded from extraction).

**Evaluation tooling.** `scripts/eval_extraction.py` (per-field variance/eval, OOV-rate signal), `scripts/measure_variance.py` (N repeated runs; reports schema-level agreement — does Block 2 flip contracts — vs field-level value-drift), `scripts/build_artifacts.py`, `scripts/compile_metadata.py`. No measured accuracy benchmark numbers found in the specs; `confidence: 0.82` / `completeness: 0.75` in the mission doc are explicitly illustrative example values, not aggregate results.

---

### B. ColdRAG — condensed spec digest

**Scope confirmed from `specs/2026-05-19-documentation/requirements.md`.** The `info/` folder (Italian-language technical docs) is the authoritative, current-state documentation, explicitly written to replace legacy references (old stack was Flask + Google-GenAI; current stack is FastAPI + OpenRouter, v3.3). Seven documents: `architettura.md`, `kg_pipeline.md`, `motore_inferenza.md`, `conversational_completion.md`, `infrastruttura.md`, `api_frontend.md`, `data_pipeline.md`.

**KG ingestion pipeline (from `info/kg_pipeline.md`, `kg_builder.py`/`ingest.py`).** Adapted from the DIAL-KG framework. Steps: deterministic Product node creation (SHA-256 id), LLM extraction of leaf entities + `product_title`, embedding generation (`BAAI/bge-m3`, 1024-dim), Coreference Alignment / Named Entity Disambiguation (Neo4j vector search + LLM Judge; "NED immunity" ensures item/product nodes are never merged into each other), Governance adjudication (Evidence check + Logical check — conservative, rejects only on outright contradiction), transactional `MERGE` via batch `UNWIND`, and Meta-Knowledge Base (MKB) auto-save.

**Retrieval / inference engine (from `info/motore_inferenza.md`, `coldrag_engine.py`).** Query analyzed by an LLM into `concetti_chiave`, a `needs_reasoning` flag, and a cumulative 1024-dim embedding. A Hybrid Router picks direct vector search vs multi-hop reasoning. Multi-hop loop: Hop-0 frontier (5 nodes via Neo4j native vector index) → fan-out Cypher (one query per hop) → edge grouping (~60% prompt compression) → LLM edge scoring (0–10) → pruning at threshold γ → iterate up to `MAX_HOPS` until enough candidates found → final LLM "blind match" ranking. Results stream to the frontend progressively via SSE. Numeric metadata anonymized with ε-differential privacy (Laplace mechanism) before exposure.

**Conversational Completion / HITL Gatekeeper (from `info/conversational_completion.md`).** `ConversationalCompletion/` module: LlamaIndex Workflows event-driven state machine (`workflow.py`, `events.py`); deterministic taxonomy semantic router over `rules.yaml`; dynamic Pydantic model generation at runtime from the taxonomy (`models.py`, RuleParser factory); LLM Judge does structured extraction and asks targeted follow-up questions for missing mandatory fields; Redis-backed session context (TTL 30 min).

**Infrastructure (from `info/infrastruttura.md`).** Neo4j is the single source of truth (nodes, edges, vector embeddings, singleton MKB). Redis ≥7.x for HITL session state. `metrics.py` defines `PerformanceTracker`: latency, estimated token counts (heuristic `len(text)//4`), API cost (configurable $/M input-output, defaults $0.30 in / $2.50 out), throughput (tokens/sec), per-item latency; `print_report()` emits a "METRICHE STACK" report, returns `{elapsed_time, total_tokens_estimated, cost_dollars, tps}`.

**API & Frontend (from `info/api_frontend.md`).** REST + WS endpoints: `/api/search` (multi-hop, SSE), `/api/ingest_product` (real-time DIAL-KG ingestion), `/ws/hitl/{session_id}`, `/api/taxonomy`, `/api/graph/overview`, `/api/db_stats`, `/api/config`, `/api/mkb`, `/api/subgraph`, `/api/egonet/{entity_id}`. Frontend: vanilla JS + vis-network.js SPA, dark theme (per `specs/2026-05-12-frontend/`).

**Configuration (from `info/architettura.md` / `infrastruttura.md`).** Key env vars: `COLDRAG_TARGET_CANDIDATES=20`, `COLDRAG_SCORE_THRESHOLD=7.0` (γ), `COLDRAG_TOP_K=5`, `COLDRAG_MAX_HOPS=5`, `COLDRAG_HOP0_FRONTIER=5`, `COLDRAG_NED_TOP_K=10`, `COLDRAG_NED_THRESHOLD=0.75`, `COLDRAG_DP_EPSILON=1.0`, `COLDRAG_SESSION_TTL=1800`, `COLDRAG_SLIDING_WINDOW=4`.

**Tech stack.** OpenRouter (OpenAI-compatible) + `instructor` in JSON mode, multi-model fallback (default `deepseek/deepseek-chat`); embeddings `BAAI/bge-m3` via sentence-transformers; Neo4j ≥5.x with native vector index (`entity_embeddings`); FastAPI + Uvicorn (WebSocket + SSE); Redis ≥7.x; `uv`; Python ≥3.13; native `asyncio` concurrency.

**Testing.** Pytest suite (`tests/`, `uv run pytest tests/ -v`): `test_models.py` (RuleParser, FinalPayload, product-ID generation), `test_workflow.py` (events, session TTL, workflow steps).

**Theory references (`specs/Teoria/`).** Contains the source PDFs for both foundational papers directly used: `ColdRAG.pdf` (Yang et al., arXiv 2505.20773) and `DIAL-KG.pdf` (Bao et al.) — confirms both should be cited distinctly in Chapter 2, with Dometria's ColdRAG explicitly flagged as an *implementation adaptation*, not the paper authors' original code (which lives separately at `github.com/WooseongYang/ColdRAG`).

**Unretrieved / unconfirmed.** `specs/Diario.md` and `specs/documentazione.md`, referenced in earlier research, do **not** appear in the current repository state (only `specs/2026-05-12-frontend/`, `specs/2026-05-19-documentation/`, `specs/Demo/`, `specs/Teoria/` exist) — treat any earlier claim about their contents as unconfirmed/superseded; a development diary may exist elsewhere in the repo (e.g. commit history) but was not located under `specs/`.

**Confirmed absence of benchmarks.** As with bulk-insert, no Recall/NDCG/HR or other recommendation-quality metrics appear anywhere in `specs/` or `info/`; the only numeric figures are configuration defaults or one illustrative infrastructure sample report (17.50 s latency, 5 items, ~1200 tokens, $0.00102, 68.57 TPS, 3.50 s/item).

---

## Part 3 — Writing Roadmap (professor's order → Cowork task sequence)

Per the professor's explicit instruction — *"Ti consiglio di partire da Capitolo 2 o 3, poi 4, lasciando intro e conclusioni in fondo"* — the drafting order is:

| Order | Chapter | What happens | Depends on |
|---|---|---|---|
| 1 | **Cap. 2 — Background** | Draft ML/LLM foundations section first (new, per feedback), then RAG/GraphRAG, cold-start, KG construction/DIAL-KG, structured output, self-consistency/LLM-as-judge, vector search, HITL/LlamaIndex Workflows, differential privacy, domain background (RICS/IVS/EVS, off-market/blind matching) | Part 2 digests above + prior full research report |
| 2 | **Cap. 3 — Sistemi Sviluppati** | Draft Part A (bulk-insert) then Part B (ColdRAG), strictly implementation-facing: models, orchestration, pre-processing, libraries, configuration — no re-explanation of theory (cross-reference Cap. 2 instead) | Part 2 digests above (both A and B sections) |
| 3 | **Cap. 4 — Risultati** | Draft using the evaluation-instruments framing (no invented benchmark numbers); explicitly state the benchmark-absence limitation | Cap. 3 draft (for terminology consistency) |
| 4 | **Cap. 1 — Introduzione** | Draft last, once scope/contributions are locked from Cap. 2–4 | Cap. 2–4 drafts |
| 5 | **Cap. 5 — Conclusioni** | Draft last, synthesizing Cap. 1–4 | All prior chapters |

**Practical Cowork sequencing suggestion:**
1. Open a Cowork session per chapter (or per Part A/Part B within Cap. 3) to keep context focused and outputs reviewable independently.
2. Feed each session the relevant slice of Part 2 above (don't paste the whole document — pick the A or B digest for Cap. 3, the full digest set for Cap. 2's domain-context anchoring).
3. After each chapter draft, send it to the professor by email per his request ("non appena hai qualcosa da farmi leggere inviami pure una mail") — I can draft that email once a chapter is ready; just say the word and I'll prepare it (I won't send anything without your confirmation).
4. Keep this document as the single source of truth for cross-chapter consistency (terminology, model names, config defaults) — update the digests here if the repos change before the thesis is finalized.

---

*Sources: direct clone and read of `/specs` in `vivri161803/ColdRAG` and `/specs` (+ `mission.md`, `tech-stack.md`, `roadmap.md`) in `vivri161803/dometria-bullk-insert`, July 21 2026, cross-checked against the prior synthesized research report in `thesis_guidelins.md`.*
