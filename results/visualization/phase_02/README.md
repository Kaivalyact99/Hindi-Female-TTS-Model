# 📊 Phase 02 — ML Duration Prediction Visualizations

All visualizations below are generated from the Hindi Female TTS corpus  
using the extracted feature CSV (`hindi_audio_features3.csv`).  
**Dataset:** 4,586 utterances | **Target:** Predict audio duration from text features

---

## 1️⃣ Feature Correlation Heatmap

<img width="515" height="435" alt="01_feature_correlation_heatmap" src="https://github.com/user-attachments/assets/fa411157-9ca3-4914-aa6c-10c889291987" />


### What This Shows
A **correlation matrix** showing the strength of relationship between  
all text features and the target variable `duration`.

### Key Observations

| Feature Pair | Correlation | Interpretation |
|-------------|-------------|----------------|
| `char_count` ↔ `duration` | **0.93** | Very strong — longer text = longer speech |
| `matra_count` ↔ `duration` | **0.76** | Strong — more matras = more syllables |
| `halant_count` ↔ `duration` | **0.42** | Moderate — halants compress sounds |
| `char_count` ↔ `matra_count` | **0.86** | Strong — related features |
| `char_count` ↔ `halant_count` | **0.52** | Moderate relationship |
| `matra_count` ↔ `halant_count` | **0.24** | Weak — largely independent |

### Key Findings
- **`char_count` is the strongest predictor** of duration (r = 0.93)
- `matra_count` is the second best predictor (r = 0.76)
- `halant_count` has moderate influence (r = 0.42) — halants  
  often cause consonant clusters which slightly compress duration
- High correlation between `char_count` and `matra_count` (0.86)  
  suggests potential **multicollinearity** — addressed in modeling

### Why It Matters
This heatmap guided our **feature selection** for the regression models.  
`char_count` was confirmed as the primary predictor before modeling began.

---

## 2️⃣ Feature vs Duration Scatter Plots

<img width="1489" height="390" alt="02_feature_vs_duration_scatter" src="https://github.com/user-attachments/assets/f077c95d-df48-4ea3-8b4f-31aba589ce97" />


### What This Shows
Three scatter plots showing the **individual linear relationship**  
between each text feature and audio duration across all 4,586 samples.

### Plot 1 — `char_count` vs `duration`
- **X-axis:** Character count (0 to ~120)
- **Y-axis:** Duration in seconds (0 to ~13)
- Points follow the red regression line **very closely**
- Confirms strong linear relationship (r = 0.93)
- Most sentences have 20–80 characters, lasting 2–8 seconds
- A few **outliers** visible (very short text, long duration) —  
  likely sentences with complex pronunciation

### Plot 2 — `matra_count` vs `duration`
- **X-axis:** Matra count (0 to ~35)
- **Y-axis:** Duration in seconds
- **Wider spread** around the regression line compared to char_count
- Still shows clear upward trend
- **Fan-shaped spread** — at higher matra counts, duration varies  
  more widely (some speakers extend vowels, some don't)

### Plot 3 — `halant_count` vs `duration`
- **X-axis:** Halant count (0 to ~10)
- **Y-axis:** Duration in seconds
- **Vertical clustering** at each integer halant value —  
  halant is a discrete count, not continuous
- Weakest relationship of the three (r = 0.42)
- Large vertical spread shows halant alone cannot predict duration well
- Halants appear mostly in 0–4 range across the corpus

### Combined Insight
`char_count` alone explains most duration variance.  
`matra_count` adds useful secondary information.  
`halant_count` contributes but has limited standalone predictive power.

---

## 3️⃣ Actual vs Predicted Duration & Residual Plot

<img width="1790" height="590" alt="03_actual_vs_predicted_residuals" src="https://github.com/user-attachments/assets/fa419b5e-deb0-465e-a501-6a68da51f19f" />


### What This Shows
Three diagnostic plots evaluating **how well the linear model performs**  
on the test set.

### Plot 1 (Left Blue) — Training Data Scatter
- Shows the spread of `char_count` vs `duration` in training data
- Used to **visualize the data distribution** before fitting
- Confirms the linear trend is appropriate for this data

### Plot 2 (Middle Green) — Actual vs Predicted Duration
- **X-axis:** Actual duration (seconds) from test set
- **Y-axis:** Model's predicted duration (seconds)
- **Dashed black line** = perfect prediction line (where actual = predicted)
- Points clustered **very close to the diagonal** = excellent predictions
- Minor spread increases at higher durations (above 8s) —  
  longer sentences are slightly harder to predict precisely
- **R² = 0.8928** means the model explains 89.28% of duration variance

### Plot 3 (Right Purple) — Residual Plot
- **X-axis:** Predicted duration
- **Y-axis:** Residuals (actual − predicted)
- **Red dashed line** = zero error (perfect prediction)
- Residuals are **randomly scattered around zero** ✅  
  → confirms the linear model assumptions are satisfied
- No systematic pattern or curve → **no need for higher-order terms**
- Spread is approximately **±1.5 seconds** — acceptable for TTS
- A few outliers beyond ±1.5s — edge cases in the corpus

### Model Quality Summary
| Metric | Value | Interpretation |
|--------|-------|----------------|
| R² Score | 0.8928 | Model explains 89.28% of variance |
| Residual Range | ±1.5s | Most predictions within 1.5 seconds |
| Pattern in Residuals | None | Linear model is appropriate ✅ |

---

## 4️⃣ Model Performance Comparison (Linear vs Polynomial)

<img width="699" height="429" alt="04_model_performance_comparison" src="https://github.com/user-attachments/assets/edc1e706-2bce-4f3d-b7e9-6a24e952c6a3" />


### What This Shows
A **bar chart comparing R² scores** of two regression models:
- **Linear Regression** (3 original features)
- **Polynomial Regression Degree 2** (9 engineered features)

### Key Observations

| Model | Features Used | R² Score | Complexity |
|-------|--------------|----------|------------|
| Linear Regression | 3 | **0.8928** | Low ✅ |
| Polynomial Degree 2 | 9 | **0.8939** | High ❌ |

- Polynomial model adds **6 extra interaction features** but only  
  improves R² by **+0.0011 (~0.1%)**
- The improvement is **statistically negligible**
- Adding complexity without meaningful gain violates  
  **Occam's Razor** in machine learning

### Our Decision
> **Linear model is preferred** for its simplicity, interpretability,  
> and near-identical performance.

### Why This Matters
This comparison demonstrates a key ML principle:  
**more complex ≠ more accurate**.  
For TTS duration prediction with text features,  
a simple linear relationship is sufficient at the ML stage.

---

## 5️⃣ Feature Coefficients — Linear & Polynomial Models

<img width="1242" height="516" alt="05_feature_coefficients_linear_polynomial" src="https://github.com/user-attachments/assets/8fa06155-8e40-4a16-be43-44243610ab87" />


### What This Shows
Two bar charts showing the **learned coefficients** (weights) of each  
feature in both models — revealing what the model actually learned.

### Left Plot — Linear Model Feature Impact

| Feature | Coefficient | Meaning |
|---------|-------------|---------|
| `char_count` | **+0.108** | Each extra character adds **0.108 seconds** |
| `matra_count` | **-0.067** | Each extra matra subtracts **0.067 seconds** |
| `halant_count` | **-0.109** | Each extra halant subtracts **0.109 seconds** |

**Interpretation:**
- `char_count` has the **largest positive impact** — the primary driver
- `matra_count` is **negative** — matras make characters more  
  phonetically efficient (a matra adds sound without adding characters)
- `halant_count` is **most negative** — halants create consonant  
  clusters that are spoken faster (no separate vowel sound)

**Real Example:**  
A sentence with 50 chars, 10 matras, 2 halants:  
`Duration ≈ (50 × 0.108) + (10 × -0.067) + (2 × -0.109) + intercept`  
`≈ 5.4 - 0.67 - 0.218 + intercept ≈ ~4.5 seconds`

### Right Plot — Polynomial Model Feature Interactions

| Feature/Interaction | Coefficient | Meaning |
|--------------------|-------------|---------|
| `char_count` | **+1.34** | Amplified in polynomial space |
| `char × matra` | **-0.36** | Interaction: chars with matras compress duration |
| `matra_count` | **-0.23** | Direct matra effect |
| `halant_count` | **-0.23** | Direct halant effect |
| `char × halant` | **+0.19** | Chars with halants slightly extend duration |

**Key Insight:**  
The **interaction term `char × matra`** (coefficient = -0.36) is the  
most interesting — it shows that sentences with **many characters AND  
many matras** tend to be spoken more efficiently (shorter duration).  
This makes linguistic sense in Hindi phonology.

### Combined Conclusion
Both models confirm the same core finding:  
**Character count is the dominant predictor of Hindi speech duration.**  
Matras and halants act as **correction factors** that fine-tune the estimate.

---

## 📋 Phase 02 Complete Summary

| # | Visualization | Purpose | Key Finding |
|---|--------------|---------|-------------|
| 1 | Correlation Heatmap | Feature selection | char_count strongest (r=0.93) |
| 2 | Feature vs Duration Scatter | Relationship analysis | Linear trend confirmed |
| 3 | Actual vs Predicted + Residuals | Model evaluation | R²=0.8928, residuals random |
| 4 | Model Comparison | Model selection | Linear preferred over Polynomial |
| 5 | Feature Coefficients | Interpretability | Each char adds 0.108s to duration |

---

## 🏆 Final Model Selected
```
Model:     Linear Regression
Features:  char_count, matra_count, halant_count
R² Score:  0.8928
Formula:   duration = 0.108×char + (-0.067×matra) + (-0.109×halant) + intercept
```

---

## 🔧 How These Were Generated

All plots generated using Python:
- `pandas` — data loading and manipulation  
- `scikit-learn` — Linear and Polynomial Regression  
- `matplotlib` / `seaborn` — visualization  
- `numpy` — numerical computations  

See full code in:  
📓 [`notebooks/phase_02_duration_prediction/predicting_hindi_speech_duration.ipynb`](../../../notebooks/phase_02_duration_prediction/)
