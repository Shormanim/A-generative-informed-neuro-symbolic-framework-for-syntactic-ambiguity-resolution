# A generative-informed neuro-symbolic framework for syntactic ambiguity resolution: Evidence from Arabic DPs

![Python 3.8+](https://img.shields.io/badge/python-3.8%2B-blue.svg)
![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)

Fine-tuning AraBERT (`aubmindlab/bert-base-arabertv02`) for Arabic structural noun-attachment disambiguation using a human-annotated gold corpus.

---

## 📌 Overview

This project implements a sequence classification pipeline for resolving $N_1$ vs. $N_2$ noun-attachment ambiguities in Arabic sentences. The pipeline combines AraBERT with `ArabertPreprocessor` and `Farasa` preprocessing, representing each instance using the sentence and its candidate attachment heads.

### Core Capabilities

* **Text Normalization & Preprocessing:** Arabic text preprocessing using `ArabertPreprocessor` and `Farasa`.

* **Structured Input Representation:** Each instance is formatted as:

  ```text
  Input = S [SEP] N1: cN1 [SEP] N2: cN2
  ```

* **Classification:** AraBERT-based sequence classification for predicting the correct attachment as $N_1$ or $N_2$.

---

## 📁 Repository Structure

```text
.
├── arabert_noun_attachment.ipynb   # Main inference and evaluation notebook
├── training_dataset.xlsx           # Human-annotated training dataset
├── valid_dataset.xlsx              # Human-annotated validation dataset
├── eval_dataset.xlsx               # Human-annotated evaluation dataset
├── requirements.txt                # Project dependencies
├── LICENSE-MIT                     # Code license
├── LICENSE-CC-BY-4.0              # Data and documentation license
└── README.md                       # Project documentation
```

---

## 🚀 Quick Start

### 1. Install Dependencies

Install the required Python packages using `pip`:

```bash
pip install -r requirements.txt
```

### 2. Run the Notebook

Open `arabert_noun_attachment.ipynb` in Google Colab or JupyterLab and run the cells sequentially.

The notebook:

1. Loads a user-provided `test_sample.xlsx` file.
2. Preprocesses the Arabic text using `ArabertPreprocessor` and Farasa.
3. Constructs the structured $N_1$/$N_2$ input representation.
4. Loads the fine-tuned AraBERT model from Hugging Face:
   `MShormani/arabert-noun-attachment`
5. Predicts the attachment class ($N_1$ or $N_2$).
6. Compares predictions with human gold annotations.
7. Reports standard classification metrics and a confusion matrix.

---

## 📊 Dataset Format

The input Excel (`.xlsx`) files use the following primary fields:

| **Column**              | **Description**                                              | **Example**                     |
| ----------------------- | ------------------------------------------------------------ | ------------------------------- |
| `sentence`              | Full context sentence in Arabic                              | `اعتمدت على كتاب الطالب الكبير` |
| `head_N1`               | First candidate attachment head ($N_1$)                      | `كتاب`                          |
| `complement_N2`         | Second candidate attachment head ($N_2$)                     | `الطالب`                        |
| `human_gold_attachment` | Human-annotated ground-truth attachment label (`N1` or `N2`) | `N1`                            |

The training, validation, and evaluation datasets are included in the repository. For independent testing, users can provide their own `test_sample.xlsx` file following the same structure.

---

## 📊 Evaluation Metrics

The notebook reports:

* **Accuracy**
* **Precision**
* **Recall**
* **Binary F1**
* **Weighted F1**
* **Per-class performance ($N_1$ vs. $N_2$)**
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

The repository provides the training, validation, and evaluation datasets, the inference and evaluation notebook, and the required software dependencies. The fine-tuned model is available through its Hugging Face repository, allowing the trained model to be independently evaluated on additional test samples.

---

## 📄 License

* **Code & Notebook:** [MIT License](LICENSE-MIT)
* **Dataset & Documentation:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE-CC-BY-4.0)
