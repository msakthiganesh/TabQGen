This repository hosts the code for the paper "Answer-Aware Question Generation from Tabular and Textual Data using T5".

In this project, we converted [ToTTo](https://github.com/google-research-datasets/ToTTo) to **TabQGen**(Question Generation Dataset for Tables). This is done mainly in 2 steps - 

  1. Creating a Multi-Type Question Generator from Text using [SQUAD](https://rajpurkar.github.io/SQuAD-explorer/) and [BoolQ](https://github.com/google-research-datasets/boolean-questions) datasets.
  2. Applying Multi-Type Question Generator to [ToTTo](https://github.com/google-research-datasets/ToTTo) descriptions and generate questions for each of them. The resulting augmented ToTTo dataset is named as **TabQGen**.

For detailed approach of our end-to-end pipeline and our findings, kindly refer our paper.

**TabQGen** datasets can be found [here](https://github.com/saichandrapandraju/TabQGen/blob/main/datasets/README.md)

# Reproducing our work:

We implemented our entire pipeline with interactive Jupyter notebooks and to reproduce our work, here are the sequential notebooks to run:

  1. **TextQGen.ipynb** creates the Multi-Type Question Generator from Text -> requires you to download [SQUAD](https://rajpurkar.github.io/SQuAD-explorer/) and [BoolQ](https://github.com/google-research-datasets/boolean-questions) datasets.
  2. **TabQgen_dataset_creation.ipynb** applies Multi-Type Question Generator to [ToTTo](https://github.com/google-research-datasets/ToTTo) descriptions which results TabQGen dataset. **language** folder is taken from [this](https://github.com/google-research/language) repo of [Google Research](https://github.com/google-research) for processing [ToTTo](https://github.com/google-research-datasets/ToTTo) data. This step outputs two types of datasets - raw TabQGen dataset which follows similar strucure as ToTTo and processed TabQGen dataset which contains questions(labels) and processed sub-table data using **language** repo. These can be found in [**datasets**](https://github.com/saichandrapandraju/TabQGen/tree/main/datasets) folder.
  3. **T5_[small | base | large]_tabqgen** folders contain files for training and testing respective T5 variant using **TabQGen** and follow same structure as follows - 
      * t5_[small | base | large]_train.ipynb -> train T5 variant with TabQGen and saves trained model in 'table_qgen' directory
      * t5_[small | base | large]_test.ipynb -> test the model in previous and saves predictions in 'test_preds.txt' file.
      * t5_[small | base | large]_scoring.ipynb -> takes the predicted results in previous step and calculates different scores as mentioned in the paper.

**Models trained on TabQGen were uploaded to [HuggingFace models](https://huggingface.co/models) and can be found in below links:** 

t5_small -> https://huggingface.co/saichandrapandraju/t5_small_tabqgen

t5_base -> https://huggingface.co/saichandrapandraju/t5_base_tabqgen

t5_large -> https://huggingface.co/saichandrapandraju/t5_large_tabqgen
