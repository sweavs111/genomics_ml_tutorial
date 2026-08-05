# Checkpoint: Genomics ML Tutorial
**Saved:** Module 1, mid-section 1.4

---

## 1. Tutorial Name & Goal
**Tutorial:** Machine Learning for Genomics (custom, Claude-guided)  
**Goal:** Predict whether a yeast (*S. cerevisiae*) gene is highly expressed based on its promoter sequence. Binary classification problem using promoter sequences as input features.

---

## 2. Steps Completed
1. Set up Python virtual environment and installed required packages (Mac/VS Code)
2. Verified environment with `verify_setup.ipynb` — all packages green
3. Generated synthetic dataset (1000 promoter sequences, 200bp, with planted TATA boxes)
4. Loaded FASTA and TSV files using BioPython and pandas
5. Built per-gene dataframe with `gc_content`, `tata_present`, and `seq_length` columns
6. Completed EDA: mean GC by class (Q1), TATA box fraction by class (Q2), GC histogram (Q3)

---

## 3. Key Code & Config

**Environment setup (Mac):**
```bash
python3 -m venv venv
source venv/bin/activate
pip install numpy pandas scikit-learn matplotlib seaborn biopython jupyter ipykernel
```

**Data generation (locked in, seed=42):**
```python
rng = np.random.default_rng(seed=42)
N_GENES = 1000
PROMOTER_LENGTH = 200
TATA_BOX = "TATAAA"
```

**Feature computation one-liners:**
```python
gc_content = (seq.count("C") + seq.count("G")) / len(seq)
tata_present = 1 if "TATAAA" in seq else 0
seq_length = len(seq)
```

**EDA code:**
```python
# Q1 - mean GC by class
avg_gc = df.groupby('label')['gc_content'].mean()

# Q2 - TATA fraction by class
fraction_tata = df.groupby('label')['tata_present'].mean()

# Q3 - GC histogram
sns.histplot(data=df, x="gc_content", hue="label")
```

---

## 4. Decisions & Deviations
- Used **synthetic data** instead of real SGD/GEO download (URLs were placeholder)
- Promoter length set to **200bp** (real yeast promoters ~1000bp) for speed
- Helper functions `tataSearch()` and `percGC()` were refactored to one-liners after code review

---

## 5. Current State
- **Working:** full data pipeline from generation → dataframe → EDA plots
- **Pending:** interpretation questions for Q1/Q2/Q3 not yet answered (biological sanity check against data generator parameters)
- **Minor fix needed:** Q2 print label says "fraction high expression" but now shows both classes

---

## 6. Next Step
Answer the three interpretation questions (do numbers match data generator expectations? why is the orange distribution left-shifted?), then move on to **feature engineering and one-hot encoding** (the main event of Module 1).
