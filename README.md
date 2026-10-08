# A generative-informed neuro-symbolic framework for syntactic ambiguity resolution: Evidence from Arabic DPs

[![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/MShormani/arabert-noun-attachment/blob/main/arabert_noun_attachment.ipynb)
![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

Fine-tuning AraBERT (`aubmindlab/bert-base-arabertv02`) for Arabic structural noun-attachment disambiguation using a human-annotated gold corpus.

---

## 📌 Overview

This project implements a sequence classification pipeline for resolving $N_1$ vs. $N_2$ noun-attachment ambiguities in Arabic sentences. The pipeline combines AraBERT with `ArabertPreprocessor` and `Farasa` preprocessing, representing each instance using the sentence and its candidate attachment heads.

### Core Capabilities

* **Text Normalization & Preprocessing:** Arabic text preprocessing using `ArabertPreprocessor` and `Farasa`.

* **Structured Input Representation:** Formats each instance as:

  ```text
  Input = S [SEP] N1: cN1 [SEP] N2: cN2
  ```

* **Classification:** AraBERT-based sequence classification for predicting the correct attachment as $N_1$ or $N_2$.

* **Evaluation:** Computes Accuracy, Precision, Recall, Binary F1, Weighted F1, classification reports, and confusion matrices.

* **Test-Sample Inference:** Provides a separate notebook for applying the fine-tuned AraBERT model to a user-provided `test_sample.xlsx` file and comparing predictions against human gold annotations.

---

## 📁 Repository Structure

```text
.
├── arabert_noun_attachment.ipynb          # Main training and evaluation notebook
├── test_sample_inference.ipynb            # Test-sample inference and evaluation notebook
├── training_dataset.xlsx                  # Human-annotated training dataset
├── valid_dataset.xlsx                     # Human-annotated validation dataset
├── eval_dataset.xlsx                      # Human-annotated evaluation dataset
├── requirements.txt                       # Project dependencies
├── LICENSE-MIT                            # Code license
├── LICENSE-CC-BY-4.0                     # Data and documentation license
└── README.md                              # Project documentation
```

---

## 🚀 Quick Start

### 1. Install Dependencies

Install the required Python packages using `pip`:

```bash
pip install -r requirements.txt
```

Main libraries used in this project include:

* `transformers`
* `datasets`
* `arabert`
* `farasa`
* `pyarabic`
* `torch`
* `scikit-learn`
* `pandas`
* `openpyxl`

### 2. Dataset Format

The project expects Excel (`.xlsx`) files containing the following primary columns:

| **Column**              | **Description**                              | **Example**                     |
| ----------------------- | -------------------------------------------- | ------------------------------- |
| `sentence`              | Full context sentence in Arabic              | `اعتمدت على كتاب الطالب الكبير` |
| `head_N1`               | First candidate attachment head ($N_1$)      | `كتاب`                          |
| `complement_N2`         | Second candidate attachment head ($N_2$)     | `الطالب`                        |
| `human_gold_attachment` | Ground-truth attachment label (`N1` or `N2`) | `N1`                            |

> **Note:** The pipeline checks for `human_gold_attachment` as the ground-truth label and falls back to `attachment` if `human_gold_attachment` is not found.

Additional dataset fields may be present and are retained as metadata where applicable.

### 3. Training and Evaluation

Open `arabert_noun_attachment.ipynb` in Google Colab or JupyterLab and run the cells sequentially.

The main notebook performs the following steps:

1. **Upload Datasets:** Upload `training_dataset.xlsx`, `valid_dataset.xlsx`, and `eval_dataset.xlsx` when prompted.
2. **Preprocessing:** Normalize and preprocess Arabic text using `ArabertPreprocessor` and Farasa.
3. **Sequence Formatting:** Construct the structured input representation containing the sentence and the two candidate attachment heads.
4. **Model Training:** Fine-tune AraBERT using the Hugging Face `Trainer`.
5. **Evaluation:** Evaluate the fine-tuned model on the evaluation dataset and generate detailed classification results.

### 4. Test-Sample Inference

The repository also provides a separate notebook for testing the trained model on a separate Excel file:

```text
test_sample.xlsx
```

Open `test_sample_inference.ipynb` in Google Colab and upload `test_sample.xlsx` when prompted.

The notebook:

1. Loads the test sample.
2. Applies the same Arabic preprocessing used by the model.
3. Formats the input using the same $N_1$/$N_2$ representation.
4. Loads the **fine-tuned AraBERT model** from the Hugging Face model repository:
   `MShormani/arabert-noun-attachment`
5. Predicts the attachment class for each instance.
6. Compares predictions against `human_gold_attachment`.
7. Reports Accuracy, Precision, Recall, Binary F1, Weighted F1, a classification report, and a confusion matrix.

The `test_sample.xlsx` file is intended as an independent user-provided test sample and does not need to be included in the repository.

---

## 📊 Evaluation Metrics

The pipeline outputs standard evaluation measures:

* **Accuracy**
* **Precision**
* **Recall**
* **Binary F1**
* **Weighted F1**
* **Per-class Performance ($N_1$ vs. $N_2$)**
* **Classification Report**
* **Confusion Matrix**

---

## ⚙️ Model Details

| **Parameter**               | **Setting**                             |
| --------------------------- | --------------------------------------- |
| **Base Model**              | `aubmindlab/bert-base-arabertv02`       |
| **Fine-tuned Model**        | `MShormani/arabert-noun-attachment`     |
| **Learning Rate**           | `2e-5`                                  |
| **Batch Size**              | `32`                                    |
| **Epochs**                  | `4`                                     |
| **Maximum Sequence Length** | `128`                                   |
| **Random Seed**             | `42`                                    |
| **Framework**               | Hugging Face `Transformers` / `Trainer` |

---

## 🔄 Reproducibility

The repository includes the training, validation, and evaluation datasets, the main training/evaluation notebook, the test-sample inference notebook, and the required dependencies to facilitate reproduction of the reported experiments and application of the fine-tuned model to additional test samples.

The training and evaluation workflow uses a fixed random seed (`42`) and a maximum sequence length of `128` tokens.

---

## 📄 License

* **Code & Notebook:** [MIT License](LICENSE-MIT)
* **Dataset & Documentation:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE-CC-BY-4.0)

The code and notebooks are distributed under the MIT License. The dataset and documentation are distributed under the CC BY 4.0 license.
