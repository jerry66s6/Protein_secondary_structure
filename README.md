# Protein Secondary Structure Prediction with ESM2

This repository provides an end-to-end pipeline to fine-tune a small ESM2 model for **per-residue secondary structure prediction**. It covers data processing, training, inference, and deployment details.

## 1. Task & Motivation

* **Task:** Given a protein amino acid sequence, predict the secondary structure label (`H`, `E`, `C`) for each residue.
* **Model:** Fine-tuned `facebook/esm2_t6_8M_UR50D` with a token classification head (Linear layer + Softmax + Cross-Entropy loss).
* **Motivation:** To demonstrate a complete workflow:
    1.  Ingesting raw FASTA + Label files.
    2.  Fine-tuning a Pre-trained Language Model。
    3.  Generating predictions for a test set.
    4.  Deploying as an online API/Demo.

## 2. Data Format

The pipeline requires three main files. You can adapt the scripts to your own data by ensuring your files match the formats below.

### 2.1 Sequences (`sequences.fasta`)

Standard FASTA format containing the full amino acid sequences.

“>3JRN
MVLSEGEWQLVLHVWAKVEADVAGHGQDILIRLFK...”

“>3KVH
EVQLVESGGGLVQPGGSLRLSCAASGFTFSSYAM...”

* **Note:** The string after `>` is the **Protein ID** (e.g., `3JRN`). This ID is used as the key to look up sequences during training and inference.

### 2.2 Training Labels (`train.tsv`)

A tab-separated file containing labeled residues.

id	secondary_structure

3JRN_LYS_8	H

3JRN_LEU_9	H

3JRN_SER_10	C



## 3. Performance

The model achieves 70% accuracy in prediction

## 4. Deployed Model & Demo

The trained model and a demonstration app are available on Hugging Face.

* **Model Weights:**
    https://huggingface.co/Jerry1030/esm2-secstruct-tokencls

* **Online Demo & API:**
    https://huggingface.co/spaces/Jerry1030/esm2-secstruct-pred

    > **Space Features:**
    > * Wraps the model in a FastAPI application.
    > * Provides a web UI for inputting sequences and visualizing structure predictions.
    > * Includes a dashboard showing usage stats (daily API calls).
