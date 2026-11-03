# Winnow-Lite: Dual-Branch Network Intrusion Detection Pipeline

[![Python 3.10+](https://img.shields.io/badge/python-3.10+-blue.svg)](https://www.python.org/downloads/)
[![PyTorch 2.0+](https://img.shields.io/badge/PyTorch-2.0+-ee4c2c.svg)](https://pytorch.org/)
[![XGBoost](https://img.shields.io/badge/XGBoost-GPU--Accelerated-green.svg)](https://xgboost.readthedocs.io/)
[![Dataset](https://img.shields.io/badge/Dataset-Corrected_CICIDS2017-orange.svg)](https://www.unb.ca/cic/datasets/ids-2017.html)
[![Release](https://img.shields.io/badge/Release-v1.0_Complete-success.svg)](file:///P:/Winnow/Figures%20and%20Results/winnow_lite_complete_release.zip)

**Winnow-Lite** is an asymmetric dual-branch intrusion detection architecture combining a high-throughput, stateless flow classifier (**Branch A**: $D=73$ XGBoost) and a temporal behavioral anomaly detector (**Branch B**: 11D PyTorch Tumbling-Window Autoencoder) regulated by a **60/40 Quantile Alert Budget Dial**.

---

## Master Pipeline Verification Status

For the complete audit table and literal OCR transcription, see **[`Transcribed Master Table.md`](file:///P:/Winnow/Transcribed%20Master%20Table.md)**.

| Phase | Directory | Description & Milestones | Status |
| :---: | :--- | :--- | :---: |
| **0** | [`phase_0`](file:///P:/Winnow/Notebook%20Code/phase_0/) | Environment setup, seeds, determinism, parquet verification, GPU verification | `VERIFIED` |
| **1** | [`phase_1`](file:///P:/Winnow/Notebook%20Code/phase_1/) | Ingestion of 5 weekday CSVs, schema validation, rate imputation, timestamp sanity | `VERIFIED` |
| **2** | [`phase_2`](file:///P:/Winnow/Notebook%20Code/phase_2/) | Temporal splitting, 48 purge gaps, zero-variance pruning ($D = 73$), `stage2_flows.parquet` | `VERIFIED` |
| **3** | [`phase_3`](file:///P:/Winnow/Notebook%20Code/phase_3/) | 11 tumbling-window features (60s), signed $\log(1+\|x\|)$, guarded scaler, Item 8 counts | `VERIFIED` |
| **4** | [`phase_4`](file:///P:/Winnow/Notebook%20Code/phase_4/) | Branch A Supervised XGBoost (265 trees), exact-twin diagnostic, threshold calibration | `VERIFIED` |
| **5** | [`phase_5`](file:///P:/Winnow/Notebook%20Code/phase_5/) | Branch B Window Autoencoder ($11 \to 8 \to 4 \to 8 \to 11$), Mann-Whitney $U$, dual calibration | `VERIFIED` |
| **6** | [`phase_6`](file:///P:/Winnow/Notebook%20Code/phase_6/) | Baseline Configs 4 & 5, 6-way validation benchmark preview, 4 LFO models, Checkpoint B4 | `VERIFIED` |
| **7** | [`phase_7`](file:///P:/Winnow/Notebook%20Code/phase_7/) | Checkpoints A5–A9, B5, B6: router permutations, drift harness, 20 reason cards, 48 gates | `VERIFIED` |
| **8** | [`phase_8`](file:///P:/Winnow/Notebook%20Code/phase_8/) | Single-pass locked Test evaluation, throughput timing, Tables 1, 1B, 2, 2B, 3, 4, 5 | `VERIFIED` |
| **9** | [`phase_9`](file:///P:/Winnow/Notebook%20Code/phase_9/) | Publication Figures 1–5: standalone (Cells 9.1–9.10) & composite master (Cell 9.11) | `VERIFIED` |
| **10** | [`phase_10`](file:///P:/Winnow/Notebook%20Code/phase_10/) | Production evaluator `winnow_score.py`, master gate ledger (109/112), release ZIPs | `VERIFIED` |
| **S_Dia** | [`s_dia`](file:///P:/Winnow/Notebook%20Code/s_dia/) | Executive styled presentation suite (Modern Palette): 6 standalone diagrams & ZIP | `VERIFIED` |

---

## Key Results on Locked Test Split ($\alpha = 10 / 10\text{k}$)

- **Overall Attack Recall:** **$97.51\%$** (up from $84.59\%$ with single-flow XGBoost alone)
- **$F_1$ Score:** **$0.9873$** (vs $0.9165$ for XGBoost and $0.0007$ for Single-Flow Autoencoder)
- **PR-AUC / ROC-AUC:** **$0.9993$ / $0.9998$**
- **PortScan Recall:** **$99.99\%$** ($9,015 / 9,016$ detected; $59.70\%$ rescued by Branch B, $40.28\%$ corroborated)
- **Observed Flow False Alarm Rate:** **$0.21$ per $10,000$ benign flows** ($6$ false alarms / $288,780$ flows)
- **Extreme Class Imbalance ($1:1,000$ Base Rate):** **$97.78\% \pm 0.44\%$ Precision**, matching theoretical Bayesian limits.

---

## Quick Links & Distribution Deliverables

- **Complete Release Archive**: [`winnow_lite_complete_release.zip`](file:///P:/Winnow/Figures%20and%20Results/winnow_lite_complete_release.zip) (9.35 MB)
- **Styled Presentation Archive**: [`winnow_s_dia_styled.zip`](file:///P:/Winnow/Figures%20and%20Results/winnow_s_dia_styled.zip) (1.37 MB)
- **Figures Archive**: [`winnow_figures.zip`](file:///P:/Winnow/Figures%20and%20Results/winnow_figures.zip) (4.68 MB)
- **Results Tables Archive**: [`winnow_results.zip`](file:///P:/Winnow/Figures%20and%20Results/winnow_results.zip) (28.1 KB)
- **Standalone Evaluator**: [`winnow_score.py`](file:///P:/Winnow/Figures%20and%20Results/winnow_lite_complete_release/winnow_score.py)
- **Executive Report**: [`FINAL_REPORT.md`](file:///P:/Winnow/Figures%20and%20Results/winnow_lite_complete_release/FINAL_REPORT.md)

