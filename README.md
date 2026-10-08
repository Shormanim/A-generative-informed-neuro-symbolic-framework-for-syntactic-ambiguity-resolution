# A generative-informed neuro-symbolic framework for syntactic ambiguity resolution: Evidence from Arabic DPs

# A Generative-Informed Neuro-Symbolic Framework for Syntactic Ambiguity Resolution: Evidence from Arabic DPs

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

* **Test-Sample Evaluation:** Applies the fine-tuned AraBERT model to a sample dataset (`test_sample.xlsx`) and compares model predictions against human gold annotations.

* **Detailed Metrics:** Computes Accuracy, Precision, Recall, Binary F1, Weighted F1, classification reports, and confusion matrices.

---

## 📁 Repository Structure

```text
.
├── arabert_noun_attachment.ipynb   # Main inference and evaluation notebook
├── test_sample.xlsx                # Sample evaluation dataset for quick testing
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
* `openpyxl`

### 2. Dataset Format

The project expects Excel (`.xlsx`) files containing the following primary columns:

| **Column**              | **Description**                              | **Example**                     |
| ----------------------- | -------------------------------------------- | ------------------------------- |
| `sentence`              | Full context sentence in Arabic              | `اعتمدت على كتاب الطالب الكبير` |
| `head_N1`               | First candidate attachment head ($N_1$)      | `كتاب`                          |
| `complement_N2`         | Second candidate attachment head ($N_2$)     | `الطالب`                        |
| `human_gold_attachment` | Ground-truth attachment label (`N1` or `N2`) | `N1`                            |

### 3. Running Inference & Evaluation

Open `arabert_noun_attachment.ipynb` in Google Colab or JupyterLab and run the cells sequentially:

1. **Upload Dataset:** Upload `test_sample.xlsx` when prompted.
2. **Preprocessing:** Normalize Arabic text using `ArabertPreprocessor` and Farasa.
3. **Sequence Formatting:** Construct structured input representations using the $N_1$/$N_2$ candidate format.
4. **Load Fine-Tuned Model:** Automatically load the fine-tuned AraBERT model from Hugging Face (`MShormani/arabert-noun-attachment`).
5. **Inference:** Predict the attachment class ($N_1$ or $N_2$) for each instance.
6. **Evaluation:** Compare predictions against human gold annotations and output Accuracy, Precision, Recall, Binary F1, Weighted F1, classification reports, and a confusion matrix.

---

## 📊 Evaluation Metrics

The pipeline outputs standard evaluation measures:

* **Accuracy**
* **Precision & Recall**
* **Binary F1 & Weighted F1**
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

The repository includes all dataset partitions (`training`, `validation`, and `evaluation`), a dedicated `test_sample.xlsx` for rapid verification, the main notebook, and the required dependencies. The fine-tuned model is referenced through its Hugging Face repository to facilitate reproducibility and independent testing.

---

## 📄 License

* **Code & Notebook:** [MIT License](LICENSE-MIT)
* **Dataset & Documentation:** [Creative Commons Attribution 4.0 International (CC BY 4.0)](LICENSE-CC-BY-4.0)

The code and notebook are distributed under the MIT License. The dataset and documentation are distributed under the CC BY 4.0 license.
