# Mobile Price Classification

Predict mobile phone **price range** (0 = Low, 1 = Medium, 2 = High, 3 = Very High) from device specs.

This repo contains two notebooks:
- `Mobile_price.ipynb` — original version using **Logistic Regression**, **Decision Tree**, **k‑NN**.
- `RF__Mobile_price_updated.ipynb` — updated version where **Decision Tree** is swapped with **Random Forest** (plus the same LR & k‑NN).

Both notebooks train on **all 20 features** from `train.csv`. A post‑analysis section (in the RF notebook variant with Top‑15 cells) reports **feature importance** and optionally extracts a **Top‑15** feature list (analysis only).

---

## 🚀 Quick Start

1. **Clone** and enter the repo
```bash
git clone <your-repo-url>.git
cd <your-repo-name>
```

2. **Install deps**
```bash
pip install -r requirements.txt
```

3. **Add data**
Place the Kaggle dataset files in the repo root:
```
train.csv
test.csv
```

4. **Run notebooks**
Open Jupyter and run either notebook end‑to‑end:
```bash
jupyter notebook
# then open Mobile_price.ipynb OR RF__Mobile_price_updated.ipynb
```

---

## 📦 Data

Dataset: **Mobile Price Classification** (Kaggle).  
Target: `price_range` (0‑3) — balanced across classes.  
Features (20): battery_power, blue, clock_speed, dual_sim, fc, four_g, int_memory, m_dep, mobile_wt, n_cores, pc, px_height, px_width, ram, sc_h, sc_w, talk_time, three_g, touch_screen, wifi.

---

## 🧠 Models

- **Logistic Regression** (scaled features)
- **Decision Tree** (trees do not require scaling) — *original notebook only*
- **Random Forest** (swap‑in for Decision Tree) — *updated notebook*
- **k‑Nearest Neighbors** (scaled features)

**Train/Test Split:** 80/20 with `random_state=42` and stratification.

---

## ✅ Results (on held‑out test set)
From the run captured in the conversation:
- **Logistic Regression** — Accuracy: **0.975** (best, strong precision/recall across classes)
- **Random Forest** — Accuracy: **0.8925**
- **Decision Tree** — Accuracy: **0.8325**
- **k‑NN** — Accuracy: **0.53**

> Confusion matrices and classification reports are produced by the notebooks.

---

## 🔍 Feature Importance & Top‑15 (Analysis Only)
The RF notebook includes a section *after* the confusion matrices that:
- Confirms the **20 features** used.
- Plots **impurity‑based** importances (`rf_model.feature_importances_`).
- Computes **Permutation Importance** on the test set (model‑agnostic).
- Prints the **Top‑15** list and (optionally) compares accuracy using only those features.

Why this matters:
- Helps justify why features like **RAM** and **battery_power** are important.
- Demonstrates that removing redundant/low‑signal features can retain accuracy (or even slightly improve it), though training remains on all 20 for the main results.

---

## 🗂️ Repo Structure

```
.
├── Mobile_price.ipynb
├── RF__Mobile_price_updated.ipynb
├── train.csv                # add locally (not tracked in git by default)
├── test.csv                 # add locally (not tracked in git by default)
├── requirements.txt
├── README.md
└── .gitignore
```

---

## 🔁 Reproducibility

- Fixed seeds where applicable (`random_state=42`).
- Scaling with `StandardScaler` for LR and k‑NN uses **training‑only fit**, then transforms test data (no leakage).

---

## 📜 License

This project is released under the **MIT License** (see `LICENSE`).

---

## 🙌 Acknowledgements

- Kaggle: Mobile Price Classification dataset.
- scikit‑learn, pandas, numpy, matplotlib, seaborn.
