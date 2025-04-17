#   LLMs for SQL Generation

The following repo for our Graduation project it  contains files to Finetune and Evaluate an LLM for Text to SQL tasks. We see a 2x improvement in ROGUE-1 and ROGUE-L scores and a 3x improvement in ROGUE-2 scores from fine-tuning. Also we found great improvements in Exact Match accuarcy and Execution Accuracy from fine -tunning against base model  These big ROGUE performance improvements demonstrate the value of fine-tuning (see figure below).

<p align="center">
  <img src="ROGUE_Scores_Llama_vs_Finetune.png" alt="Text2SQL Evaluation Results" width="900"/>
</p>

In this project we used the ROGUE scores ,Exact Match and Execution Accurcy for evaluation and we realize that  better approach (metric) is to run queries against a reference database to validate and evaluate results 

The datset used for this project is the b-mc2/sql-create-context dataset available on the Hugging Face Hub. The model is trained using ~4K examples. Evaluation is done with ~450 test data examples that were not used during training.

The files in the repo do the following:

Text2SQL_Data_preprocessing.ipynb (CPU) -This notebook Removes repeated question-SQL pairs to avoid data leakage(Duplicate Removal), we do implicit Table Filter: Drops samples where the SQL query's table is not explicitly mentioned in the question — ensures the model learns realistic mappings and avoids hallucinations,Train/Test Split + Formatting: Splits the dataset (~4K samples) into training and test sets, formats them using an instruction-response template.
Text2SQL_FineTune_Llama2GPTQv3.ipynb (GPU Needed) - Finetunes LLama2GPTQ Model using training data. Takes ~20mins.
Text2SQL_Evaluate_Llama2GPTQv3.ipynb (GPU Needed) - Runs Inference on test data using the LLama2GPTQ Model. Takes ~40mins.
Text2SQL_Evaluate_Llama2GPTQFineTunev3.ipynb (GPU Needed) - Runs Inference on test data using the Finetuned LLama2GPTQ Model. Takes ~40mins.
Text2SQL_Compare_ROGUEv3.ipynb (CPU) - Computes ROGUE-1, ROGUE-2, ROUGE-L Scores for both Pre & Post Finetune Models.
Text2SQL_HFUpload_Llama2GPTQFineTunev3.ipynb (GPU Needed) - Uploads Finetuned Model to HF Hub (WIP)
---



