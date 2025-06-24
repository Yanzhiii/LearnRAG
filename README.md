# LearnRAG

A lightweight retrieval-augmented learning assistant that pairs classical (BM25) and neural (ChromaDB) retrieval with compact LLMs, LoRA fine-tuning and chain-of-thought (CoT) reasoning.

---

## Colab Notebook

Interactive demo: **[Open in Colab](YOUR_COLAB_LINK_HERE)**


---

## Roadmap

- **Basic working process in Colab Notebook – done**  
- **Finetuning scripts – done, pending upload**  
- **Vector database integration – planned**  
- **Evaluation – planned**

---

## Abstract
This project builds a chatbot that helps students explore topics such as machine learning, deep learning and natural-language processing.  
Using a Retrieval-Augmented Generation (RAG) framework, the system retrieves external context instead of fine-tuning the base model directly. Three pipelines are implemented:

1. **V1** – BM25 + TinyLlama-1.1B-Chat baseline (RAG / non-RAG prompt styles).  
2. **V2** – ChromaDB vector retriever + LLaMA-3.2-3B-Instruct (4-bit).  
3. **V3** – V2 + LoRA fine-tuning and chat-style CoT prompts.

---

## Methodology

### Pipeline Architectures
![Figure 1 – Pipeline overview](docs/img/pipeline_overview.png)

### Dataset Construction Workflow
![Figure 2 – Dataset creation workflow](docs/img/dataset_creation_workflow.png)

### Prompt Templates
![Figure 4 – Prompt structures](docs/img/prompt_templates.png)

### Language Model Fine-tuning
Fine-tuning follows the **RAFT** recipe: for each knowledge chunk, three GPT-generated queries and CoT answers are created; three distractor chunks are injected to teach the model to ignore noise.  
LoRA rank 8, α = 16, 10 epochs; checkpoint from epoch 3 is used once loss ≈ 0.4.  
Core libraries: Hugging Face *Transformers*, *PEFT*, *TRL*.

---

## References

- Zhang T. *et al.* “RAFT: Adapting Language Model to Domain-Specific RAG”, 2024.  
- **Gorilla** dataset & tools – <https://github.com/ShishirPatil/gorilla>  
- Hu E. *et al.* “LoRA: Low-Rank Adaptation of Large Language Models”, 2021.
