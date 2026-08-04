# Thesis

Master's thesis in Data Science & AI, University of Florence. Written in
**English**. The subject is the ColdRAG work (GraphRAG applied to matching)
built for the Dometria project.

`thesis_planning_document.md` is the authoritative outline. Follow it. If you
believe it needs changing, say so and wait — do not restructure on your own.

## Environment

Headless Debian LXC on a Proxmox host. No GUI, no display, no browser.
Running as unprivileged user `thesis`. This session is usually driven from a
phone via Remote Control, so responses are read on a small screen.

## Repository layout

```
thesis/
├── thesis_planning_document.md   # outline — the spec you write against
├── bib.md                        # source bibliography (articles to cite)
├── tex/                          # ALL LaTeX source lives here, nowhere else
│   ├── main.tex                  # preamble + \input{} only, no prose
│   ├── refs.bib                  # generated from bib.md
│   └── NN_section.tex            # one file per component, numbered
└── build/                        # latexmk output only — never edit by hand
```

`build/` holds the compiled PDF and latexmk's intermediate artifacts, nothing
else. Never copy, snapshot, or version `.tex` files into it — history is git's
job.

## Build

```bash
cd tex && latexmk -pdf -interaction=nonstopmode -halt-on-error \
  -output-directory=../build main.tex
```

- Toolchain is **texlive + latexmk**. Tectonic is not installed and does not
  work here — never suggest it.
- Installed: `texlive-latex-recommended`, `texlive-latex-extra`,
  `texlive-fonts-recommended`, `latexmk`. If you need a package outside these,
  name the `texlive-*` package that provides it and stop — do not install it.
- Clean with `latexmk -C -output-directory=../build` from `tex/`.
- Build after every set of edits. A section that does not compile is not done.
- Report the compile result in one line. Do not paste the LaTeX log unless it
  failed, and then only the relevant error.
- The PDF in `build/` is served over the tailnet. You do not need to open it.

## LaTeX structure

Strict main + components:

- `main.tex` holds documentclass, packages, macros, metadata, and a sequence
  of `\input{}` calls. **No prose ever goes in `main.tex`.**
- Each component is one `.tex` file in `tex/`, numbered by document order.
- A component file starts at `\section{}` or `\chapter{}` — no preamble, no
  `\begin{document}`.
- Do not create a new component file without asking. The section list comes
  from the planning document.
- Keep the preamble minimal. Add a package only when something actually needs
  it, and say why in the commit message.

## Tone

Concise, academic, precise. Concretely:

- Prefer the shortest sentence that carries the claim. Cut hedging, throat
  clearing, and transition padding ("It is important to note that…").
- Every claim is either cited, derived from my own work, or removed.
- Define a term once, on first use, then use it consistently. No synonyms for
  technical terms.
- Present tense for what the system does, past tense for what was done.
- No marketing register: nothing is "powerful", "novel", or "state of the
  art" unless that is a measured comparison against a named baseline.
- Passive voice is acceptable where the actor is irrelevant; do not use it to
  hide who did what.

## Citations

- `bib.md` is the source of truth for what may be cited. I maintain it; you
  do not edit it.
- **You own `tex/refs.bib`** and generate it from `bib.md`. Before citing
  anything, check that its entry exists in `refs.bib` and add it if not.
- Only cite entries that appear in `bib.md`. Never invent a citation, a
  number, or a result. If a claim needs a source you do not have, write
  `\todo{cite}` and continue.
- Entries must be complete: authors, title, venue, year, DOI or URL. No
  placeholder keys, no `{n.d.}` years. If `bib.md` lacks a field you need,
  ask rather than guessing.
- Citation keys: `lastnameYEARkeyword`, e.g. `chen2024coldrag`. Stable once
  used — never rename a key that already appears in the text.

## Reference implementations

Everything you need is written below. **Do not fetch these URLs, clone the
repos, or make any network request about them unless I explicitly tell you to
in that message.** Standing permission is never implied — not by a question
that would be easier to answer with a fetch, not by a gap in this file. If
something here is missing or looks stale, say what you need and stop.

- `https://github.com/vivri161803/ColdRAG`
- `https://github.com/vivri161803/dometria-bullk-insert` (name unverified)

### ColdRAG — what it is

Prototype recommendation system addressing the cold-start problem by
combining retrieval-augmented generation with knowledge-graph reasoning. The
graph is built by an extraction pipeline adapted from the DIAL-KG framework
and lives entirely in Neo4j. A human-in-the-loop conversational module handles
structured data acquisition with dynamic Pydantic validation.

Current domain is real-estate M&A (~30 subcategories). The architecture is
domain-agnostic: swapping `rules.yaml` and the source data retargets it.

### Stack

| Layer | Technology |
| --- | --- |
| LLM engine | OpenRouter (OpenAI-compatible) + `instructor` in JSON mode |
| Embeddings | `BAAI/bge-m3` via sentence-transformers, 1024-dim, cosine |
| Graph + vector store | Neo4j — native vector index, nodes/edges, MKB singleton |
| Backend | FastAPI + Uvicorn (ASGI), WebSocket + SSE |
| HITL orchestration | LlamaIndex Workflows (event-driven) |
| Session store | Redis, 30-minute TTL |
| Frontend | Vanilla JS + vis-network.js |
| Packaging | `uv`, Python ≥ 3.13 |
| Privacy | ε-differential privacy, Laplace mechanism |

### Pipeline 1 — ingestion (DIAL-KG)

Document → deterministic Product node (SHA-256 of text) → LLM extraction of
leaf entities and product title → coreference alignment (NED) via vector
search plus an LLM judge → governance layer applying an evidence check and a
logical check → transactional MERGE into Neo4j using batched UNWIND → entity
profiles auto-saved to the Meta-Knowledge Base.

Three guarantees worth stating in the thesis: the product node is idempotent
(same text yields the same ID); item and product nodes are never merged by
NED ("NED immunity"); governance is conservative, rejecting a fact only when
the text contradicts it.

### Pipeline 2 — multi-hop retrieval

Query → LLM extracts key concepts and a `needs_reasoning` flag → hybrid router
chooses direct vector search or multi-hop → hop-0 frontier of 5 nodes via
vector search → multi-hop loop up to `MAX_HOPS`, each iteration doing a
fan-out Cypher query, edge grouping (roughly 60% prompt compression), LLM
scoring of each edge on 0–10, and pruning below the γ threshold → final
ranking by LLM blind match with justified ordering → metadata anonymized under
ε-DP. Candidates stream to the frontend over SSE as exploration proceeds.

### Pipeline 3 — HITL gatekeeper

User selects intent → macro-category → subcategory, then a loop: an LLM judge
performs structured extraction against a Pydantic model generated at runtime
from `rules.yaml`; missing fields trigger a targeted streamed question; once
all mandatory fields validate, a summary and confirmation produce a structured
payload routed to either ingestion or search.

### Default hyperparameters

| Parameter | Default |
| --- | --- |
| `COLDRAG_TARGET_CANDIDATES` | 20 |
| `COLDRAG_SCORE_THRESHOLD` (γ) | 7.0 |
| `COLDRAG_TOP_K` | 5 |
| `COLDRAG_MAX_HOPS` | 5 |
| `COLDRAG_HOP0_FRONTIER` | 5 |
| `COLDRAG_NED_TOP_K` | 10 |
| `COLDRAG_NED_THRESHOLD` | 0.75 |
| `COLDRAG_DP_EPSILON` | 1.0 |
| `COLDRAG_SESSION_TTL` | 1800 s |
| `COLDRAG_SLIDING_WINDOW` | 4 messages |

These are the documented defaults, not measured results. If the thesis needs
the values actually used in an experiment, ask me — do not present a default
as an experimental setting.

### Module map

`coldrag_engine.py` multi-hop reasoning · `kg_builder.py` DIAL-KG pipeline
(extraction, NED, governance) · `ingest.py` incremental CLI ingestion ·
`fastapi_app.py` backend (WebSocket HITL, REST, SSE) · `pydantic_classes.py`
data models · `config.py` centralized configuration · `metrics.py` latency,
token and cost tracking · `lib/neo4j_manager.py` and `lib/redis_manager.py`
async drivers · `ConversationalCompletion/` HITL workflow, events, semantic
router, `rules.yaml` taxonomy.

Theoretical grounding: the ColdRAG paper and the DIAL-KG paper.

### Constraints on use

- Any figure or number in the thesis must come from this file or from `bib.md`.
  If neither has it, write `\todo{}` and tell me what is missing.
- Both repos are documented in Italian. The thesis is English — translate
  terminology consistently and do not carry Italian phrasing across.
- Do not infer implementation details that are not stated here. "The code
  probably does X" never reaches the page.

Note both repos are documented in Italian. The thesis is in English —
translate terminology consistently and do not carry Italian phrasing across.

## Working style

- Keep responses short. Summarize what changed; do not echo file contents.
- One component at a time. Never rewrite a whole section unless asked.
- When proposing prose, show the paragraph, not the surrounding file.
- I review the rendered PDF and come back with changes. Optimize for small,
  reviewable diffs.

## Git

- Commit after each component or meaningful revision. Message format:
  `<file>: <what changed>`, e.g. `03_method: tighten NED description`.
- Never force-push, rebase, or amend published commits.
- `build/` is gitignored.

## Out of scope

- Do not modify system config, systemd units, or Tailscale settings.
- Do not install packages.
- Do not touch anything outside this directory.
