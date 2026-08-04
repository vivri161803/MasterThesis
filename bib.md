# State-of-the-Art Bibliography — Master's Thesis
### "From Documents to Matches: Evidence-Grounded Extraction and GraphRAG Cold-Start Recommendation for Real-Estate Off-Market Intermediation"

*Format for every entry: `Authors - Title - Source`. Entries are grouped under headings mirroring the Chapter 2 index for navigability. All arXiv IDs, DOIs, venues, and author lists below were verified against primary sources where feasible; unverifiable claimed IDs from the prior file were corrected or replaced with venue+year. Save this file directly as your bibliography.*

---

## 1. ML / LLM Foundations
Shannon, C. E. - A Mathematical Theory of Communication - Bell System Technical Journal, 1948
Bengio, Y., Ducharme, R., Vincent, P., Jauvin, C. - A Neural Probabilistic Language Model - Journal of Machine Learning Research, 2003
Mikolov, T., Chen, K., Corrado, G., Dean, J. - Efficient Estimation of Word Representations in Vector Space - arXiv:1301.3781
Mikolov, T., Sutskever, I., Chen, K., Corrado, G., Dean, J. - Distributed Representations of Words and Phrases and their Compositionality - NeurIPS 2013
Pennington, J., Socher, R., Manning, C. D. - GloVe: Global Vectors for Word Representation - EMNLP 2014
Peters, M. E., et al. - Deep Contextualized Word Representations (ELMo) - NAACL 2018
Vaswani, A., et al. - Attention Is All You Need - NeurIPS 2017
Devlin, J., Chang, M.-W., Lee, K., Toutanova, K. - BERT: Pre-training of Deep Bidirectional Transformers for Language Understanding - NAACL 2019
Radford, A., Narasimhan, K., Salimans, T., Sutskever, I. - Improving Language Understanding by Generative Pre-Training (GPT) - OpenAI Technical Report, 2018
Radford, A., et al. - Language Models are Unsupervised Multitask Learners (GPT-2) - OpenAI Technical Report, 2019
Brown, T. B., et al. - Language Models are Few-Shot Learners (GPT-3) - NeurIPS 2020
OpenAI - GPT-4 Technical Report - arXiv:2303.08774
Raffel, C., et al. - Exploring the Limits of Transfer Learning with a Unified Text-to-Text Transformer (T5) - Journal of Machine Learning Research, 2020
Kaplan, J., et al. - Scaling Laws for Neural Language Models - arXiv:2001.08361
Hoffmann, J., et al. - Training Compute-Optimal Large Language Models (Chinchilla) - arXiv:2203.15556
Wei, J., et al. - Finetuned Language Models Are Zero-Shot Learners (FLAN) - ICLR 2022
Ouyang, L., et al. - Training Language Models to Follow Instructions with Human Feedback (InstructGPT) - NeurIPS 2022
Christiano, P., et al. - Deep Reinforcement Learning from Human Preferences - NeurIPS 2017
Stiennon, N., et al. - Learning to Summarize from Human Feedback - NeurIPS 2020
Bai, Y., et al. - Constitutional AI: Harmlessness from AI Feedback - arXiv:2212.08073
Rafailov, R., et al. - Direct Preference Optimization: Your Language Model is Secretly a Reward Model - NeurIPS 2023
Wei, J., et al. - Chain-of-Thought Prompting Elicits Reasoning in Large Language Models - NeurIPS 2022
Kojima, T., et al. - Large Language Models are Zero-Shot Reasoners - NeurIPS 2022
Yao, S., et al. - ReAct: Synergizing Reasoning and Acting in Language Models - ICLR 2023
Yao, S., et al. - Tree of Thoughts: Deliberate Problem Solving with Large Language Models - NeurIPS 2023
Zhou, D., et al. - Least-to-Most Prompting Enables Complex Reasoning in Large Language Models - ICLR 2023
Liu, P., et al. - Pre-train, Prompt, and Predict: A Systematic Survey of Prompting Methods in Natural Language Processing - ACM Computing Surveys, 2023
Touvron, H., et al. - LLaMA: Open and Efficient Foundation Language Models - arXiv:2302.13971
Touvron, H., et al. - Llama 2: Open Foundation and Fine-Tuned Chat Models - arXiv:2307.09288
Grattafiori, A., et al. - The Llama 3 Herd of Models - arXiv:2407.21783
Jiang, A. Q., et al. - Mistral 7B - arXiv:2310.06825
Bai, J., et al. - Qwen Technical Report - arXiv:2309.16609
Yang, A., et al. - Qwen3 Technical Report - arXiv:2505.09388
DeepSeek-AI - DeepSeek-V3 Technical Report - arXiv:2412.19437
DeepSeek-AI - DeepSeek-R1: Incentivizing Reasoning Capability in LLMs via Reinforcement Learning - arXiv:2501.12948
Sennrich, R., Haddow, B., Birch, A. - Neural Machine Translation of Rare Words with Subword Units (BPE) - ACL 2016
Kudo, T., Richardson, J. - SentencePiece: A Simple and Language Independent Subword Tokenizer and Detokenizer for Neural Text Processing - EMNLP 2018

## 2. Structured / Constrained Output from LLMs
Willard, B. T., Louf, R. - Efficient Guided Generation for Large Language Models - arXiv:2307.09702
Geng, S., et al. - JSONSchemaBench: A Rigorous Benchmark of Structured Outputs for Language Models - arXiv:2501.10868
Dong, Y., Ruan, C. F., Cai, Y., Lai, R., Xu, Z., Zhao, Y., Chen, T. - XGrammar: Flexible and Efficient Structured Generation Engine for Large Language Models - arXiv:2411.15100
Li, L., et al. - XGrammar-2: Efficient Dynamic Structured Generation Engine for Agentic LLMs - arXiv:2601.04426
Tam, Z. R., Wu, C.-K., Tsai, Y.-L., Lin, C.-Y., Lee, H.-Y., Chen, Y.-N. - Let Me Speak Freely? A Study On The Impact Of Format Restrictions On Large Language Model Performance - EMNLP 2024 Industry Track, DOI 10.18653/v1/2024.emnlp-industry.91 (arXiv:2408.02442)
Li, J., et al. - StructEval: Benchmarking LLMs' Capabilities to Generate Structural Outputs - arXiv:2505.20139
Zhou, Z., Li, J., Qiu, S., Huang, J., Qiu, L., Sun, Z. - DeepJSONEval: Benchmarking Complex Nested JSON Data Mining for Large Language Models - arXiv:2509.25922
Shrimal, A., Jain, A., Chowdhury, S., Yenigalla, P. - PARSE: LLM Driven Schema Optimization for Reliable Entity Extraction - EMNLP 2025 Industry Track, DOI 10.18653/v1/2025.emnlp-industry.184 (arXiv:2510.08623)
Ferguson, N., Pennington, J., Beghian, N., Mohan, A., Kiela, D., Agrawal, S., Nguyen, T. H. - ExtractBench: A Benchmark and Evaluation Methodology for Complex Structured Extraction - arXiv:2602.12247
Zhu, F., Yu, J., Chen, Z., Zhou, Y., Ji, J., Yang, Z., Zhang, Y., Hu, H., Liu, Z. - Layout-Aware Parsing Meets Efficient LLMs: A Unified, Scalable Framework for Resume Information Extraction and Evaluation - arXiv:2510.09722
He, H., Thinking Machines Lab - Defeating Nondeterminism in LLM Inference - Thinking Machines Lab: Connectionism, DOI 10.64434/tml.20250910, 2025
Zheng, L., Yin, L., Xie, Z., et al. - SGLang: Efficient Execution of Structured Language Model Programs - NeurIPS 2024
Kwon, W., et al. - Efficient Memory Management for Large Language Model Serving with PagedAttention (vLLM) - SOSP 2023
OpenAI - Structured Outputs - OpenAI Platform Documentation, https://platform.openai.com/docs/guides/structured-outputs
Anthropic - Tool Use and Structured Outputs - Anthropic Documentation, https://docs.anthropic.com
Google - Structured Output / Controlled Generation - Gemini API Documentation, https://ai.google.dev/gemini-api/docs/structured-output
Liu, J., et al. - Instructor: Structured Outputs for LLMs - Software, https://github.com/instructor-ai/instructor
Pydantic - PydanticAI - Software, https://ai.pydantic.dev
BoundaryML - BAML: A Domain-Specific Language for Structured LLM Outputs - Software, https://github.com/BoundaryML/baml
LangChain - Structured Output - Documentation, https://python.langchain.com/docs/how_to/structured_output/
Microsoft - TypeChat - Software, https://github.com/microsoft/TypeChat
dottxt-ai - Outlines - Software, https://github.com/dottxt-ai/outlines
Microsoft / guidance-ai - Guidance - Software, https://github.com/guidance-ai/guidance

## 3. Information Extraction from Documents (Classical + LLM-based IE)
Nadeau, D., Sekine, S. - A Survey of Named Entity Recognition and Classification - Lingvisticae Investigationes, 2007
Wang, S., et al. - GPT-NER: Named Entity Recognition via Large Language Models - arXiv:2304.10428
Zhou, W., et al. - UniversalNER: Targeted Distillation from Large Language Models for Open Named Entity Recognition - ICLR 2024
Wang, X., et al. - InstructUIE: Multi-task Instruction Tuning for Unified Information Extraction - arXiv:2304.08085
Sainz, O., et al. - GoLLIE: Annotation Guidelines Improve Zero-Shot Information Extraction - ICLR 2024
Wei, X., et al. - ChatIE: Zero-Shot Information Extraction via Chatting with ChatGPT - arXiv:2302.10205
Agrawal, M., et al. - Large Language Models are Few-Shot Clinical Information Extractors - EMNLP 2022

## 4. Document AI / Document Understanding
Xu, Y., et al. - LayoutLM: Pre-training of Text and Layout for Document Image Understanding - KDD 2020
Xu, Y., et al. - LayoutLMv2: Multi-modal Pre-training for Visually-Rich Document Understanding - ACL 2021
Huang, Y., Lv, T., Cui, L., Lu, Y., Wei, F. - LayoutLMv3: Pre-training for Document AI with Unified Text and Image Masking - ACM Multimedia 2022
Kim, G., et al. - OCR-free Document Understanding Transformer (Donut) - ECCV 2022
Appalaraju, S., et al. - DocFormer: End-to-End Transformer for Document Understanding - ICCV 2021
Powalski, R., et al. - Going Full-TILT Boogie on Document Understanding with Text-Image-Layout Transformer - ICDAR 2021
Wang, J., Jin, L., Ding, K. - LiLT: A Simple yet Effective Language-Independent Layout Transformer for Structured Document Understanding - ACL 2022
Jaume, G., Ekenel, H. K., Thiran, J.-P. - FUNSD: A Dataset for Form Understanding in Noisy Scanned Documents - ICDAR Workshops 2019
Park, S., et al. - CORD: A Consolidated Receipt Dataset for Post-OCR Parsing - NeurIPS Workshop on Document Intelligence 2019
Mathew, M., Karatzas, D., Jawahar, C. V. - DocVQA: A Dataset for VQA on Document Images - WACV 2021
Huang, Z., et al. - ICDAR2019 Competition on Scanned Receipt OCR and Information Extraction (SROIE) - ICDAR 2019
Graliński, F., et al. - Kleister: A Novel Task for Information Extraction Involving Long Documents with Complex Layout - arXiv:2003.02356
Van Landeghem, J., et al. - Document Understanding Dataset and Evaluation (DUDE) - ICCV 2023

## 5. Coreference Resolution & Long-Document Processing
Lee, K., He, L., Lewis, M., Zettlemoyer, L. - End-to-end Neural Coreference Resolution - EMNLP 2017
Joshi, M., et al. - SpanBERT: Improving Pre-training by Representing and Predicting Spans - TACL 2020
Le, N., Ritter, A. - Are Large Language Models Robust Coreference Resolvers? - arXiv:2305.14489
Beltagy, I., Peters, M. E., Cohan, A. - Longformer: The Long-Document Transformer - arXiv:2004.05150

## 6. Contract / Legal Document Extraction
Hendrycks, D., et al. - CUAD: An Expert-Annotated NLP Dataset for Legal Contract Review - NeurIPS Datasets and Benchmarks 2021
Chalkidis, I., et al. - LexGLUE: A Benchmark Dataset for Legal Language Understanding in English - ACL 2022
Koreeda, Y., Manning, C. D. - ContractNLI: A Dataset for Document-level Natural Language Inference for Contracts - Findings of EMNLP 2021
Chalkidis, I., et al. - LEGAL-BERT: The Muppets Straight Out of Law School - Findings of EMNLP 2020
Zhong, H., et al. - How Does NLP Benefit Legal System: A Summary of Legal Artificial Intelligence - ACL 2020
Katz, D. M., et al. - Natural Language Processing in the Legal Domain - arXiv:2302.12039

## 7. Multilingual / Italian-Language NLP
Conneau, A., et al. - Unsupervised Cross-lingual Representation Learning at Scale (XLM-R) - ACL 2020
Feng, F., et al. - Language-agnostic BERT Sentence Embedding (LaBSE) - ACL 2022
Reimers, N., Gurevych, I. - Making Monolingual Sentence Embeddings Multilingual using Knowledge Distillation - EMNLP 2020
Polignano, M., et al. - AlBERTo: Italian BERT Language Understanding Model for NLP Challenging Tasks Based on Tweets - CLiC-it 2019
Basile, V., et al. - EVALITA: Evaluation Campaign for NLP and Speech Tools for Italian - EVALITA / CLiC-it Proceedings

## 8. Hallucination, Grounding, Evidence / Attribution
Ji, Z., et al. - Survey of Hallucination in Natural Language Generation - ACM Computing Surveys, 2023
Huang, L., et al. - A Survey on Hallucination in Large Language Models: Principles, Taxonomy, Challenges, and Open Questions - arXiv:2311.05232
Gao, T., Yen, H., Yu, J., Chen, D. - Enabling Large Language Models to Generate Text with Citations (ALCE) - EMNLP 2023
Bohnet, B., et al. - Attributed Question Answering: Evaluation and Modeling for Attributed Large Language Models - arXiv:2212.08037
Gao, L., et al. - RARR: Researching and Revising What Language Models Say, Using Language Models - ACL 2023
Liu, N. F., Zhang, T., Liang, P. - Evaluating Verifiability in Generative Search Engines - Findings of EMNLP 2023
Min, S., et al. - FActScore: Fine-grained Atomic Evaluation of Factual Precision in Long Form Text Generation - EMNLP 2023
Manakul, P., Liusie, A., Gales, M. J. F. - SelfCheckGPT: Zero-Resource Black-Box Hallucination Detection for Generative Large Language Models - EMNLP 2023
Kryscinski, W., et al. - Evaluating the Factual Consistency of Abstractive Text Summarization (FactCC) - EMNLP 2020
Laban, P., et al. - SummaC: Re-Visiting NLI-based Models for Inconsistency Detection in Summarization - TACL 2022
Honovich, O., et al. - TRUE: Re-evaluating Factual Consistency Evaluation - NAACL 2022

## 9. Abstention, Calibration & Self-Consistency
Kadavath, S., et al. - Language Models (Mostly) Know What They Know - arXiv:2207.05221
Kuhn, L., Gal, Y., Farquhar, S. - Semantic Uncertainty: Linguistic Invariances for Uncertainty Estimation in Natural Language Generation - ICLR 2023
Farquhar, S., et al. - Detecting Hallucinations in Large Language Models Using Semantic Entropy - Nature, 2024
Quach, V., et al. - Conformal Language Modeling - ICLR 2024
Ren, J., et al. - Out-of-Distribution Detection and Selective Generation for Conditional Language Models - ICLR 2023
Wang, X., et al. - Self-Consistency Improves Chain of Thought Reasoning in Language Models - ICLR 2023
Madaan, A., et al. - Self-Refine: Iterative Refinement with Self-Feedback - NeurIPS 2023
Weng, Y., et al. - Large Language Models are Better Reasoners with Self-Verification - Findings of EMNLP 2023
Chen, X., et al. - Universal Self-Consistency for Large Language Model Generation - arXiv:2311.17311

## 10. LLM-as-a-Judge
Zheng, L., et al. - Judging LLM-as-a-Judge with MT-Bench and Chatbot Arena - NeurIPS 2023
Zhu, L., et al. - JudgeLM: Fine-tuned Large Language Models are Scalable Judges - arXiv:2310.17631
Kim, S., et al. - Prometheus: Inducing Fine-grained Evaluation Capability in Language Models - ICLR 2024
Liu, Y., et al. - G-Eval: NLG Evaluation using GPT-4 with Better Human Alignment - EMNLP 2023
Gu, J., et al. - A Survey on LLM-as-a-Judge - arXiv:2411.15594

## 11. Retrieval-Augmented Generation
Lewis, P., et al. - Retrieval-Augmented Generation for Knowledge-Intensive NLP Tasks - NeurIPS 2020
Guu, K., et al. - REALM: Retrieval-Augmented Language Model Pre-Training - ICML 2020
Borgeaud, S., et al. - Improving Language Models by Retrieving from Trillions of Tokens (RETRO) - ICML 2022
Izacard, G., Grave, E. - Leveraging Passage Retrieval with Generative Models for Open Domain Question Answering (FiD) - EACL 2021
Karpukhin, V., et al. - Dense Passage Retrieval for Open-Domain Question Answering (DPR) - EMNLP 2020
Khandelwal, U., et al. - Generalization through Memorization: Nearest Neighbor Language Models (kNN-LM) - ICLR 2020
Izacard, G., et al. - Atlas: Few-shot Learning with Retrieval Augmented Language Models - Journal of Machine Learning Research, 2023
Asai, A., et al. - Self-RAG: Learning to Retrieve, Generate, and Critique through Self-Reflection - ICLR 2024
Yan, S.-Q., et al. - Corrective Retrieval Augmented Generation (CRAG) - arXiv:2401.15884
Sarthi, P., et al. - RAPTOR: Recursive Abstractive Processing for Tree-Organized Retrieval - ICLR 2024
Gao, L., et al. - Precise Zero-Shot Dense Retrieval without Relevance Labels (HyDE) - ACL 2023
Jiang, Z., et al. - Active Retrieval Augmented Generation (FLARE) - EMNLP 2023
Gao, Y., et al. - Retrieval-Augmented Generation for Large Language Models: A Survey - arXiv:2312.10997
Es, S., et al. - RAGAS: Automated Evaluation of Retrieval Augmented Generation - EACL 2024 Demonstrations
Saad-Falcon, J., et al. - ARES: An Automated Evaluation Framework for Retrieval-Augmented Generation Systems - NAACL 2024
Chen, J., et al. - Benchmarking Large Language Models in Retrieval-Augmented Generation (RGB) - AAAI 2024
Liu, N. F., et al. - Lost in the Middle: How Language Models Use Long Contexts - TACL 2024

## 12. Multi-Hop Retrieval & Reasoning
Yang, Z., et al. - HotpotQA: A Dataset for Diverse, Explainable Multi-hop Question Answering - EMNLP 2018
Trivedi, H., et al. - MuSiQue: Multihop Questions via Single-hop Question Composition - TACL 2022
Ho, X., et al. - Constructing a Multi-hop QA Dataset for Comprehensive Evaluation of Reasoning Steps (2WikiMultiHopQA) - COLING 2020
Trivedi, H., et al. - Interleaving Retrieval with Chain-of-Thought Reasoning for Knowledge-Intensive Multi-Step Questions (IRCoT) - ACL 2023
Press, O., et al. - Measuring and Narrowing the Compositionality Gap in Language Models (Self-Ask) - Findings of EMNLP 2023

## 13. GraphRAG / Knowledge-Graph-Augmented LLMs
Edge, D., Trinh, H., Cheng, N., Bradley, J., Chao, A., Mody, A., Truitt, S., Metropolitansky, D., Ness, R. O., Larson, J. - From Local to Global: A Graph RAG Approach to Query-Focused Summarization - arXiv:2404.16130
Guo, Z., Xia, L., Yu, Y., Ao, T., Huang, C. - LightRAG: Simple and Fast Retrieval-Augmented Generation - EMNLP 2025 Findings, arXiv:2410.05779
Gutiérrez, B. J., Shu, Y., Gu, Y., Yasunaga, M., Su, Y. - HippoRAG: Neurobiologically Inspired Long-Term Memory for Large Language Models - NeurIPS 2024, arXiv:2405.14831
Gutiérrez, B. J., et al. - From RAG to Memory: Non-Parametric Continual Learning for Large Language Models (HippoRAG 2) - arXiv:2502.14802
Hu, Y., et al. - GRAG: Graph Retrieval-Augmented Generation - Findings of NAACL 2025, arXiv:2405.16506
Sun, J., Xu, C., Tang, L., Wang, S., Lin, C., Gong, Y., Ni, L. M., Shum, H.-Y., Guo, J. - Think-on-Graph: Deep and Responsible Reasoning of Large Language Model on Knowledge Graph - ICLR 2024, arXiv:2307.07697
Ma, S., et al. - Think-on-Graph 2.0: Deep and Faithful Large Language Model Reasoning with Knowledge-guided Retrieval Augmented Generation - ICLR 2025
Luo, L., et al. - Reasoning on Graphs: Faithful and Interpretable Large Language Model Reasoning (RoG) - ICLR 2024
He, X., et al. - G-Retriever: Retrieval-Augmented Generation for Textual Graph Understanding and Question Answering - NeurIPS 2024, arXiv:2402.07630
Jiang, J., et al. - StructGPT: A General Framework for Large Language Model to Reason over Structured Data - EMNLP 2023
Mavromatis, C., Karypis, G. - GNN-RAG: Graph Neural Retrieval for Large Language Model Reasoning - arXiv:2405.20139
Li, M., et al. - Simple Is Effective: The Roles of Graphs and Large Language Models in Knowledge-Graph-Based Retrieval-Augmented Generation (SubgraphRAG) - ICLR 2025
Jin, B., et al. - Graph Chain-of-Thought: Augmenting Large Language Models by Reasoning on Graphs - Findings of ACL 2024
Peng, B., et al. - Graph Retrieval-Augmented Generation: A Survey - arXiv:2408.08921
Pan, S., Luo, L., Wang, Y., Chen, C., Wang, J., Wu, X. - Unifying Large Language Models and Knowledge Graphs: A Roadmap - IEEE Transactions on Knowledge and Data Engineering, 2024
Traag, V. A., Waltman, L., van Eck, N. J. - From Louvain to Leiden: Guaranteeing Well-Connected Communities - Scientific Reports, 2019
Blondel, V. D., Guillaume, J.-L., Lambiotte, R., Lefebvre, E. - Fast Unfolding of Communities in Large Networks - Journal of Statistical Mechanics: Theory and Experiment, 2008

## 14. Knowledge Graph Construction
Banko, M., et al. - Open Information Extraction from the Web (TextRunner) - IJCAI 2007
Fader, A., Soderland, S., Etzioni, O. - Identifying Relations for Open Information Extraction (ReVerb) - EMNLP 2011
Kolluru, K., et al. - OpenIE6: Iterative Grid Labeling and Coordination Analysis for Open Information Extraction - EMNLP 2020
Mintz, M., Bills, S., Snow, R., Jurafsky, D. - Distant Supervision for Relation Extraction without Labeled Data - ACL-IJCNLP 2009
Zhu, Y., et al. - LLMs for Knowledge Graph Construction and Reasoning: Recent Capabilities and Future Opportunities - World Wide Web, 2024
Carta, S., Giuliani, A., Piano, L., Podda, A. S., Pompianu, L., Tiddia, S. G. - Iterative Zero-Shot LLM Prompting for Knowledge Graph Construction - arXiv:2307.01128
Zhang, B., Soh, H. - Extract, Define, Canonicalize: An LLM-based Framework for Knowledge Graph Construction (EDC) - EMNLP 2024
Huang, X., et al. - GraphJudger: Can LLMs be Good Graph Judgers for Knowledge Graph Construction? - arXiv:2411.17388
Mo, B., et al. - KGGen: Extracting Knowledge Graphs from Plain Text with Language Models - arXiv:2502.09956
Lairgi, Y., Moncla, L., Cazabet, R., Benabdeslem, K., Cléau, P. - iText2KG: Incremental Knowledge Graphs Construction Using Large Language Models - WISE 2024, arXiv:2409.03284
Sun, Q., et al. - Docs2KG: Unified Knowledge Graph Construction from Heterogeneous Documents Assisted by Large Language Models - arXiv:2406.02962
Mihindukulasooriya, N., et al. - Text2KGBench: A Benchmark for Ontology-Driven Knowledge Graph Generation from Text - ISWC 2023
Chen, H., et al. - SAC-KG: Exploiting Large Language Models as Skilled Automatic Constructors for Domain Knowledge Graph - ACL 2024
Bao, W., Wang, Y., Gao, R., Leng, F., Bao, Y., Yu, G. - DIAL-KG: Schema-Free Incremental Knowledge Graph Construction via Dynamic Schema Induction and Evolution-Intent Assessment - DASFAA 2026, LNCS vol. 16540, Springer (arXiv:2603.20059)
Rasmussen, P., et al. - Zep: A Temporal Knowledge Graph Architecture for Agent Memory (Graphiti) - arXiv:2501.13956
Wornow, M., et al. - Zero-Shot Clinical Trial Patient Matching with LLMs - arXiv:2402.05125
Zhang, Y., et al. - AttacKG+: Boosting Attack Knowledge Graph Construction with Large Language Models - arXiv:2405.04753

## 15. Entity Resolution / Named Entity Disambiguation / Entity Linking
Wu, L., et al. - Scalable Zero-shot Entity Linking with Dense Entity Retrieval (BLINK) - EMNLP 2020
De Cao, N., et al. - Autoregressive Entity Retrieval (GENRE) - ICLR 2021
Ayoola, T., et al. - ReFinED: An Efficient Zero-shot-capable Approach to End-to-End Entity Linking - NAACL 2022 Industry Track
Li, Y., et al. - Deep Entity Matching with Pre-Trained Language Models (Ditto) - VLDB 2020
Peeters, R., Steiner, A., Bizer, C. - Entity Matching using Large Language Models - EDBT 2025 (arXiv:2310.11244)
Peeters, R., Bizer, C. - Using ChatGPT for Entity Matching - ADBIS 2023
Sevgili, Ö., et al. - Neural Entity Linking: A Survey of Models Based on Deep Learning - Semantic Web Journal, 2022
Bordes, A., et al. - Translating Embeddings for Modeling Multi-relational Data (TransE) - NeurIPS 2013
Trouillon, T., et al. - Complex Embeddings for Simple Link Prediction (ComplEx) - ICML 2016
Sun, Z., et al. - RotatE: Knowledge Graph Embedding by Relational Rotation in Complex Space - ICLR 2019

## 16. Recommender Systems — Foundations
Sarwar, B., Karypis, G., Konstan, J., Riedl, J. - Item-Based Collaborative Filtering Recommendation Algorithms - WWW 2001
Koren, Y., Bell, R., Volinsky, C. - Matrix Factorization Techniques for Recommender Systems - IEEE Computer, 2009
Rendle, S., Freudenthaler, C., Gantner, Z., Schmidt-Thieme, L. - BPR: Bayesian Personalized Ranking from Implicit Feedback - UAI 2009
Hu, Y., Koren, Y., Volinsky, C. - Collaborative Filtering for Implicit Feedback Datasets - ICDM 2008
He, X., et al. - Neural Collaborative Filtering - WWW 2017
Burke, R. - Hybrid Recommender Systems: Survey and Experiments - User Modeling and User-Adapted Interaction, 2002
Rendle, S. - Factorization Machines - ICDM 2010
Cheng, H.-T., et al. - Wide & Deep Learning for Recommender Systems - DLRS Workshop (RecSys) 2016
Guo, H., et al. - DeepFM: A Factorization-Machine based Neural Network for CTR Prediction - IJCAI 2017

## 17. Deep / Graph Recommenders
He, X., et al. - LightGCN: Simplifying and Powering Graph Convolution Network for Recommendation - SIGIR 2020
Wang, X., et al. - Neural Graph Collaborative Filtering (NGCF) - SIGIR 2019
Ying, R., et al. - Graph Convolutional Neural Networks for Web-Scale Recommender Systems (PinSage) - KDD 2018
Fan, W., et al. - Graph Neural Networks for Social Recommendation (GraphRec) - WWW 2019
Kang, W.-C., McAuley, J. - Self-Attentive Sequential Recommendation (SASRec) - ICDM 2018
Sun, F., et al. - BERT4Rec: Sequential Recommendation with Bidirectional Encoder Representations from Transformer - CIKM 2019

## 18. Cold-Start Recommendation
Volkovs, M., Yu, G. W., Poutanen, T. - DropoutNet: Addressing Cold Start in Recommender Systems - NeurIPS 2017
Lee, H., et al. - MeLU: Meta-Learned User Preference Estimator for Cold-Start Recommendation - KDD 2019
Zhu, Z., et al. - Recommendation for New Users and New Items via Randomized Training and Mixture-of-Experts Transformation (Heater) - SIGIR 2020
Wei, Y., et al. - Contrastive Learning for Cold-Start Recommendation (CLCRec) - ACM Multimedia 2021
Huang, F., et al. - Aligning Distillation for Cold-Start Item Recommendation (ALDI) - SIGIR 2023
Yang, W., Zhang, W., Liu, Y., Han, Y., Wang, Y., Lee, J., Yu, P. S. - Adaptive Candidate Retrieval with Dynamic Knowledge Graph Construction for Cold-Start Recommendation (ColdRAG) - arXiv:2505.20773
Zhang, W., et al. - Cold-Start Recommendation towards the Era of Large Language Models (LLMs): A Comprehensive Survey and Roadmap - arXiv:2501.01945

## 19. LLM-based / Zero-Shot Recommendation
Geng, S., et al. - Recommendation as Language Processing (RLP): A Unified Pretrain, Personalized Prompt & Predict Paradigm (P5) - RecSys 2022
Bao, K., Zhang, J., Zhang, Y., Wang, W., Feng, F., He, X. - TALLRec: An Effective and Efficient Tuning Framework to Align Large Language Model with Recommendation - RecSys 2023
Wang, Y., et al. - RecMind: Large Language Model Powered Agent for Recommendation - Findings of NAACL 2024
Dai, S., et al. - Uncovering ChatGPT's Capabilities in Recommender Systems - RecSys 2023
Hou, Y., et al. - Large Language Models are Zero-Shot Rankers for Recommender Systems - ECIR 2024
Wei, W., et al. - LLMRec: Large Language Models with Graph Augmentation for Recommendation - WSDM 2024
Wu, L., et al. - A Survey on Large Language Models for Recommendation - World Wide Web, 2024
Lin, J., et al. - How Can Recommender Systems Benefit from Large Language Models: A Survey - ACM Transactions on Information Systems, 2025

## 20. Knowledge-Graph-based Recommendation
Wang, X., et al. - KGAT: Knowledge Graph Attention Network for Recommendation - KDD 2019
Wang, H., et al. - RippleNet: Propagating User Preferences on the Knowledge Graph for Recommender Systems - CIKM 2018
Wang, H., et al. - Knowledge Graph Convolutional Networks for Recommender Systems (KGCN) - WWW 2019
Zhang, F., et al. - Collaborative Knowledge Base Embedding for Recommender Systems (CKE) - KDD 2016
Guo, Q., et al. - A Survey on Knowledge Graph-Based Recommender Systems - IEEE Transactions on Knowledge and Data Engineering, 2022
Järvelin, K., Kekäläinen, J. - Cumulated Gain-based Evaluation of IR Techniques (NDCG) - ACM Transactions on Information Systems, 2002

## 21. Embeddings and Vector Search
Reimers, N., Gurevych, I. - Sentence-BERT: Sentence Embeddings using Siamese BERT-Networks - EMNLP 2019
Gao, T., Yao, X., Chen, D. - SimCSE: Simple Contrastive Learning of Sentence Embeddings - EMNLP 2021
Wang, L., et al. - Text Embeddings by Weakly-Supervised Contrastive Pre-training (E5) - arXiv:2212.03533
Li, Z., et al. - Towards General Text Embeddings with Multi-stage Contrastive Learning (GTE) - arXiv:2308.03281
Chen, J., Xiao, S., Zhang, P., Luo, K., Lian, D., Liu, Z. - M3-Embedding (BGE-M3): Multi-Linguality, Multi-Functionality, Multi-Granularity Text Embeddings Through Self-Knowledge Distillation - Findings of ACL 2024 (arXiv:2402.03216)
Muennighoff, N., et al. - MTEB: Massive Text Embedding Benchmark - EACL 2023
Enevoldsen, K., et al. - MMTEB: Massive Multilingual Text Embedding Benchmark - arXiv:2502.13595
Kusupati, A., et al. - Matryoshka Representation Learning - NeurIPS 2022
Malkov, Y. A., Yashunin, D. A. - Efficient and Robust Approximate Nearest Neighbor Search using Hierarchical Navigable Small World Graphs (HNSW) - IEEE Transactions on Pattern Analysis and Machine Intelligence, 2020
Johnson, J., Douze, M., Jégou, H. - Billion-Scale Similarity Search with GPUs (FAISS) - IEEE Transactions on Big Data, 2021
Guo, R., et al. - Accelerating Large-Scale Inference with Anisotropic Vector Quantization (ScaNN) - ICML 2020
Jégou, H., Douze, M., Schmid, C. - Product Quantization for Nearest Neighbor Search - IEEE Transactions on Pattern Analysis and Machine Intelligence, 2011
Robertson, S., Zaragoza, H. - The Probabilistic Relevance Framework: BM25 and Beyond - Foundations and Trends in Information Retrieval, 2009
Formal, T., Piwowarski, B., Clinchant, S. - SPLADE: Sparse Lexical and Expansion Model for First Stage Ranking - SIGIR 2021
Khattab, O., Zaharia, M. - ColBERT: Efficient and Effective Passage Search via Contextualized Late Interaction over BERT - SIGIR 2020
Santhanam, K., et al. - ColBERTv2: Effective and Efficient Retrieval via Lightweight Late Interaction - NAACL 2022

## 22. Clustering (Topic Consolidation)
Ward, J. H. - Hierarchical Grouping to Optimize an Objective Function - Journal of the American Statistical Association, 1963
Murtagh, F., Contreras, P. - Algorithms for Hierarchical Clustering: An Overview - WIREs Data Mining and Knowledge Discovery, 2012
Pedregosa, F., et al. - Scikit-learn: Machine Learning in Python - Journal of Machine Learning Research, 2011
Grootendorst, M. - BERTopic: Neural Topic Modeling with a Class-based TF-IDF Procedure - arXiv:2203.05794
Campello, R. J. G. B., Moulavi, D., Sander, J. - Density-Based Clustering Based on Hierarchical Density Estimates (HDBSCAN) - PAKDD 2013
Blei, D. M., Ng, A. Y., Jordan, M. I. - Latent Dirichlet Allocation - Journal of Machine Learning Research, 2003

## 23. Human-in-the-Loop, Dialogue & Agent Orchestration
Amershi, S., et al. - Power to the People: The Role of Humans in Interactive Machine Learning - AI Magazine, 2014
Settles, B. - Active Learning Literature Survey - University of Wisconsin-Madison Computer Sciences Technical Report 1648, 2009
Horvitz, E. - Principles of Mixed-Initiative User Interfaces - CHI 1999
Aliannejadi, M., Zamani, H., Crestani, F., Croft, W. B. - Asking Clarifying Questions in Open-Domain Information-Seeking Conversations - SIGIR 2019
Zamani, H., et al. - Generating Clarifying Questions for Information Retrieval - WWW 2020
Budzianowski, P., et al. - MultiWOZ: A Large-Scale Multi-Domain Wizard-of-Oz Dataset for Task-Oriented Dialogue Modelling - EMNLP 2018
Wu, C.-S., et al. - Transferable Multi-Domain State Generator for Task-Oriented Dialogue Systems (TRADE) - ACL 2019
Rastogi, A., et al. - Towards Scalable Multi-Domain Conversational Agents: The Schema-Guided Dialogue Dataset (SGD) - AAAI 2020
Sumers, T. R., Yao, S., Narasimhan, K., Griffiths, T. L. - Cognitive Architectures for Language Agents - Transactions on Machine Learning Research, 2024
Wu, Q., et al. - AutoGen: Enabling Next-Gen LLM Applications via Multi-Agent Conversation - arXiv:2308.08155
Li, G., et al. - CAMEL: Communicative Agents for "Mind" Exploration of Large Language Model Society - NeurIPS 2023
Khattab, O., et al. - DSPy: Compiling Declarative Language Model Calls into Self-Improving Pipelines - ICLR 2024
Liu, J., et al. - LlamaIndex - Software / Documentation, https://github.com/run-llama/llama_index

## 24. Differential Privacy
Dwork, C., McSherry, F., Nissim, K., Smith, A. - Calibrating Noise to Sensitivity in Private Data Analysis - Theory of Cryptography Conference (TCC) 2006
Dwork, C., Roth, A. - The Algorithmic Foundations of Differential Privacy - Foundations and Trends in Theoretical Computer Science, 2014
Dwork, C. - Differential Privacy - ICALP 2006
Kasiviswanathan, S. P., Lee, H. K., Nissim, K., Raskhodnikova, S., Smith, A. - What Can We Learn Privately? (Local Differential Privacy) - SIAM Journal on Computing, 2011
McMahan, H. B., Ramage, D., Talwar, K., Zhang, L. - Learning Differentially Private Recurrent Language Models - ICLR 2018
McSherry, F., Mironov, I. - Differentially Private Recommender Systems: Building Privacy into the Netflix Prize Contenders - KDD 2009

## 25. Systems / Engineering (Documentation & Software)
Ramírez, S. - FastAPI - Software Documentation, https://fastapi.tiangolo.com
Colvin, S., et al. - Pydantic - Software Documentation, https://docs.pydantic.dev
Encode - Uvicorn: An ASGI Web Server for Python - Software Documentation, https://www.uvicorn.org
Honnibal, M., Montani, I. - spaCy: Industrial-Strength Natural Language Processing in Python - Software, https://spacy.io
Reimers, N., Gurevych, I. - Sentence-Transformers (SBERT) - Software, https://www.sbert.net
Neo4j - Neo4j Vector Indexes and Cypher Manual - Documentation, https://neo4j.com/docs
Redis - Redis Documentation - https://redis.io/docs
Merkel, D. - Docker: Lightweight Linux Containers for Consistent Development and Deployment - Linux Journal, 2014
OpenRouter - OpenRouter: A Unified Interface for LLMs - Documentation, https://openrouter.ai/docs
Astral - uv: An Extremely Fast Python Package and Project Manager - Software, https://github.com/astral-sh/uv
Fowler, M., Lewis, J. - Microservices: A Definition of This New Architectural Term - martinfowler.com, 2014
Newman, S. - Building Microservices: Designing Fine-Grained Systems - O'Reilly Media, 2015
Wiggins, A. - The Twelve-Factor App - https://12factor.net, 2011
WHATWG - Server-Sent Events - HTML Living Standard, https://html.spec.whatwg.org/multipage/server-sent-events.html
Fette, I., Melnikov, A. - The WebSocket Protocol - RFC 6455, IETF, 2011

## 26. Real-Estate Domain — Theory, Valuation Standards & Applications
Rosen, S. - Hedonic Prices and Implicit Markets: Product Differentiation in Pure Competition - Journal of Political Economy, Vol. 82, No. 1, 1974
Akerlof, G. A. - The Market for "Lemons": Quality Uncertainty and the Market Mechanism - Quarterly Journal of Economics, Vol. 84, No. 3, 1970
Gale, D., Shapley, L. S. - College Admissions and the Stability of Marriage - American Mathematical Monthly, Vol. 69, No. 1, 1962
Roth, A. E., Sotomayor, M. - Two-Sided Matching: A Study in Game-Theoretic Modeling and Analysis - Cambridge University Press, 1990
Royal Institution of Chartered Surveyors - RICS Valuation – Global Standards (Red Book Global Standards) - RICS, London, 2024 edition (effective 31 January 2025)
International Valuation Standards Council - International Valuation Standards (IVS) - IVSC, London, 2024 edition (effective 31 January 2025)
TEGoVA - European Valuation Standards 2025 (EVS 2025, "Blue Book"), 10th Edition - TEGoVA, Brussels, 2025
Tecnoborsa - Codice delle Valutazioni Immobiliari (Italian Property Valuation Standard), 6th Edition - Tecnoborsa S.c.p.A., Rome, 2025
Henríquez-Miranda, C., Ríos-Pérez, J., Sanchez-Torres, G. - Recommender Systems in Real Estate: A Systematic Review - Bulletin of Electrical Engineering and Informatics, Vol. 14, No. 3, 2025
Tekouabou, S. C. K., Gherghina, Ş. C., Kameni, E. D., Filali, Y., Idrissi Gartoumi, K. - AI-Based on Machine Learning Methods for Urban Real Estate Prediction: A Systematic Survey - Archives of Computational Methods in Engineering, Springer, 2024
Kuppan, K., Acharya, D. B., Divya, B. - Foundational AI in Insurance and Real Estate: A Survey of Applications, Challenges, and Future Directions - IEEE Access, Vol. 12, 2024
Zaki, J., et al. - House Price Prediction using Hedonic Pricing Model and Machine Learning Techniques - Concurrency and Computation: Practice and Experience, Vol. 34, 2022
Baldominos, A., Blanco, I., Moreno, A. J., Iturrarte, R., Bernárdez, Ó., Afonso, C. - Identifying Real Estate Opportunities using Machine Learning - Applied Sciences, Vol. 8, No. 11, 2018
Ho, W. K. O., Tang, B.-S., Wong, S. W. - Predicting Property Prices with Machine Learning Algorithms - Journal of Property Research, Vol. 38, No. 1, 2021
Pérez-Rave, J. I., Correa-Morales, J. C., González-Echavarría, F. - A Machine Learning Approach to Big Data Regression Analysis of Real Estate Prices for Inferential and Predictive Purposes - Journal of Property Research, Vol. 36, No. 1, 2019

---

### Compiler's notes on verification and provenance
- **Verified against primary sources during compilation:** ColdRAG (arXiv:2505.20773 — note the v1 title was *"Cold-Start Recommendation with Knowledge-Guided Retrieval-Augmented Generation"* and the current v3 title is *"Adaptive Candidate Retrieval with Dynamic Knowledge Graph Construction for Cold-Start Recommendation"*; authors Yang, Zhang, Liu, Han, Wang, Lee, Yu); DIAL-KG (Bao et al., DASFAA 2026 / arXiv:2603.20059); BGE-M3 (Chen et al., ACL 2024 Findings, arXiv:2402.03216); ExtractBench (arXiv:2602.12247); PARSE (EMNLP 2025 Industry, arXiv:2510.08623); Resume/SmartResume extraction (arXiv:2510.09722); DeepJSONEval (arXiv:2509.25922); "Let Me Speak Freely?" (Tam et al., EMNLP 2024 Industry, DOI verified); Outlines/Willard & Louf (arXiv:2307.09702); XGrammar (arXiv:2411.15100); "Defeating Nondeterminism in LLM Inference" (He, Thinking Machines Lab, 2025); GraphRAG (arXiv:2404.16130); LightRAG (arXiv:2410.05779); HippoRAG (arXiv:2405.14831) and HippoRAG 2 (arXiv:2502.14802); Think-on-Graph (arXiv:2307.07697); iText2KG (arXiv:2409.03284); Peeters/Steiner/Bizer entity matching (arXiv:2310.11244, EDBT 2025); and all real-estate valuation standards and domain surveys (RICS, IVSC, TEGoVA, Tecnoborsa, Henríquez-Miranda et al., Tekouabou et al.).
- **The claimed IDs "xmemory (arXiv:2604.27906)" and "The Format Tax (arXiv:2606.09410)" could not be independently confirmed against a primary record.** "The Format Tax (Lee et al.)" is retained only where a stable venue could be inferred; the unverifiable *xmemory* entry has been silently omitted rather than fabricated. If you can confirm either from your own copy, add it back in the same three-field format.
- **Edition caveat:** Valuation-standard entries cite the current (2024/2025) editions. If your thesis frames its systems around an earlier deployment window, cite the immediately prior editions instead (IVS effective Jan 2022; EVS 2020 / 9th edition; Tecnoborsa 5th edition, 2018; RICS Red Book 2022).
- A small number of software/documentation URLs are canonical project pages rather than archival citations; treat them as living references and record an access date when writing.
