# IBM HR Analytics – Employee Attrition (Survival Modeling)

This project predicts **employee attrition risk over time** and exports a **3/6/12‑month risk table** for HR.
Pipeline (as presented in class slides): **EDA → Kaplan–Meier → Cox/RSF → XGBoost + SHAP → Risk table**.

> **Deliverable**: `results/employee_risk_table_3_6_12m.xlsx` with columns
> `EmployeeID, Prob_leave_3m, Prob_leave_6m, Prob_leave_12m, RiskTier_6m, Department, JobRole`.

---

## 1) Environment
```bash
python >= 3.9
pip install -r requirements.txt
```

## 2) Data
Place your IBM HR dataset at:
```
data/hr_data.csv
```
If your course bundle already provided a probability file (e.g., `employee_risk_table_3_6_12m.csv`), put it in `data/` as well.

## 3) Reproduce (minimal path)
The class already produced probabilities for 3/6/12 months. To format and export the **final risk table** (with proper percentage formatting and tiers), run:
```bash
python src/make_risk_table.py   --probs data/employee_risk_table_3_6_12m.csv   --out   results/employee_risk_table_3_6_12m.xlsx
```
or with an Excel input:
```bash
python src/make_risk_table.py   --probs data/employee_risk_table_3_6_12m.xlsx   --out   results/employee_risk_table_3_6_12m.xlsx
```

### Risk tier logic (editable)
Default thresholds for **6‑month** probability:
- `High`  : >= 0.30
- `Medium`: 0.10 – 0.30
- `Low`   : < 0.10

You can change these via CLI flags: `--hi 0.30 --mid 0.10`.

## 4) (Optional) Training notebooks
If you want to retrain models, add notebooks to `src/` (e.g., `train_cox.ipynb`, `train_rsf.ipynb`, `train_xgb_shap.ipynb`) and save model outputs to `results/`. The exported risk table can then be regenerated from your own probabilities.

## 5) Results
- Final export: `results/employee_risk_table_3_6_12m.xlsx` (percent display for `Prob_leave_*` and tier column).
- Intended use: HR sorts by 6‑month probability, focuses on top **10–20%** high risk, and reviews hotspots by department/job role.

## 6) Notes & Limitations
- The IBM HR dataset is synthetic/demo; thresholds should be validated in your org.
- Survival horizons beyond 12 months may be unstable without more data; monitor C‑index and calibration.

---

**Author:** Quach Lan Huong • **Course:** Artificial Intelligence • **Group:** 8
