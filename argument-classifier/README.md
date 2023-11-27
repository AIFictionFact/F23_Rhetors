# Source Code

### Dependencies
* PyTorch
* transformers library
* tqdm library


**To run inference:**

You can run trained LogBERT on your own statement-claim pairs under `/src/`.
```
python main_logbert_infer.py -logic nli senti normarg -data input.csv -out output.csv -model ../logs/sup-kialo/sup_blend-20231126_142451-DTkialo-TYnormative-BWup-TSmain+nli+normarg_conseq_senti+normarg_jtype+normarg_norm_senti+normarg_polar+senti-BTno.model -cuda 0
```
 - `[INPUT_CSV_PATH]`: An input csv file should have three columns: (1) `pairid` - a unique ID for each pair, (2) `text_from` - statement or premise, (3) `text_to` - claim or hypothesis.
 - `[OUTPUT_CSV_PATH]`: The output csv will contain five columns: (1) `id` - pair ID, (2) `con_text` - text_to, (3) `pre_text` - text_from, (4) `label_prop` - probability scores of labels [support, attack, neutral], (5) `label_pred` - label with the highest probability score. 
 - `[LOGBERT_MODEL_PATH]` should be a LogBERT model, and can be downloaded [here](https://drive.google.com/file/d/1NrinALrs8lQ2CZj1IIPkTHBqWmR6FFoF/view?usp=sharing)

The script runs inference and writes the results for every 50,000 rows internally (to prevent loading too many instances all at once).


