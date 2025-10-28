## OmniReasoner: A Multi-Agent Framework for Transparent, Multimodal, Tool-Augmented Reasoning with Retrieval Guidance

### 1. Overview and Goal

**OmniReasoner** is a research project designed to address the challenges of factual consistency and hallucination in Large Language Models ($\text{LLMs}$) when tackling complex, knowledge-intensive questions. It operates as a multi-agent framework intended to deliver a complete, transparent, and verifiable reasoning pipeline, which is currently a shortcoming of market-ready systems. The primary focus is on enhancing Knowledge Graph Question Answering ($\text{KGQA}$) through a novel, structured inference process.

### 2. Core Methodology

The project's innovation is centered on two key strategies:

* **Chain-of-Thought Enhanced Knowledge Rewriting ($\text{CoTKR}$):** This method moves beyond single-step knowledge rewriting by generating a high-quality knowledge representation. It iteratively generates **reasoning traces** interleaved with knowledge **summaries**, ensuring the final **Enhanced Rewritten Knowledge** is semantically coherent with the question and filters out irrelevant information. This step provides a logical organization that aligns with the question's reasoning path.
* **Preference Alignment from Question Answering Feedback ($\text{PAQAF}$):** This is a training strategy used to optimize the knowledge rewriter by leveraging feedback from the downstream $\text{QA}$ model. $\text{PAQAF}$ evaluates the quality of different knowledge representations based on the corresponding responses from the $\text{QA}$ model to construct preference pairs, which are then used to fine-tune the rewriter.

### 3. System Architecture and Workflow

The system is built on a modular, multi-agent design with a pipeline that sequentially processes a user's complex query.

1.  **Retrieval Module:** Upon receiving a **Complex Question**, this module searches the comprehensive **Knowledge Graph ($\text{KG}$)** to extract the most relevant information, outputting an **Initial Subgraph** of related triples.
2.  **Knowledge Rewriting Module:** The Initial Subgraph is transformed using the **CoTKR** approach. It alternatively conducts:
    * **Reasoning:** Decomposing the question and generating a reasoning trace to identify needed knowledge.
    * **Summarization:** Summarizing the relevant knowledge from the subgraph based on the reasoning trace.
3.  **Prompt Augmentation and Answer Generation:** The resulting **Enhanced Rewritten Knowledge** is used to augment the prompt for the **Answer Generation Module**. A powerful **LLM** (e.g., Llama-3 or Mistral) then synthesizes the final, verifiable **Answer** by leveraging the structured context.

![swimlane1 (1)](https://github.com/user-attachments/assets/1ddf46e0-c287-4e68-ad95-8f2906947feb)

### 4. Dependencies and Research Context

The project's rigorous evaluation and implementation are anchored in established $\text{KGQA}$ benchmarks and resources:

* **Knowledge Graph:** Freebase.
* **Datasets:** The system is trained and evaluated using the challenging multi-hop $\text{KGQA}$ datasets, $\text{GrailQA}$ and $\text{GraphQuestions}$.
* **Large Language Models (LLMs):** The framework utilizes modern, high-performing $\text{LLMs}$ such as $\text{Llama-3}$ and $\text{Mistral}$ (e.g., $\text{Llama-3-8B-Instruct}$ and $\text{Mistral-7B-Instruct v0.3}$) for the knowledge rewriting and final question answering stages.
* **Training Foundation:** $\text{CoTKR}$ is initially mastered through supervised fine-tuning using knowledge representations distilled from powerful models like $\text{ChatGPT}$.
