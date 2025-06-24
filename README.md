# LearnRAG

A lightweight retrieval-augmented learning assistant that combines BM25/ChromaDB retrieval with TinyLlama & LLaMA-3 back-ends, LoRA fine-tuning and chain-of-thought reasoning.

## Abstract
This project builds a chatbot to assist students with topics in machine learning, deep learning and natural-language processing. Using a Retrieval-Augmented Generation (RAG) framework, the system retrieves context instead of fine-tuning the base model directly. Three pipelines are implemented: (1) a BM25 + TinyLlama baseline; (2) a ChromaDB retriever with LLaMA-3.2-3B-Instruct; and (3) a LoRA-fine-tuned variant that injects chain-of-thought reasoning.

## Methodology

### Pipeline Architectures
| Version | Retriever | LLM | Notes |
|---------|-----------|-----|-------|
| **V1** | BM25 | TinyLlama-1.1B-Chat | Fast prototype, two prompt styles (RAG / non-RAG) |
| **V2** | ChromaDB (vector) | LLaMA-3.2-3B-Instruct (4-bit) | Higher recall, smaller GPU memory |
| **V3** | ChromaDB | V2 LLM + LoRA | Prompts rewritten to chat-style tags; LoRA heads on q/k/v/o projections |

### Language Model Fine-tuning
Fine-tuning follows the **RAFT** recipe: for each knowledge chunk, three GPT-generated queries and chain-of-thought answers are created; three distractor chunks are injected to teach the model to ignore noise. LoRA rank 8, α = 16, trained 10 epochs; checkpoint at epoch 3 selected once loss ≈ 0.4. Core libs: HuggingFace Transformers, PEFT, TRL.

## References
- Zhang T. *et al.*, “RAFT: Adapting Language Model to Domain Specific RAG”, 2024.  
- **Gorilla** Dataset & Tools, <https://github.com/ShishirPatil/gorilla>  
- Hu E. *et al.*, “LoRA: Low-Rank Adaptation of Large Language Models”, 2021.  
