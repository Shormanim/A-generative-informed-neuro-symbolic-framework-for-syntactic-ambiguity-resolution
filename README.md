# A generative-informed neuro-symbolic framework for syntactic ambiguity resolution: Evidence from Arabic DPs

Fine-tuning AraBERT (`aubmindlab/bert-base-arabertv02`) for Arabic structural noun-attachment disambiguation using a human-annotated gold corpus.

---

## 📌 Overview

This project implements a sequence classification pipeline for resolving $N_1$ vs. $N_2$ noun-attachment ambiguities in Arabic sentences. The pipeline combines AraBERT with `ArabertPreprocessor` and `Farasa` preprocessing, representing each instance using the sentence and its candidate attachment heads.

### Core Capabilities

* **Text Normalization & Preprocessing:** Arabic text preprocessing using `ArabertPreprocessor` and `Farasa`.
* **Structured Input Representation:** Formats input candidates as:

```text
[sentence] [SEP] N1: [head_N1] [SEP] N2: [complement_N2]
```

* **Classification:** AraBERT-based sequence classification.
* **Evaluation:** Computes Accuracy, Precision, Recall, Binary F1, Weighted F1, classification reports, and confusion matrices.

---

## 📁 Repository Structure

```text
.
├── arabert_noun_attachment.ipynb   # Main training and evaluation notebook
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

Main libraries used in this project include:

* `transformers`
* `datasets`
* `arabert`
* `farasa`
* `pyarabic`
* `torch`
* `scikit-learn`
* `pandas`

### 2. Dataset Format

The project expects Excel (`.xlsx`) files containing the following primary columns:

| **Column**              | **Description**                               | **Example**                     |
| ----------------------- | --------------------------------------------- | ------------------------------- |
| `sentence`              | Full context sentence in Arabic               | `اعتمدت على كتاب الطالب الكبير` |
| `head_N1`               | First candidate attachment head ($N_1$)       | `كتاب`                          |
| `complement_N2`         | Second candidate attachment head ($N_2$)      | `الطالب`                        |
| `human_gold_attachment` | Ground-truth attachment label (`N1` or `N2`)* | `N1`                            |

> **Note:** The pipeline automatically looks for `human_gold_attachment` as the ground-truth label, with a fallback to `attachment` if `human_gold_attachment` is not found.

### 3. Running the Pipeline

Open `arabert_noun_attachment.ipynb` in Google Colab or JupyterLab and run all cells sequentially:

1. **Upload Datasets:** Upload `training_dataset.xlsx`, `valid_dataset.xlsx`, and `eval_dataset.xlsx` when prompted.
2. **Preprocessing:** Normalize and preprocess Arabic text using `ArabertPreprocessor`.
3. **Sequence Formatting:** Construct structured input sequences.
4. **Model Training:** Fine-tune AraBERT using the Hugging Face `Trainer`.
5. **Evaluation:** Evaluate performance on the evaluation dataset and view detailed classification reports.

---

## 📊 Evaluation Metrics

The pipeline outputs standard evaluation measures:

* **Accuracy**
* **Precision & Recall**
* **Binary F1 & Weighted F1**
* **Per-class Performance ($N_1$ vs. $N_2$)**
* **Classification Report & Confusion Matrix**

---

## ⚙️ Model Details

| **Parameter**     | **Setting**                             |
| ----------------- | --------------------------------------- |
| **Base Model**    | `aubmindlab/bert-base-arabertv02`       |
| **Learning Rate** | `2e-5`                                  |
| **Batch Size**    | `32`                                    |
| **Epochs**        | `4`                                     |
| **Random Seed**   | `42`                                    |
| **Framework**     | Hugging Face `Transformers` / `Trainer` |

---

## 🔄 Reproducibility

The repository includes the training, validation, and evaluation datasets, the main Jupyter notebook, and the required dependencies to facilitate full reproduction of the experiments.

---

## 📄 License

* **Code & Notebook:** [MIT License](LICENSE-MIT)
* **Dataset & Documentation:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE-CC-BY-4.0)

The code and notebook are distributed under the MIT License. The dataset and documentation are distributed under the CC BY 4.0 license.
