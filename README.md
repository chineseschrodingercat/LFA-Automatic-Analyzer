# 🧬 LFA Automatic Analyzer: High-Throughput Quantification for Lateral Flow Assays

[![Streamlit App](https://static.streamlit.io/badges/streamlit_badge_black_white.svg)](https://streamlit.io)
[![Python 3.8+](https://img.shields.io/badge/python-3.8+-blue.svg)](https://www.python.org/downloads/release/python-380/)
[![License: GPL v3](https://img.shields.io/badge/License-GPLv3-blue.svg)](https://www.gnu.org/licenses/gpl-3.0)

## 📌 Overview
The **LFA Automatic Analyzer** is a robust, research-grade bioinformatics tool designed to automate the quantification of Lateral Flow Assay (LFA) strips. Unlike subjective visual interpretation, this tool leverages **Computer Vision** and **Signal Processing** algorithms to extract precise **Test/Control (T/C) ratios**, enabling quantitative analysis for applications ranging from clinical diagnostics (e.g., hCG) to toxicology (e.g., Xylazine detection).

This platform features an interactive **Streamlit** interface, allowing researchers to process batch datasets or individual biological samples with real-time visualization of signal profiles.

## ✨ Key Technical Features

### 1. Robust Signal Processing Pipeline
* **Auto-Orientation & Segmentation:** Algorithms automatically detect strip boundaries and correct orientation for consistent profiling.
* **Background Detrending (Baseline Correction):** Implements a **polynomial fitting algorithm** to remove membrane background noise (e.g., "smiling effects" or uneven lighting), ensuring a flat global baseline for integration.
* **Adaptive Smoothing:** Utilizes **Savitzky-Golay filters** to reduce high-frequency sensor noise while preserving the integrity of peak morphology.

### 2. Dual-Mode Workflow
* **📂 High-Throughput Batch Mode:** Process hundreds of pre-cropped strip images simultaneously, exporting a consolidated Excel report with Pivot Tables for statistical analysis.
* **✂️ Interactive Single-Image Mode:** Upload a raw photo of a multi-strip board. The integrated ROI selector allows users to define active zones, and the system automatically slices and analyzes each strip individually.

### 3. Advanced Peak Integration
* **Dynamic Assay Sensitivity:**
    * *Traditional Mode:* High sensitivity (`prominence=0.5`) for detecting faint positives.
    * *Competitive Mode:* High specificity (`prominence=1.8`) for analyzing competitive inhibition assays (e.g., small molecule detection).
* **Global Baseline Integration:** Calculates Area Under the Curve (AUC) using a unified baseline floor anchored to the signal minima, preventing bias in T/C ratio calculations.

## 🛠️ Installation & Usage

### Prerequisites
* Python 3.8+
* `pip` package manager

### Quick Start
1.  **Clone the repository:**
    ```bash
    git clone [https://github.com/YourUsername/LFA-Automatic-Analyzer.git](https://github.com/YourUsername/LFA-Automatic-Analyzer.git)
    cd LFA-Automatic-Analyzer
    ```

2.  **Install dependencies:**
    ```bash
    pip install -r requirements.txt
    ```

3.  **Launch the Dashboard:**
    ```bash
    streamlit run app.py
    ```
    The application will automatically open in your default browser at `http://localhost:8501`.

## ⚙️ Algorithmic Configuration
Researchers can fine-tune the following parameters in `app.py` to adapt to different membrane materials:

| Parameter | Default | Description |
| :--- | :--- | :--- |
| `SMOOTH_WINDOW` | `15` | Window length for Savitzky-Golay filtering. Increase for noisy nitrocellulose membranes. |
| `BASELINE_METHOD` | `'lower'` | Strategy for baseline anchoring (`'lower'` recommended for maximum sensitivity). |
| `T_DIST_NEAR` | `30` | Minimum pixel distance upstream from Control line to define the Test zone. |

## 📊 Outputs
* **Structured Data:** `Summary_Analysis.xlsx` containing raw and adjusted T/C ratios.
* **Visualization:** High-resolution plots (`.png`) for every processed strip, showing the raw signal, fitted baseline, and integration boundaries.

## 🤝 Contribution
Developed by **Minhao Liu** (Lead Developer).
* **Algorithm Design:** Signal processing logic and T/C quantification.
* **UI/UX:** Streamlit dashboard implementation.

**Acknowledgment:**
* **Pu Sun** (Technical Contributor): Contributed to the conceptual design of the processing pipeline and provided insights for code refinement.
