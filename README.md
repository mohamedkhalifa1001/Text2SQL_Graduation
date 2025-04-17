#  TEXT2SQL: Fine-tune & Evaluate LLMs for SQL Generation

This repository enables you to **fine-tune and evaluate a Language Model (LLM)** for **Text-to-SQL** tasks using real-world SQL data. Fine-tuning significantly boosts performance — showing up to **2x improvement in ROUGE-1 and ROUGE-L**, and **3x in ROUGE-2** scores.

> These gains highlight the real value of fine-tuning LLMs for structured query generation.

---

## Project Overview

This project uses the [`b-mc2/sql-create-context`](https://huggingface.co/datasets/b-mc2/sql-create-context) dataset from Hugging Face, containing ~4K training examples and ~450 held-out test cases. Evaluation is based on ROUGE metrics (though real execution-based evaluation is a **Work in Progress**).

---

### 📷 Example Output

<p align="center">
  <img src="ROGUE_Scores_Llama_vs_Finetune.png" alt="Text2SQL Evaluation Results" width="600"/>
</p>

---

##  Repository Contents

| Notebook | Description | Requirements |
|----------|-------------|--------------|
| `0_Text2SQL_Create_Datav3.ipynb` | Prepares training and test datasets. | 💻 CPU |
| `1_Text2SQL_FineTune_Llama2GPTQv3.ipynb` | Fine-tunes the LLama2-GPTQ model on training data (~20 mins). | ⚡ GPU |
| `2a_Text2SQL_Evaluate_Llama2GPTQv3.ipynb` | Runs inference using the **base model** on test data (~40 mins). | ⚡ GPU |
| `2b_Text2SQL_Evaluate_Llama2GPTQFineTunev3.ipynb` | Runs inference using the **fine-tuned model** (~40 mins). | ⚡ GPU |
| `2c_Text2SQL_Compare_ROGUEv3.ipynb` | Computes ROUGE-1, ROUGE-2, and ROUGE-L scores for base vs fine-tuned model. | 💻 CPU |
| `3_Text2SQL_HFUpload_Llama2GPTQFineTunev3.ipynb` | Uploads your fine-tuned model to the Hugging Face Hub (**Work in Progress**). | ⚡ GPU |

---

##  Evaluation Strategy

Currently, model outputs are evaluated using **ROUGE metrics**. However, we recommend implementing a **database-execution-based evaluation** for more accurate validation of SQL generation (coming soon 🚧).

---



