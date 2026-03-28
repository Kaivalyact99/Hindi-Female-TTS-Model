# 🎙️ Hindi Female TTS — Duration Prediction using Machine Learning

> Predicting speech duration from Hindi text using acoustic features and 
> traditional machine learning. Built on a 10-hour studio-quality 
> Hindi female speech corpus (4,586 utterances).

![Python](https://img.shields.io/badge/Python-3.8+-blue.svg)
![License](https://img.shields.io/badge/License-MIT-green.svg)
![Phase](https://img.shields.io/badge/Phase-02%20Complete-brightgreen)
![Dataset](https://img.shields.io/badge/Dataset-4586%20Files-orange)

---

## 📌 Project Overview

This project explores **Text-to-Speech (TTS) duration modeling** for Hindi 
using a studio-quality female voice corpus. We extract linguistic and 
acoustic features from text and audio, then train machine learning models 
to predict how long a spoken Hindi sentence will be.

**Current Focus:** Traditional Machine Learning (Phase 01 & 02)  
**Future Scope:** Deep Learning — Acoustic Models, Neural TTS (Phase 03+)

---

## 🗃️ Dataset

| Property | Details |
|----------|---------|
| Source | [AI4Bharat / IndiaAI AiKosh](https://aikosh.indiaai.gov.in/web/datasets/details/hindi_female_mono_indictts_phase3.html) |
| Total Files | 4,586 `.wav` audio files |
| Total Duration | ~10 hours |
| Language | Hindi (Standard) |
| Speaker | Single Female, Monolingual |
| Recording | Studio Quality |
| Sampling Rate | 48,000 Hz (48 kHz) |
| Bit Depth | 16-bit |
| Channels | Mono |

### Feature CSV Columns

| Column | Description |
|--------|-------------|
| `filename` | Audio file index |
| `hindi_transcript` | Raw Hindi sentence |
| `char_count` | Total character count |
| `word_count` | Number of words |
| `matra_count` | Count of matras (vowel diacritics) |
| `halant_count` | Count of halant characters |
| `avg_word_len` | Average word length |
| `duration` | **Target variable** — audio duration (seconds) |

> ⚠️ Audio files are NOT stored in this repo due to size (~10 GB).  
> See [`data/raw/README.md`](data/raw/README.md) for download instructions.

---

## 🔬 Project Phases

### ✅ Phase 01 — Dataset Description & Audio Signal Processing
- Dataset overview and exploratory data analysis
- Waveform, spectrogram, MFCCs visualization
- Distribution analysis of duration, character counts, word counts
- 📓 [View Notebook](notebooks/phase_01_eda_signal_processing/)
- 📄 [View Report & Presentation](docs/phase_01/)

### ✅ Phase 02 — Predicting Hindi Speech Duration from Text (ML)
- Feature engineering from Hindi text
- Models trained: Linear Regression, Random Forest, XGBoost, SVR
- Evaluation metrics: MAE, RMSE, R²
- 📓 [View Notebook](notebooks/phase_02_duration_prediction/)
- 📄 [View Report & Presentation](docs/phase_02/)

### 🔜 Phase 03 — Deep Learning (Coming Soon)
- Sequence-to-sequence duration models
- Transformer-based prediction
- End-to-end Neural TTS exploration

---

## 📊 Results Summary (Phase 02)

| Model | MAE (s) | RMSE (s) | R² |
|-------|---------|----------|-----|
| Linear Regression | — | — | — |
| Random Forest | — | — | — |
| XGBoost | — | — | — |
| SVR | — | — | — |

---

## ⚙️ Installation
```bash
git clone https://github.com/YOUR_USERNAME/hindi-female-tts-ml.git
cd hindi-female-tts-ml
pip install -r requirements.txt
```

---

## 🚀 Usage
```bash
# Phase 01
jupyter notebook notebooks/phase_01_eda_signal_processing/

# Phase 02
jupyter notebook notebooks/phase_02_duration_prediction/
```

---

## 👥 Contributors

| Name | Role |
|------|------|
| Your Name | Feature Engineering, ML Modeling |
| Friend Name | Audio Processing, Signal Analysis |
| Friend Name | Dataset Collection, Documentation |

---

## 🗺️ Roadmap

- [x] Phase 01: Dataset EDA & Audio Signal Processing
- [x] Phase 02: ML-based Duration Prediction  
- [ ] Phase 03: Deep Learning Duration Modeling
- [ ] Phase 04: End-to-End Neural TTS
- [ ] Phase 05: Web Demo / Deployment

---

## 📄 License

MIT License — see [LICENSE](LICENSE)  
Dataset from [AI4Bharat IndiaAI AiKosh](https://aikosh.indiaai.gov.in)
```

4. Scroll down → **"Commit changes"** (green button)
5. In the popup, write commit message: `docs: add complete README`
6. Click **"Commit changes"**

---

### 📄 File 2: requirements.txt

**Add file → Create new file** → name it `requirements.txt`
```
# Core Data Science
numpy>=1.21.0
pandas>=1.3.0
scikit-learn>=1.0.0

# Audio Processing
librosa>=0.9.0
soundfile>=0.10.3
scipy>=1.7.0

# Visualization
matplotlib>=3.4.0
seaborn>=0.11.0

# Notebooks
jupyter>=1.0.0
ipykernel>=6.0.0

# ML Models
xgboost>=1.5.0

# Utilities
tqdm>=4.62.0
regex>=2021.8.3
