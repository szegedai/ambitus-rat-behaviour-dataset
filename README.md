
# Ambitus Rat Behaviour Dataset

This repository provides access to a large-scale, multi-generational dataset collected using the **Ambitus behavioural testing protocol** in rats. The dataset enables the analysis of exploratory behaviour, motivation, learning, and cognitive flexibility in rodent models over time, including **transgenerational trends**.

[![Binder](https://mybinder.org/badge_logo.svg)](
  https://mybinder.org/v2/gh/szegedai/ambitus-rat-behaviour-dataset/master?labpath=notebooks%2Ftechnical_validation.ipynb
)
[![Open In Colab](
  https://colab.research.google.com/assets/colab-badge.svg)](
  https://colab.research.google.com/github/szegedai/ambitus-rat-behaviour-dataset/blob/master/notebooks/technical_validation.ipynb
)


---

## What is the Ambitus Protocol?

The **Ambitus test** is a high-throughput behavioural paradigm developed to assess:

- **Exploration**: how actively and persistently animals explore new environments  
- **Motivation**: latency and engagement in goal-directed tasks  
- **Learning capacity**: ability to adapt to reinforcement structures  
- **Cognitive control**: trade-offs between exploration and exploitation across trials  

Each rat performs multiple trials in a sensor-equipped arena with controlled stimuli and reward feedback. The setup allows detailed, repeatable measurements and enables robust cross-generational comparisons.

---

## What's in the Dataset?

- **Subjects**: 1100+ rats across 16 generations (2012 – 2019). 
- **Groups**: Lisket (experimental) vs. LE (control)  
- **Collected via**: Ambitus platform, using motion sensors and automated data capture  
- **Duration**: Multi-year experimental campaign with consistent protocol  
- **Structure**:
  - **Raw data**: Trial-level, time-stamped metrics (parquet format)
  - **Processed data**: One-row-per-rat behavioral summaries (CSV)

### Feature Types

- Total locomotion and exploration
- Pre- and post-reward zone entries and durations
- Learning efficiency and strategy ratios
- Trial-by-trial behaviour dynamics
- Metadata: sex, generation, year, weight, box, paradigm, group

---

## Repository Structure

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

## How to Use

1. Clone the repo:
   ```bash
   git clone https://github.com/szegedai/ambitus-rat-behaviour-dataset.git
   cd ambitus-rat-behaviour-dataset
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


## Outputs

- `ambitus_0_15_ml_ready_*.csv` – Flattened, clean per-subject dataset  
- `feature_missingness.csv`, `fig_missing_bar.pdf` – Completeness reports  
- `gen_drift_spearman.csv` – Generational drift correlations  
- `fig_drift_heatmap.pdf`, `fig_drift_lineplot.pdf` – Trend visualizations  

---

## Citation

If you use this dataset in your research, please cite:

> DOI: 10.5281/zenodo.16414893

---

## Contact

For questions or collaboration:
- korosi.gabor [at] inf.u-szeged.hu
- czimbalmos [at] inf.u-szeged.hu
- University of Szeged – Institute of Informatics

---

## Keywords

`rat behaviour`, `ambitus`, `multi-generational`, `exploration`, `motivation`, `learning`, `neuroscience`, `machine learning`, `ANOVA`, `phenotyping`

---
## Feature descriptions

### raw/ambitus_0_15_log_29_07_2025.parquet


| Feature name | Description | Unit | Note |
| --- | --- | --- | --- |
| Matadata |  |  |  |
| Animal | Animal ID | Text (str) |  |
| Generation | Number of the generation where the rat belongs | Number (int or float) |  |
| Season | The season when the animals were delivered | Date |  |
| Separation | Date of the separation from the bunch | Date |  |
| G_S | The searon of the different generations | Text (str) |  |
| Paradigm | Types of tasks: Task1 or Task2 | Text (str) |  |
| Date_Ambitus | Date of Ambitus test | Date |  |
| Year | Year of the experiment (0-15) | Number (int or float) |  |
| NR | ID number of the animal | Text (str) |  |
| Group | The group label of the rat | Number (int or float) |  |
| Sex | Sex of the rat |  |  |
| GR_Sex | The sex of the animals in the different groups together | Text (str) |  |
| Trials | Number of trial | Number (int or float) |  |
| Reward collection related parameters |  |  |  |
| EAT_E_Nr | The number of the collected rewards from the external boxes | Number (int or float) | Only trial 1-2 |
| EAT_E_% | The percentage of the collected rewards from the external boxes (number of collected rewards x 100)/8available rewards [8]) | % | Only trial 1-2 |
| EAT_I_Nr | The number of the collected rewards from the internal boxes | Number (int or float) |  |
| EAT_I_% | The percentage of the collected rewards from the internal boxes (number of collected rewards x 100)/8available rewards [8]) | % |  |
| EAT_TOT_Nr | The number of the collected rewards from all boxes | Number (int or float) |  |
| EAT_TOT_%% | The percentage of the collected rewards from all boxes (number of collected rewards x 100)/8available rewards [16]) | % |  |
| EAT_E_T | The time up to the collection of the rewards from the external boxes (cut off time: 300) | Second | Only trial 1-2 |
| EAT_I_T | The time up to the collection of the rewards from the internal boxes (cut off time: 300) | Second |  |
| EAT_TOT_T | The time up to the collection of the rewards from all boxes (cut off time: 300) | Second |  |
| Locomotion related parameters |  |  |  |
| Dir_Change_Nr | The number of direction changes  during the 300s | Number (int or float) |  |
| Circle_Nr | The number of total circles  during the 300s | Number (int or float) |  |
| LOCO_TOT | The number of entries into the corridors during the 300s | Number (int or float) |  |
| Explored Area | The number of visited corridors (max:4) | Number (int or float) |  |
| Loco_BEF_NR | The number of entries into the corridors up to collection of rewards. (Number of corridor entries up to collection of rewards × 300) / EAT_TOT_T. | Number (int or float) |  |
| LOCO_BEF | Locomotion frequency up to the task completion. (Number of entries in a corridor × 300s) / Eating time (s). | Number (int or float) |  |
| Exploratory activity related parameters |  |  |  |
| Expl_E_BEF_Nr | Number of external box visits before reward collection. | Number (int or float) |  |
| Expl_I_BEF_Nr | Number of internal box visits before reward collection. | Number (int or float) |  |
| Expl_E_I_BEF_Nr | Number of all box visits before reward collection. | Number (int or float) |  |
| Expl_E_BEF_Calc | Subset exploration categorized as external box visits up to collection of the rewards. (Number of external box exploration × 300) / EAT_TOT_T. | Number (int or float) |  |
| Expl_I_BEF_Calc | Subset of exploration categorized as internal box visits up to collection of the rewards. (Number of internal box exploration × 300) / EAT_TOT_T. | Number (int or float) |  |
| EXPL_BEF | Subset of exploration up to collection of the rewards.(Number of box exploration up to collection of reward × 300) / EAT_TOT_T. | Number (int or float) |  |
| Expl_E_AFT_Nr | Number of external box exploration after the collection of the rewards. | Number (int or float) | If the eating time is 300, there is no value |
| Expl_I_AFT_Nr | Number of internal box exploration after the collection of the rewards. | Number (int or float) | If the eating time is 300, there is no value |
| Expl_E_I_AFT_Nr | Number of all box exploration after the collection of the rewards. | Number (int or float) | If the eating time is 300, there is no value |
| Expl_E_AFT_Calc | Subset of external box exploration after the collection of all rewards. (Number of external box exploration after the collection of all rewards × 300) / (300-EAT_TOT_T). | Number (int or float) | If the eating time is 300, there is no value |
| Expl_I_AFT_Calc | Subset of internal exploration after the collection of all rewards. (Number of internal box exploration after the collection of all rewards × 300) / (300-EAT_TOT_T). | Number (int or float) | If the eating time is 300, there is no value |
| Expl_E_I_AFT_Calc | Subset of exploration after the collection of all rewards. (Number of box exploration after the collection of all rewards × 300) / (300-EAT_TOT_T). | Number (int or float) | If the eating time is 300, there is no value |
| Expl_E_BEF_AFT_Nr | Number of external box exploration during 300 s. | Number (int or float) |  |
| Expl_I_BEF_AFT_Nr | Number of internal box exploration during 300 s. | Number (int or float) |  |
| EXPL_TOT | Number of all box exploration during 300 s. | Number (int or float) |  |
| Expl_E_BEF_T | Duration of external box visits up to the collection of rewards | Second |  |
| Expl_I_BEF_T | Duration of internal box visits up to the collection of rewards | Second |  |
| Expl_E_I_BEF_T | Duration of box visits up to the collection of rewards | Second |  |
| Expl_E_BEF_Calc_T | Subset exploration time categorized as external box visits up to collection of the rewards. (Duration of external box exploration × 300) / EAT_TOT_T. | Second |  |
| Expl_I_BEF_Calc_T | Subset exploration time categorized as external box visits up to collection of the rewards. (Duration of external box exploration × 300) / EAT_TOT_T. | Second |  |
| Expl_E_I_BEF_Calc_T | Subset exploration time categorized as external box visits up to collection of the rewards. (Duration of external box exploration × 300) /EAT_TOT_T. | Second |  |
| Expl_E_AFT_T | Duration of external box visits after the collection of all rewards | Second | If the eating time is 300, there is no value |
| Expl_I_AFT_T | Duration of internal box visits after the collection of all rewards | Second | If the eating time is 300, there is no value |
| Expl_E_I_AFT_T | Duration of box visits after the collection of all rewards | Second | If the eating time is 300, there is no value |
| Expl_E_AFT_T_Calc | Subset exploration time categorized as external box visits after the collection of all rewards. (Duration of external box exploration after the collection of all rewards × 300) / (300-EAT_TOT_T). | Second | If the eating time is 300, there is no value |
| Expl_I_AFT_T_Calc | Subset exploration time categorized as internal box visits after the collection of all rewards. (Duration of internal box exploration after the collection of all rewards × 300) / (300-EAT_TOT_T). | Second | If the eating time is 300, there is no value |
| Expl_E_I_AFT_T_Calc | Subset exploration time categorized as external box visits after the collection of all rewards. (Duration of external box exploration after the collection of all rewards × 300) / (300-EAT_TOT_T). | Second | If the eating time is 300, there is no value |
| Expl_E_BEF_AFT_T | Duration of external box exploration during 300 s. | Second |  |
| Expl_I_BEF_AFT_T | Duration of internal box exploration during 300 s. | Second |  |
| Expl_TOT_T | Duration of all box exploration during 300 s. | Second |  |
| Expl_E_BEF_Loco_ratio | Locomotion-independent exploration into the external boxes up to the EAT_T:  The ratio of external visits to locomotor activity until all rewards were collected. | Number (int or float) | Only trial 1-2 |
| Expl_I_BEF_Loco_ratio | Locomotion-independent exploration into the internal boxes up to the EAT_T:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio |  |
| Expl_EI_BEF_Loco_ratio | Locomotion-independent exploration into the  boxes up to the EAT_T:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio |  |
| Expl_E_TOT_Loco_ratio | Locomotion-independent exploration into the external boxes during the 300 s:  The ratio of external visits to locomotor activity until all rewards were collected. | Ratio |  |
| Expl_I_TOT_Loco_ratio | Locomotion-independent exploration into the internal boxes during the 300 s:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio |  |
| Expl_E_I_TOT_Loco_ratio | Locomotion-independent exploration into the  boxes during the 300 s:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio |  |
| LAT_E | Latency of the first exploration into an external box. | ms |  |
| LAT_I | Latency of the first exploration into an internal box. | ms |  |
| LAT_E_I | Latency of the first exploration into a box. | ms |  |
| Lat_Tot_Log | Logarithmic value of the latency of the first exploration into an external box. | Log(ms) |  |
| Lat_E_Log | Logarithmic value of the latency of the first exploration into an internal box. | Log(ms) |  |
| Lat_I_Log | Logarithmic value of the latency of the first exploration into a box. | Log(ms) |  |
| Box_E_BEF_Nr | Number of visited external boxes up to EAT_TOT_T. | Number (int or float) | Maximum:8 |
| Box_I_BEF_Nr | Number of visited internal boxes up to EAT_TOT_T. | Number (int or float) | Maximum:8 |
| Box_E_I_BEF_Nr | Number of visited boxes up to EAT_TOT_T. | Number (int or float) | Maximum:16 |
| Box_REP_E_BEF_Nr | Number of repeatedly visited external boxes up to EAT_TOT_T. | Number (int or float) |  |
| Box_REP_I_BEF_Nr | Number of repeatedly visited internal boxes up to EAT_TOT_T. | Number (int or float) |  |
| Box_REP_E_I_BEF_Nr | Number of repeatedly visited boxes up to EAT_TOT_T. | Number (int or float) |  |
| Expl_REP_E_BEF_Nr | Number of repetition of the explorations into the internal boxes up to EAT_TOT_T. | Number (int or float) |  |
| Expl_REP_I_BEF_Nr | Number of repetition of the explorations into the internal boxes up to EAT_TOT_T. | Number (int or float) |  |
| Expl_REP_BEF_Nr | Number of repetition of the explorations into the internal boxes up to EAT_TOT_T. | Number (int or float) |  |
| Expl_REP_E_BEF_Calc_T | Exploration repetitions in the external boxes up to collection of the rewards. (Number of external box visit repetition × 300) / EAT_TOT_T. | Number (int or float) |  |
| Expl_REP_I_BEF_Calc_T | Exploration repetitions in the internal boxes up to collection of the rewards. (Number of internal box visit repetition × 300) / EAT_TOT_T. | Number (int or float) |  |
| Expl_REP_E_I_BEF_Calc_T | Exploration repetitions in the all boxes up to collection of the rewards. (Number of box visit repetition × 300) / EAT_TOT_T. | Number (int or float) |  |
| Expl_REP_E_AFT_Nr | Number of repetition of the explorations into the internal boxes after EAT_TOT_T. | Number (int or float) | If the eating time is 300, there is no value |
| Expl_REP_I_AFT_Nr | Number of repetition of the explorations into the internal boxes after EAT_TOT_T. | Number (int or float) | If the eating time is 300, there is no value |
| Expl_REP_AFT_Nr | Number of repetition of the explorations into the internal boxes after EAT_TOT_T. | Number (int or float) |  |
| Expl_REP_E_AFT_Nr_Calc | Exploration repetitions in the external boxes after the collection of the rewards. (Number of external box visit repetition × 300) / 300-EAT_TOT_T). | Number (int or float) |  |
| Expl_REP_I_AFT_Nr_Calc | Exploration repetitions in the internal boxes after the collection of the rewards. (Number of internal box visit repetition × 300) / 300-EAT_TOT_T). | Number (int or float) |  |
| Expl_REP_AFT_Nr_Calc | Exploration repetitions in the external boxes after the collection of the rewards. (Number of box visit repetition × 300) / 300-EAT_TOT_T). | Number (int or float) |  |
| Expl_REP_E_BEF_AFT_Nr | Number of repeated external box exploration during 300 s. | Number (int or float) |  |
| Expl_REP_I_BEF_AFT_Nr | Number of repeated internal box exploration during 300 s. | Number (int or float) |  |
| Expl_REP_TOT_Nr | Number of repeated all box exploration during 300 s. | Number (int or float) |  |
| Learning related parameters |  |  |  |
| L_C_E | Learning capacity at the external boxes: (Eat_E_Nr x 300 x 100)/[(number of available rewards; [8]) x (Eat_E_T)] | % | No food there, no value (Trial 3,4) |
| L_C_I | Learning capacity at the internal boxes: (Eat_I_Nr x 300 x 100)/[(number of available rewards; [8]) x (Eat_I_T)] | % | There is value for 1-4 trials |
| L_C_Tot | Learning capacity at both sides: (Eat_Nr x 300 x 100)/[(number of rewards)x(Eat_Tot_T)] | % | Only trial 1-2 |
| L_C | Learning capacity for all trials at both sides: (Eat_Nr x 300 x 100)/[(number of rewards)x(Eat_Tot_T)] | % |  |
| A_E | Adequate exploration: (Eat_Nr x 100)/(number of explorations up to Eat_T) | % | If the divisor is 0 the value is 0 |
| Error related parameters |  |  |  |
| First_Box location | The side of the first visit (1=internal; 2=external box) | Number (int or float) | Discrete feature only value 1 or 2 |
| Skipping | The number of entries into the corridors up to the first exploration | Number (int or float) |  |
| Expl_E_BEF_Ratio | The ratio of visits to external and total explorations up to collection of all rewards. | ratio |  |
| Expl_E_TOT_Ratio | The ratio of visits to external and total explorations during 300s. | ratio |  |
| Eff_Expl_E | (Eat_E_Nr x 100)/(number of external box visited [max:8]) | ratio | Only trial 1-2 |
| Eff_Expl_I | (Eat_I_Nr x 100)/(number of internal box visited [max:8]) | % |  |
| Eff_Expl_EI | (Eat_Tot_Nr x 100)/(number of box visited [max:16]) | % | Only trial 1-2 |
| E_E | Effective exploration.  (Eat_Nr x 100)/(number of box visited [max:16 for trials 1-2 and max:8 for trials 3-4]) | % |  |

### processed/ambitus_0_15_ml_ready_29_07_2025.csv

| Feature Name | Description | Unit | Note |
| --- | --- | --- | --- |
| Generation | Number of the generation where the rat belongs | Number (int or float) |  |
| Season | The season when the animals were delivered | Date |  |
| Paradigm | Types of tasks: Task1 or Task2 | Text (str) |  |
| Year | Year of the experiment (0-15) | Number (int or float) |  |
| NR | ID number of the animal | Text (str) |  |
| Group | The group label of the rat | Number (int or float) |  |
| Sex | Sex of the rat |  |  |
| EAT_E_% | The percentage of the collected rewards from the external boxes (number of collected rewards x 100)/8available rewards [8]) | % | At first trial |
| EAT_I_% | The percentage of the collected rewards from the internal boxes (number of collected rewards x 100)/8available rewards [8]) | % | At first trial |
| EAT_TOT_%% | The percentage of the collected rewards from all boxes (number of collected rewards x 100)/8available rewards [16]) | % | At first trial |
| EAT_E_T | The time up to the collection of the rewards from the external boxes (cut off time: 300) | Second | At first trial |
| EAT_I_T | The time up to the collection of the rewards from the internal boxes (cut off time: 300) | Second | At first trial |
| EAT_TOT_T | The time up to the collection of the rewards from all boxes (cut off time: 300) | Second | At first trial |
| Expl_E_BEF_Calc | Subset exploration categorized as external box visits up to collection of the rewards. (Number of external box exploration × 300) / EAT_TOT_T. | Number (int or float) |  |
| Expl_I_BEF_Calc | Subset of exploration categorized as internal box visits up to collection of the rewards. (Number of internal box exploration × 300) / EAT_TOT_T. | Number (int or float) | At first trial |
| EXPL_BEF | Subset of exploration up to collection of the rewards.(Number of box exploration up to collection of reward × 300) / EAT_TOT_T. | Number (int or float) | At first trial |
| Expl_E_BEF_AFT_Nr | Number of external box exploration during 300 s. | Number (int or float) | At first trial |
| Expl_I_BEF_AFT_Nr | Number of internal box exploration during 300 s. | Number (int or float) | At first trial |
| EXPL_TOT | Number of all box exploration during 300 s. | Number (int or float) | At first trial |
| Expl_E_BEF_AFT_T | Duration of external box exploration during 300 s. | Second | At first trial |
| Expl_I_BEF_AFT_T | Duration of internal box exploration during 300 s. | Second | At first trial |
| Expl_TOT_T | Duration of all box exploration during 300 s. | Second | At first trial |
| Lat_Tot_Log | Logarithmic value of the latency of the first exploration into an external box. | Log(ms) | At first trial |
| Lat_E_Log | Logarithmic value of the latency of the first exploration into an internal box. | Log(ms) | At first trial |
| Lat_I_Log | Logarithmic value of the latency of the first exploration into a box. | Log(ms) | At first trial |
| Box_E_BEF_Nr | Number of visited external boxes up to EAT_TOT_T. | Number (int or float) | At first trial |
| Box_I_BEF_Nr | Number of visited internal boxes up to EAT_TOT_T. | Number (int or float) | At first trial |
| Box_E_I_BEF_Nr | Number of visited boxes up to EAT_TOT_T. | Number (int or float) | At first trial |
| Box_REP_E_BEF_Nr | Number of repeatedly visited external boxes up to EAT_TOT_T. | Number (int or float) | At first trial |
| Box_REP_I_BEF_Nr | Number of repeatedly visited internal boxes up to EAT_TOT_T. | Number (int or float) | At first trial |
| Box_REP_E_I_BEF_Nr | Number of repeatedly visited boxes up to EAT_TOT_T. | Number (int or float) | At first trial |
| Expl_REP_E_BEF_Calc_T | Exploration repetitions in the external boxes up to collection of the rewards. (Number of external box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At first trial |
| Expl_REP_I_BEF_Calc_T | Exploration repetitions in the internal boxes up to collection of the rewards. (Number of internal box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At first trial |
| Expl_REP_E_I_BEF_Calc_T | Exploration repetitions in the all boxes up to collection of the rewards. (Number of box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At first trial |
| Expl_REP_E_BEF_AFT_Nr | Number of repeated external box exploration during 300 s. | Number (int or float) | At first trial |
| Expl_REP_I_BEF_AFT_Nr | Number of repeated internal box exploration during 300 s. | Number (int or float) | At first trial |
| Expl_REP_TOT_Nr | Number of repeated all box exploration during 300 s. | Number (int or float) | At first trial |
| Dir_Change_Nr | The number of direction changes  during the 300s | Number (int or float) | At first trial |
| Circle_Nr | The number of total circles  during the 300s | Number (int or float) | At first trial |
| LOCO_TOT | The number of entries into the corridors during the 300s | Number (int or float) | At first trial |
| Explored Area | The number of visited corridors (max:4) | Number (int or float) | At first trial |
| Loco_BEF_NR | The number of entries into the corridors up to collection of rewards. (Number of corridor entries up to collection of rewards × 300) / EAT_TOT_T. | Number (int or float) | At first trial |
| Expl_E_BEF_Ratio | The ratio of visits to external and total explorations up to collection of all rewards. | ratio | At first trial |
| Expl_E_TOT_Ratio | The ratio of visits to external and total explorations during 300s. | ratio | At first trial |
| L_C_E | Learning capacity at the external boxes: (Eat_E_Nr x 300 x 100)/[(number of available rewards; [8]) x (Eat_E_T)] | % | At first trial |
| L_C_I | Learning capacity at the internal boxes: (Eat_I_Nr x 300 x 100)/[(number of available rewards; [8]) x (Eat_I_T)] | % | At first trial |
| L_C | Learning capacity for all trials at both sides: (Eat_Nr x 300 x 100)/[(number of rewards)x(Eat_Tot_T)] | % | At first trial |
| A_E | Adequate exploration: (Eat_Nr x 100)/(number of explorations up to Eat_T) | % | At first trial |
| Expl_E_BEF_Loco_ratio | Locomotion-independent exploration into the external boxes up to the EAT_T:  The ratio of external visits to locomotor activity until all rewards were collected. | Number (int or float) | At first trial |
| Expl_I_BEF_Loco_ratio | Locomotion-independent exploration into the internal boxes up to the EAT_T:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio | At first trial |
| Expl_EI_BEF_Loco_ratio | Locomotion-independent exploration into the  boxes up to the EAT_T:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio | At first trial |
| Expl_E_TOT_Loco_ratio | Locomotion-independent exploration into the external boxes during the 300 s:  The ratio of external visits to locomotor activity until all rewards were collected. | Ratio | At first trial |
| Expl_I_TOT_Loco_ratio | Locomotion-independent exploration into the internal boxes during the 300 s:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio | At first trial |
| Expl_E_I_TOT_Loco_ratio | Locomotion-independent exploration into the  boxes during the 300 s:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio | At first trial |
| Eff_Expl_E | (Eat_E_Nr x 100)/(number of external box visited [max:8]) | ratio | At first trial |
| Eff_Expl_I | (Eat_I_Nr x 100)/(number of internal box visited [max:8]) | % | At first trial |
| Eff_Expl_EI | (Eat_Tot_Nr x 100)/(number of box visited [max:16]) | % | At first trial |
| E_E | Effective exploration.  (Eat_Nr x 100)/(number of box visited [max:16 for trials 1-2 and max:8 for trials 3-4]) | % | At first trial |
| id | Unique identifier constructed from Group, NR and Generation | Number (int) |  |
| EAT_E_%_2 | The percentage of the collected rewards from the external boxes (number of collected rewards x 100)/8available rewards [8]) | % | At second trial |
| EAT_I_%_2 | The percentage of the collected rewards from the internal boxes (number of collected rewards x 100)/8available rewards [8]) | % | At second trial |
| EAT_TOT_%%_2 | The percentage of the collected rewards from all boxes (number of collected rewards x 100)/8available rewards [16]) | % | At second trial |
| EAT_E_T_2 | The time up to the collection of the rewards from the external boxes (cut off time: 300) | Second | At second trial |
| EAT_I_T_2 | The time up to the collection of the rewards from the internal boxes (cut off time: 300) | Second | At second trial |
| EAT_TOT_T_2 | The time up to the collection of the rewards from all boxes (cut off time: 300) | Second | At second trial |
| Expl_E_BEF_Calc_2 | Subset exploration categorized as external box visits up to collection of the rewards. (Number of external box exploration × 300) / EAT_TOT_T. | Number (int or float) | At second trial |
| Expl_I_BEF_Calc_2 | Subset of exploration categorized as internal box visits up to collection of the rewards. (Number of internal box exploration × 300) / EAT_TOT_T. | Number (int or float) | At second trial |
| EXPL_BEF_2 | Subset of exploration up to collection of the rewards.(Number of box exploration up to collection of reward × 300) / EAT_TOT_T. | Number (int or float) | At second trial |
| Expl_E_BEF_AFT_Nr_2 | Number of external box exploration during 300 s. | Number (int or float) | At second trial |
| Expl_I_BEF_AFT_Nr_2 | Number of internal box exploration during 300 s. | Number (int or float) | At second trial |
| EXPL_TOT_2 | Number of all box exploration during 300 s. | Number (int or float) | At second trial |
| Expl_E_BEF_AFT_T_2 | Duration of external box exploration during 300 s. | Second | At second trial |
| Expl_I_BEF_AFT_T_2 | Duration of internal box exploration during 300 s. | Second | At second trial |
| Expl_TOT_T_2 | Duration of all box exploration during 300 s. | Second | At second trial |
| Lat_Tot_Log_2 | Logarithmic value of the latency of the first exploration into an external box. | Log(ms) | At second trial |
| Lat_E_Log_2 | Logarithmic value of the latency of the first exploration into an internal box. | Log(ms) | At second trial |
| Lat_I_Log_2 | Logarithmic value of the latency of the first exploration into a box. | Log(ms) | At second trial |
| Box_E_BEF_Nr_2 | Number of visited external boxes up to EAT_TOT_T. | Number (int or float) | At second trial |
| Box_I_BEF_Nr_2 | Number of visited internal boxes up to EAT_TOT_T. | Number (int or float) | At second trial |
| Box_E_I_BEF_Nr_2 | Number of visited boxes up to EAT_TOT_T. | Number (int or float) | At second trial |
| Box_REP_E_BEF_Nr_2 | Number of repeatedly visited external boxes up to EAT_TOT_T. | Number (int or float) | At second trial |
| Box_REP_I_BEF_Nr_2 | Number of repeatedly visited internal boxes up to EAT_TOT_T. | Number (int or float) | At second trial |
| Box_REP_E_I_BEF_Nr_2 | Number of repeatedly visited boxes up to EAT_TOT_T. | Number (int or float) | At second trial |
| Expl_REP_E_BEF_Calc_T_2 | Exploration repetitions in the external boxes up to collection of the rewards. (Number of external box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At second trial |
| Expl_REP_I_BEF_Calc_T_2 | Exploration repetitions in the internal boxes up to collection of the rewards. (Number of internal box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At second trial |
| Expl_REP_E_I_BEF_Calc_T_2 | Exploration repetitions in the all boxes up to collection of the rewards. (Number of box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At second trial |
| Expl_REP_E_BEF_AFT_Nr_2 | Number of repeated external box exploration during 300 s. | Number (int or float) | At second trial |
| Expl_REP_I_BEF_AFT_Nr_2 | Number of repeated internal box exploration during 300 s. | Number (int or float) | At second trial |
| Expl_REP_TOT_Nr_2 | Number of repeated all box exploration during 300 s. | Number (int or float) | At second trial |
| Dir_Change_Nr_2 | The number of direction changes  during the 300s | Number (int or float) | At second trial |
| Circle_Nr_2 | The number of total circles  during the 300s | Number (int or float) | At second trial |
| LOCO_TOT_2 | The number of entries into the corridors during the 300s | Number (int or float) | At second trial |
| Explored Area_2 | The number of visited corridors (max:4) | Number (int or float) | At second trial |
| Expl_E_BEF_Ratio_2 | The ratio of visits to external and total explorations up to collection of all rewards. | ratio | At second trial |
| Expl_E_TOT_Ratio_2 | The ratio of visits to external and total explorations during 300s. | ratio | At second trial |
| L_C_E_2 | Learning capacity at the external boxes: (Eat_E_Nr x 300 x 100)/[(number of available rewards; [8]) x (Eat_E_T)] | % | At second trial |
| L_C_I_2 | Learning capacity at the internal boxes: (Eat_I_Nr x 300 x 100)/[(number of available rewards; [8]) x (Eat_I_T)] | % | At second trial |
| L_C_2 | Learning capacity for all trials at both sides: (Eat_Nr x 300 x 100)/[(number of rewards)x(Eat_Tot_T)] | % | At second trial |
| A_E_2 | Adequate exploration: (Eat_Nr x 100)/(number of explorations up to Eat_T) | % | At second trial |
| Expl_E_BEF_Loco_ratio_2 | Locomotion-independent exploration into the external boxes up to the EAT_T:  The ratio of external visits to locomotor activity until all rewards were collected. | Number (int or float) | At second trial |
| Expl_I_BEF_Loco_ratio_2 | Locomotion-independent exploration into the internal boxes up to the EAT_T:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio | At second trial |
| Expl_EI_BEF_Loco_ratio_2 | Locomotion-independent exploration into the  boxes up to the EAT_T:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio | At second trial |
| Expl_E_TOT_Loco_ratio_2 | Locomotion-independent exploration into the external boxes during the 300 s:  The ratio of external visits to locomotor activity until all rewards were collected. | Ratio | At second trial |
| Expl_I_TOT_Loco_ratio_2 | Locomotion-independent exploration into the internal boxes during the 300 s:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio | At second trial |
| Expl_E_I_TOT_Loco_ratio_2 | Locomotion-independent exploration into the  boxes during the 300 s:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio | At second trial |
| Eff_Expl_E_2 | (Eat_E_Nr x 100)/(number of external box visited [max:8]) | ratio | At second trial |
| Eff_Expl_I_2 | (Eat_I_Nr x 100)/(number of internal box visited [max:8]) | % | At second trial |
| Eff_Expl_EI_2 | (Eat_Tot_Nr x 100)/(number of box visited [max:16]) | % | At second trial |
| E_E_2 | Effective exploration.  (Eat_Nr x 100)/(number of box visited [max:16 for trials 1-2 and max:8 for trials 3-4]) | % | At second trial |
| EAT_I_%_3 | The percentage of the collected rewards from the internal boxes (number of collected rewards x 100)/8available rewards [8]) | % | At third trial |
| EAT_TOT_%%_3 | The percentage of the collected rewards from all boxes (number of collected rewards x 100)/8available rewards [16]) | % | At third trial |
| EAT_I_T_3 | The time up to the collection of the rewards from the internal boxes (cut off time: 300) | Second | At third trial |
| EAT_TOT_T_3 | The time up to the collection of the rewards from all boxes (cut off time: 300) | Second | At third trial |
| Expl_E_BEF_Calc_3 | Subset exploration categorized as external box visits up to collection of the rewards. (Number of external box exploration × 300) / EAT_TOT_T. | Number (int or float) | At third trial |
| Expl_I_BEF_Calc_3 | Subset of exploration categorized as internal box visits up to collection of the rewards. (Number of internal box exploration × 300) / EAT_TOT_T. | Number (int or float) | At third trial |
| EXPL_BEF_3 | Subset of exploration up to collection of the rewards.(Number of box exploration up to collection of reward × 300) / EAT_TOT_T. | Number (int or float) | At third trial |
| Expl_E_BEF_AFT_Nr_3 | Number of external box exploration during 300 s. | Number (int or float) | At third trial |
| Expl_I_BEF_AFT_Nr_3 | Number of internal box exploration during 300 s. | Number (int or float) | At third trial |
| EXPL_TOT_3 | Number of all box exploration during 300 s. | Number (int or float) | At third trial |
| Expl_E_BEF_AFT_T_3 | Duration of external box exploration during 300 s. | Second | At third trial |
| Expl_I_BEF_AFT_T_3 | Duration of internal box exploration during 300 s. | Second | At third trial |
| Expl_TOT_T_3 | Duration of all box exploration during 300 s. | Second | At third trial |
| Lat_Tot_Log_3 | Logarithmic value of the latency of the first exploration into an external box. | Log(ms) | At third trial |
| Lat_E_Log_3 | Logarithmic value of the latency of the first exploration into an internal box. | Log(ms) | At third trial |
| Lat_I_Log_3 | Logarithmic value of the latency of the first exploration into a box. | Log(ms) | At third trial |
| Box_E_BEF_Nr_3 | Number of visited external boxes up to EAT_TOT_T. | Number (int or float) | At third trial |
| Box_I_BEF_Nr_3 | Number of visited internal boxes up to EAT_TOT_T. | Number (int or float) | At third trial |
| Box_E_I_BEF_Nr_3 | Number of visited boxes up to EAT_TOT_T. | Number (int or float) | At third trial |
| Box_REP_E_BEF_Nr_3 | Number of repeatedly visited external boxes up to EAT_TOT_T. | Number (int or float) | At third trial |
| Box_REP_I_BEF_Nr_3 | Number of repeatedly visited internal boxes up to EAT_TOT_T. | Number (int or float) | At third trial |
| Box_REP_E_I_BEF_Nr_3 | Number of repeatedly visited boxes up to EAT_TOT_T. | Number (int or float) | At third trial |
| Expl_REP_E_BEF_Calc_T_3 | Exploration repetitions in the external boxes up to collection of the rewards. (Number of external box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At third trial |
| Expl_REP_I_BEF_Calc_T_3 | Exploration repetitions in the internal boxes up to collection of the rewards. (Number of internal box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At third trial |
| Expl_REP_E_I_BEF_Calc_T_3 | Exploration repetitions in the all boxes up to collection of the rewards. (Number of box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At third trial |
| Expl_REP_E_BEF_AFT_Nr_3 | Number of repeated external box exploration during 300 s. | Number (int or float) | At third trial |
| Expl_REP_I_BEF_AFT_Nr_3 | Number of repeated internal box exploration during 300 s. | Number (int or float) | At third trial |
| Expl_REP_TOT_Nr_3 | Number of repeated all box exploration during 300 s. | Number (int or float) | At third trial |
| Dir_Change_Nr_3 | The number of direction changes  during the 300s | Number (int or float) | At third trial |
| Circle_Nr_3 | The number of total circles  during the 300s | Number (int or float) | At third trial |
| LOCO_TOT_3 | The number of entries into the corridors during the 300s | Number (int or float) | At third trial |
| Explored Area_3 | The number of visited corridors (max:4) | Number (int or float) | At third trial |
| Expl_E_BEF_Ratio_3 | The ratio of visits to external and total explorations up to collection of all rewards. | ratio | At third trial |
| Expl_E_TOT_Ratio_3 | The ratio of visits to external and total explorations during 300s. | ratio | At third trial |
| L_C_I_3 | Learning capacity at the internal boxes: (Eat_I_Nr x 300 x 100)/[(number of available rewards; [8]) x (Eat_I_T)] | % | At third trial |
| L_C_3 | Learning capacity for all trials at both sides: (Eat_Nr x 300 x 100)/[(number of rewards)x(Eat_Tot_T)] | % | At third trial |
| A_E_3 | Adequate exploration: (Eat_Nr x 100)/(number of explorations up to Eat_T) | % | At third trial |
| Expl_E_BEF_Loco_ratio_3 | Locomotion-independent exploration into the external boxes up to the EAT_T:  The ratio of external visits to locomotor activity until all rewards were collected. | Number (int or float) | At third trial |
| Expl_I_BEF_Loco_ratio_3 | Locomotion-independent exploration into the internal boxes up to the EAT_T:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio | At third trial |
| Expl_EI_BEF_Loco_ratio_3 | Locomotion-independent exploration into the  boxes up to the EAT_T:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio | At third trial |
| Expl_E_TOT_Loco_ratio_3 | Locomotion-independent exploration into the external boxes during the 300 s:  The ratio of external visits to locomotor activity until all rewards were collected. | Ratio | At third trial |
| Expl_I_TOT_Loco_ratio_3 | Locomotion-independent exploration into the internal boxes during the 300 s:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio | At third trial |
| Expl_E_I_TOT_Loco_ratio_3 | Locomotion-independent exploration into the  boxes during the 300 s:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio | At third trial |
| Eff_Expl_I_3 | (Eat_I_Nr x 100)/(number of internal box visited [max:8]) | % | At third trial |
| Eff_Expl_EI_3 | (Eat_Tot_Nr x 100)/(number of box visited [max:16]) | % | At third trial |
| E_E_3 | Effective exploration.  (Eat_Nr x 100)/(number of box visited [max:16 for trials 1-2 and max:8 for trials 3-4]) | % | At third trial |
| EAT_I_%_4 | The percentage of the collected rewards from the internal boxes (number of collected rewards x 100)/8available rewards [8]) | % | At fourth trial |
| EAT_TOT_%%_4 | The percentage of the collected rewards from all boxes (number of collected rewards x 100)/8available rewards [16]) | % | At fourth trial |
| EAT_I_T_4 | The time up to the collection of the rewards from the internal boxes (cut off time: 300) | Second | At fourth trial |
| EAT_TOT_T_4 | The time up to the collection of the rewards from all boxes (cut off time: 300) | Second | At fourth trial |
| Expl_E_BEF_Calc_4 | Subset exploration categorized as external box visits up to collection of the rewards. (Number of external box exploration × 300) / EAT_TOT_T. | Number (int or float) | At fourth trial |
| Expl_I_BEF_Calc_4 | Subset of exploration categorized as internal box visits up to collection of the rewards. (Number of internal box exploration × 300) / EAT_TOT_T. | Number (int or float) | At fourth trial |
| EXPL_BEF_4 | Subset of exploration up to collection of the rewards.(Number of box exploration up to collection of reward × 300) / EAT_TOT_T. | Number (int or float) | At fourth trial |
| Expl_E_BEF_AFT_Nr_4 | Number of external box exploration during 300 s. | Number (int or float) | At fourth trial |
| Expl_I_BEF_AFT_Nr_4 | Number of internal box exploration during 300 s. | Number (int or float) | At fourth trial |
| EXPL_TOT_4 | Number of all box exploration during 300 s. | Number (int or float) | At fourth trial |
| Expl_E_BEF_AFT_T_4 | Duration of external box exploration during 300 s. | Second | At fourth trial |
| Expl_I_BEF_AFT_T_4 | Duration of internal box exploration during 300 s. | Second | At fourth trial |
| Expl_TOT_T_4 | Duration of all box exploration during 300 s. | Second | At fourth trial |
| Lat_Tot_Log_4 | Logarithmic value of the latency of the first exploration into an external box. | Log(ms) | At fourth trial |
| Lat_E_Log_4 | Logarithmic value of the latency of the first exploration into an internal box. | Log(ms) | At fourth trial |
| Lat_I_Log_4 | Logarithmic value of the latency of the first exploration into a box. | Log(ms) | At fourth trial |
| Box_E_BEF_Nr_4 | Number of visited external boxes up to EAT_TOT_T. | Number (int or float) | At fourth trial |
| Box_I_BEF_Nr_4 | Number of visited internal boxes up to EAT_TOT_T. | Number (int or float) | At fourth trial |
| Box_E_I_BEF_Nr_4 | Number of visited boxes up to EAT_TOT_T. | Number (int or float) | At fourth trial |
| Box_REP_E_BEF_Nr_4 | Number of repeatedly visited external boxes up to EAT_TOT_T. | Number (int or float) | At fourth trial |
| Box_REP_I_BEF_Nr_4 | Number of repeatedly visited internal boxes up to EAT_TOT_T. | Number (int or float) | At fourth trial |
| Box_REP_E_I_BEF_Nr_4 | Number of repeatedly visited boxes up to EAT_TOT_T. | Number (int or float) | At fourth trial |
| Expl_REP_E_BEF_Calc_T_4 | Exploration repetitions in the external boxes up to collection of the rewards. (Number of external box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At fourth trial |
| Expl_REP_I_BEF_Calc_T_4 | Exploration repetitions in the internal boxes up to collection of the rewards. (Number of internal box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At fourth trial |
| Expl_REP_E_I_BEF_Calc_T_4 | Exploration repetitions in the all boxes up to collection of the rewards. (Number of box visit repetition × 300) / EAT_TOT_T. | Number (int or float) | At fourth trial |
| Expl_REP_E_BEF_AFT_Nr_4 | Number of repeated external box exploration during 300 s. | Number (int or float) | At fourth trial |
| Expl_REP_I_BEF_AFT_Nr_4 | Number of repeated internal box exploration during 300 s. | Number (int or float) | At fourth trial |
| Expl_REP_TOT_Nr_4 | Number of repeated all box exploration during 300 s. | Number (int or float) | At fourth trial |
| Dir_Change_Nr_4 | The number of direction changes  during the 300s | Number (int or float) | At fourth trial |
| Circle_Nr_4 | The number of total circles  during the 300s | Number (int or float) | At fourth trial |
| LOCO_TOT_4 | The number of entries into the corridors during the 300s | Number (int or float) | At fourth trial |
| Explored Area_4 | The number of visited corridors (max:4) | Number (int or float) | At fourth trial |
| Expl_E_BEF_Ratio_4 | The ratio of visits to external and total explorations up to collection of all rewards. | ratio | At fourth trial |
| Expl_E_TOT_Ratio_4 | The ratio of visits to external and total explorations during 300s. | ratio | At fourth trial |
| L_C_I_4 | Learning capacity at the internal boxes: (Eat_I_Nr x 300 x 100)/[(number of available rewards; [8]) x (Eat_I_T)] | % | At fourth trial |
| L_C_4 | Learning capacity for all trials at both sides: (Eat_Nr x 300 x 100)/[(number of rewards)x(Eat_Tot_T)] | % | At fourth trial |
| A_E_4 | Adequate exploration: (Eat_Nr x 100)/(number of explorations up to Eat_T) | % | At fourth trial |
| Expl_E_BEF_Loco_ratio_4 | Locomotion-independent exploration into the external boxes up to the EAT_T:  The ratio of external visits to locomotor activity until all rewards were collected. | Number (int or float) | At fourth trial |
| Expl_I_BEF_Loco_ratio_4 | Locomotion-independent exploration into the internal boxes up to the EAT_T:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio | At fourth trial |
| Expl_EI_BEF_Loco_ratio_4 | Locomotion-independent exploration into the  boxes up to the EAT_T:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio | At fourth trial |
| Expl_E_TOT_Loco_ratio_4 | Locomotion-independent exploration into the external boxes during the 300 s:  The ratio of external visits to locomotor activity until all rewards were collected. | Ratio | At fourth trial |
| Expl_I_TOT_Loco_ratio_4 | Locomotion-independent exploration into the internal boxes during the 300 s:  The ratio of internal visits to locomotor activity until all rewards were collected. | Ratio | At fourth trial |
| Expl_E_I_TOT_Loco_ratio_4 | Locomotion-independent exploration into the  boxes during the 300 s:  The ratio of visits to locomotor activity until all rewards were collected. | Ratio | At fourth trial |
| Eff_Expl_I_4 | (Eat_I_Nr x 100)/(number of internal box visited [max:8]) | % | At fourth trial |
| Eff_Expl_EI_4 | (Eat_Tot_Nr x 100)/(number of box visited [max:16]) | % | At fourth trial |
| E_E_4 | Effective exploration.  (Eat_Nr x 100)/(number of box visited [max:16 for trials 1-2 and max:8 for trials 3-4]) | % | At fourth trial |