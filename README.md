# Efficient LLM Fine-Tuning for Code Generation

A comparative study and implementation of **Parameter-Efficient Fine-Tuning (PEFT)** strategies versus full-parameter tuning for code generation tasks. This project adapts **GPT-2 (124M)** to generate functional Python code using the **CodeXGlue** dataset, optimizing for inference and training efficiency in resource-constrained environments.

📄 **[Read the Full Technical Milestone Report (PDF)](https://github.com/MridulTailor/llm-codegen-lora-finetuning/blob/main/Milestone_Report.pdf)**

## 🚀 Project Overview

Standard fine-tuning of Large Language Models (LLMs) is computationally expensive. This project implements **Low-Rank Adaptation (LoRA)** to democratize access to state-of-the-art code generation. By freezing the pre-trained model weights and injecting trainable rank-decomposition matrices, we aim to achieve comparable performance to full fine-tuning with a fraction of the trainable parameters.

### Key Objectives

  * **Efficiency:** Implement LoRA to reduce GPU VRAM usage and training time.
  * **Functional Correctness:** Move beyond textual metrics (BLEU/ROUGE) by implementing an **Execution Pass Rate** pipeline that actually runs generated code.
  * **Scalability:** Data processing pipelines handling the 250k+ sample CodeXGlue (Python) dataset.

## 📊 Key Results

We established a rigorous evaluation baseline using a custom pipeline that measures both semantic similarity and functional execution.

| Metric | Baseline (Full Fine-Tune) | LoRA (PEFT) |
| :--- | :--- | :--- |
| **Execution Pass Rate** | **39.58%** | *Pending final run* |
| **BLEU Score** | 17.03 | *Pending final run* |
| **ROUGE-L (F1)** | 0.444 | *Pending final run* |

> *Note: Baseline achieved after 3 epochs on a 10k sample subset. See the [Full Report](https://www.google.com/search?q=./Milestone_Report.pdf) for detailed analysis.*

## 🛠️ System Architecture

### 1\. Data Pipeline

  * **Source:** `google/code_x_glue_ct_code_to_text` (Python subset).
  * **Preprocessing:** Tokenization and formatting into `Prompt: [docstring] Code: [code]` pairs.

### 2\. Training Configuration

  * **Model:** GPT-2 (124M parameters).
  * **Technique:** Comparison of Full Fine-Tuning vs. LoRA (Low-Rank Adaptation).
  * **Frameworks:** PyTorch, Hugging Face Transformers, PEFT library.

### 3\. Evaluation Pipeline

Unlike standard NLP tasks, code generation requires functional verification. We built a custom evaluation script that:

1.  Takes a docstring prompt.
2.  Generates code using the fine-tuned model.
3.  **Executes the code** in a sandboxed environment against unit tests.
4.  Calculates the **Execution Pass Rate** (percentage of generated code that runs successfully).

## 🚀 Future Enhancements

Based on our initial findings and baseline performance, the following roadmap is planned to improve model robustness and usability:

  * **Scaling to Full Dataset:** Expand training from the 10,000-sample subset to the full **251,000-sample** CodeXGlue dataset to significantly boost functional correctness and generalization.
  * **LoRA vs. Full Fine-Tune Benchmarking:** Conduct a final direct comparison of resource usage (VRAM, training time) to quantify the efficiency gains of the LoRA implementation.
  * **Hybrid Evaluation Analysis:** Perform a deep analysis of the trade-off between textual similarity (BLEU) and functional correctness (Execution Rate), as preliminary results suggest these metrics are not always perfectly correlated.
  * **Assistant Interface:** Develop a CLI or basic web interface to allow real-time user interaction with the debugging assistant.

## 📂 Repository Structure

```text
├── plots/                     # Visualizations of loss curves and pass rates
│   ├── execution_pass_plot.png
│   └── bleu_rouge_plot.png
├── Efficient_Codegen.ipynb    # Complete pipeline: Data Prep, Training, and Evaluation
├── Milestone_Report.pdf       # Detailed technical findings and methodology
└── README.md
```

## 👥 Contributors

  * **Mridul Tailor**
  * Mayank Vyas
  * Savankumar Pethani
  * Vacha Patel
  * Charu Sneha Laguduva Ravi

*Arizona State University - School of Computing and Augmented Intelligence*
