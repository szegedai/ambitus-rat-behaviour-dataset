
# 🧪 Ambitus Rat Behaviour Dataset

This repository provides access to a large-scale, multi-generational dataset collected using the **Ambitus behavioural testing protocol** in rats. The dataset enables the analysis of exploratory behaviour, motivation, learning, and cognitive flexibility in rodent models over time, including **transgenerational trends**.

---

## 🧬 What is the Ambitus Protocol?

The **Ambitus test** is a high-throughput behavioural paradigm developed to assess:

- 🧭 **Exploration**: how actively and persistently animals explore new environments  
- 🎯 **Motivation**: latency and engagement in goal-directed tasks  
- 🧠 **Learning capacity**: ability to adapt to reinforcement structures  
- 🔄 **Cognitive control**: trade-offs between exploration and exploitation across trials  

Each rat performs multiple trials in a sensor-equipped arena with controlled stimuli and reward feedback. The setup allows detailed, repeatable measurements and enables robust cross-generational comparisons.

---

## 📊 What's in the Dataset?

- **Subjects**: 1100+ rats across 14 generations  
- **Groups**: Lisket (experimental) vs. LE (control)  
- **Collected via**: Ambitus platform, using motion sensors and automated data capture  
- **Duration**: Multi-year experimental campaign with consistent protocol  
- **Structure**:
  - **Raw data**: Trial-level, time-stamped metrics (parquet format)
  - **Processed data**: One-row-per-rat behavioral summaries (CSV)

### 🧠 Feature Types

- Total locomotion and exploration
- Pre- and post-reward zone entries and durations
- Learning efficiency and strategy ratios
- Trial-by-trial behaviour dynamics
- Metadata: sex, generation, year, weight, box, paradigm, group

---

## 📂 Repository Structure

```
.
├── raw/                      # Original data files (.parquet)
├── processed/                # Cleaned, ML-ready datasets (.csv)
├── notebooks/
│   ├── base_stats.ipynb           # Descriptive stats, correlation plots, distributions
│   ├── cleaner.ipynb              # Converts raw to ML-ready one-row-per-rat format
│   ├── ml_playground.ipynb        # Supervised classification (Group prediction)
│   ├── anova_playground.ipynb     # Factorial ANOVA: Group × Sex × Year
│   └── technical_validation.ipynb # Missingness, variance, ICCs
├── utils/                    # Optional helpers
└── README.md
```

---

## 🔧 How to Use

1. Clone the repo:
   ```bash
   git clone https://github.com/szegedai/ambitus-rat-behaviour-datase.git
   cd ambitus-rat-behaviour-datase
   ```

2. Open and explore notebooks in `/notebooks`:
   - Statistical analysis (`anova_playground`, `base_stats`)
   - Data cleaning (`cleaner.ipynb`)
   - ML experiments (`ml_playground.ipynb`)

3. Clean your own version:
   ```python
   from cleaner import make_rat_one_row
   ```

---

## 📁 Outputs

- `ambitus_0_15_ml_ready_*.csv` – Flattened, clean per-subject dataset  
- `feature_missingness.csv`, `fig_missing_bar.pdf` – Completeness reports  
- `gen_drift_spearman.csv` – Generational drift correlations  
- `fig_drift_heatmap.pdf`, `fig_drift_lineplot.pdf` – Trend visualizations  

---

## 📜 Citation

If you use this dataset in your research, please cite:

> **Kőrösi G. et al.** *Transgenerational profiling of rat behaviour using the Ambitus protocol*.  
> Nature Scientific Data (in review / forthcoming).

---

## 📬 Contact

For questions or collaboration:
- 📧 korosi.gabor [at] inf.u-szeged.hu  
- 🏫 University of Szeged – Institute of Informatics

---

## 🧠 Keywords

`rat behaviour`, `ambitus`, `multi-generational`, `exploration`, `motivation`, `learning`, `neuroscience`, `machine learning`, `ANOVA`, `phenotyping`
