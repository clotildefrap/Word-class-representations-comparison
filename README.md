# Word-class-representations-comparison


This repository contains the work done for a project aiming at extracting the embeddings of different categories of words, with the primary intent being the comparison of the representations of function VS content words, extracted from three different layers (2, 8, 24) in two twenty-four layer models (BERT and GPT2).


## Data

The data used in this implementation comes from the study done by Breithaupt, F., Otenen, E., Wright, D.R. et al. entitled "Humans create more novelty than ChatGPT when asked to retell a story" which investigates the differences in creativity in story retellings produced by ChatGPT3 and human retellers hired on Amazon Mechanical Turk (AMT). https://doi.org/10.1038/s41598-023-50229-7
The file containing the data is open source and was easily downloaded. It consists in a dataframe containing the original stories used to obtain the retellings, the retellings by the model and the retellings by the human participants. In total, there are 156 stories, and three retellings of each type (model and human), thus 936 retellings, and 1092 stories in total including the original version.

All seven versions of each stories were extracted and stored along with their retellers and their common ID. The code is available in this repository. 

## Tokenizers

Each of the stories was tokenized using the English SpaCy tokenizer, the BPE tokenizer of GPT2 and the Word-Piece tokenizer of the BERT model.

## Models and process

The models used to conduct the experiment, "GPT2-medium" and "bert-large-uncased", are open-source twenty-four layer pretrained models whose codes are available on Hugging Face (https://huggingface.co/openai-community/gpt2-medium ; https://huggingface.co/google-bert/bert-large-uncased). The models were loaded and fed the stories one by one ; the hidden states of the layers of interest (2, 8, 24) were extracted and stored with their corresponding tokens and token IDs. 3D PCA was fitted on the data, which was then visualised (see plots below). The tokens obtained from the SpaCy tokenizer were systematically compared to the tokens produced by the tokenizers of GPT2 and BERT and the ones that did not match (we call them "misaligned tokens") were identified and stored. Using a Mahalanobis distance function that we adapt from https://www.geeksforgeeks.org/python/how-to-calculate-mahalanobis-distance-in-python/, we identify and flag the outliers, and check if they crrespond to the misaligned tokens.


## Code

The code is available is this repository and had been designed to be reproducible and adaptable. 



## Plots

All the plots were created using the Plotly library and are interactive. They are available in the repository and can be called individually through the index page. The names are under the format : "gpt_layer24_story_156_Retell_3_Human.html", "bert_layer24_story_156_Retell_3_Human.html".

