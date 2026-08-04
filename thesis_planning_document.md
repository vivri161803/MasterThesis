afting order is:
 
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
