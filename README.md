#   LLMs for SQL Generation

The following repo for our Graduation project it  contains files to Finetune and Evaluate an LLM for Text to SQL tasks. We see a 2x improvement in ROGUE-1 and ROGUE-L scores and a 3x improvement in ROGUE-2 scores from fine-tuning. Also we found great improvements in Exact Match accuarcy and Execution Accuracy from fine -tunning against base model  These big ROGUE performance improvements demonstrate the value of fine-tuning (see figure below).

<p align="center">
  <img src="ROGUE_Scores_Llama_vs_Finetune.png" alt="Text2SQL Evaluation Results" width="900"/>
</p>

In this project we used the ROGUE scores ,Exact Match and Execution Accurcy for evaluation and we realize that  better approach (metric) is to run queries against a reference database to validate and evaluate results 

The datset used for this project is the b-mc2/sql-create-context dataset available on the Hugging Face Hub. The model is trained using ~4K examples. Evaluation is done with ~450 test data examples that were not used during training.

The files in the repo do the following:

- Text2SQL Data pre-processing.ipynb (CPU):
-This notebook Removes repeated question-SQL pairs to avoid data leakage(Duplicate Removal), we do implicit Table Filter: Drops samples where the SQL query's table is not explicitly mentioned in the question — ensures the model learns realistic mappings and avoids hallucinations,Train/Test Split + Formatting: Splits the dataset (~4K samples) into training and test sets, formats them using an instruction-response template.

- Text2SQL_FineTune_Llama2GPTQv3.ipynb (GPU Needed) :
here we Finetunes the LLaMA2  model using the training dataset with parameter efficient fine-tuning via QLoRA (adapter weights) — a lightweight technique that enables training on consumer GPUs.
After training, we perform inference on sample questions from the test set.The model’s generated SQL is very close to the ground truth responses — confirming that it successfully learned the task

-Text2SQL FineTuned_V3.ipynb (GPU Needed) :
here we re-Finetune  the LLaMA2  model again using the training dataset with parameter efficient fine-tuning via QLoRA (adapter weights) but we change the Lora configration training arguements (ex: increasing training time > max_steps= 510) After the training again , we perform inference on sample questions from the test set.The model’s generated SQL is exactly close to the ground truth responses — confirming that it successfully learned the task very well also the inference time the model taken become much smaller than the last time .

Text2SQL_Evaluate_Llama2GPTQv3.ipynb (GPU Needed) - Runs Inference on test data using the LLama2GPTQ Model. Takes ~40mins.

Text2SQL_Evaluate_Llama2GPTQFineTunev3.ipynb (GPU Needed) - Runs Inference on test data using the Finetuned LLama2GPTQ Model. Takes ~40mins.

Text2SQL_Compare_ROGUEv3.ipynb (CPU) - Computes ROGUE-1, ROGUE-2, ROUGE-L Scores for both Pre & Post Finetune Models.
Text2SQL_HFUpload_Llama2GPTQFineTunev3.ipynb (GPU Needed) - Uploads Finetuned Model to HF Hub (WIP)

---



