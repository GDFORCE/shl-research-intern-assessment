---

# Research Internship Hiring Assessment – Final Submission

This repository contains my final submission for a **research internship hiring assessment**.
The solution addresses **spoken grammar evaluation** by explicitly modeling discrepancies between noisy and smoothed ASR transcripts.

---

## 📌 Core Idea

The model jointly analyzes:

* **Raw transcript** (faithful to speaker errors)
* **Smoothed transcript** (ASR-corrected version)

By contrasting both views, the system separates **true grammatical errors** from **automatic speech recognition noise**.

> Example:
> Raw: *“I goes to school”*
> Smooth: *“I went to school”*
> → Identified as a **grammar error**, not transcription noise.

---

## 🛠️ System Architecture

The pipeline combines **Whisper-based transcription** with a **Transformer-based regression model**.
graph TD
    A[Raw Audio Files]
    B[Whisper Small]
    C[Whisper Medium]

    A --> B
    A --> C

    B --> D[Raw Transcript - Noisy]
    C --> E[Smoothed Transcript - Corrected]

    D --> F[Concatenation]
    E --> F

    F --> G[Dual Input Text]
    G --> H[RoBERTa Base Encoder]
    H --> I[Mean Pooling Layer]
    I --> J[Regression Head]
    J --> K[Final Score 0 to 5]

---

## 🔑 Key Technical Decisions

* **Dual-ASR Strategy:**
  Uses Whisper Small and Whisper Medium to preserve error contrast.

* **Backbone Model:**
  `roberta-base`, selected for robustness under noisy token distributions.

* **Pooling Method:**
  **Mean Pooling** instead of `[CLS]` to capture full-sentence semantics.

* **Training Setup:**

  * 5-Fold Cross-Validation
  * 5 Epochs
  * Batch Size: 4

---

## 📂 Repository Structure

```text
├── finalsubmission.ipynb    # Complete end-to-end training & inference notebook
├── README.md               # Documentation
└── requirements.txt        # Dependencies (auto-managed in notebook)
```

---

## ⚙️ Robust Execution Logic

The notebook implements a **Smart Fallback Mechanism**:

1. Checks for pre-generated transcription files.
2. If unavailable, automatically:

   * Downloads Whisper models
   * Generates transcriptions from raw audio
3. Proceeds with training and inference without manual intervention.

This ensures **reproducibility across environments**.

---

## 🚀 How to Run

The notebook is self-contained and designed for **Kaggle or Google Colab** environments.

### Prerequisites

* Python 3.10+
* GPU (P100 or T4 recommended)
* Internet access (only required for initial model downloads)

### Execution

Run all cells sequentially in `finalsubmission.ipynb`.

The notebook automatically:

1. Removes conflicting libraries to free GPU memory
2. Installs required dependencies
3. Downloads models (if missing)
4. Performs transcription (if required)
5. Trains the model
6. Generates `submission.csv`

---

## 📊 Focus Areas

* Natural Language Processing
* Speech & Audio Processing
* Transformer-based Deep Learning
* Regression Modeling

---

## 📎 Notes

* The notebook **matches the evaluated submission**.
* Designed for **clarity, robustness, and reproducibility**.

---

