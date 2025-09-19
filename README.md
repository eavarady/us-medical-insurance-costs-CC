# U.S. Medical Insurance Costs (Pure Python Exploration)

## 1. Overview

This project performs an exploratory analysis of a U.S. medical insurance dataset using only the Python standard library (no pandas or numpy required). The notebook (`us-medical-insurance-costs.ipynb`) demonstrates how to:

- Load a CSV file manually with `csv.DictReader`
- Store each column in simple Python lists for transparency
- Encapsulate repeated logic in a lightweight analysis class (`PatientsInfo`)
- Produce baseline descriptive summaries (age, charges, categorical counts)

The approach is intentionally minimal to reinforce core Python concepts before introducing data-analysis libraries.

## 2. Dataset

`insurance.csv` contains synthetic / de‑identified records commonly used for instructional purposes. Each row represents one insured individual.

Columns:
| Column    | Type   | Description |
|-----------|--------|-------------|
| age       | int    | Age in years |
| sex       | str    | Biological sex (`female` / `male`) |
| bmi       | float  | Body Mass Index (kg/m²) |
| children  | int    | Number of dependents covered |
| smoker    | str    | Smoking status (`yes` / `no`) |
| region    | str    | U.S. region (e.g. southwest) |
| charges   | float  | Annual medical insurance charges (USD) |

> Source attribution: This structure mirrors the widely circulated “Medical Cost Personal Datasets” (Kaggle) used in many introductory data analysis exercises.

## 3. Repository Structure

```
.
├── insurance.csv                 # Dataset (must be present to run the notebook)
├── us-medical-insurance-costs.ipynb  # Main exploratory notebook (pure Python)
├── README.md                     # Project documentation
└── LICENSE                       # License information
```

## 4. Core Design Choices

1. Lists instead of DataFrames: Emphasizes fundamental iteration, indexing, and aggregation logic.
2. Single loader function: Centralizes CSV reading; avoids redundant loops.
3. Deferred type conversion: Raw strings are only cast (to `int` / `float`) inside analytical methods—keeps ingestion simple.
4. Encapsulation with `PatientsInfo`: Groups related computations and keeps namespace clean.

## 5. Analysis Features Implemented

| Feature | Method / Section | Notes |
|---------|------------------|-------|
| Average age | `PatientsInfo.average_age()` | Converts age strings to `int` lazily |
| Average BMI | `PatientsInfo.average_bmi()` | Mean over float‑cast BMI values |
| Average dependents | `PatientsInfo.average_children()` | Simple mean of children counts |
| Smoker percentage | `PatientsInfo.smoker_percentage()` | Share of records marked `yes` |
| Smoker vs non-smoker cost ratio | `PatientsInfo.smoker_to_charge_ratio()` | Compares average charges |
| Average charge | `PatientsInfo.average_charge()` | Mean of annual charges |
| Sex distribution | `PatientsInfo.analyze_sexes()` | Returns count by category |
| Unique regions | `PatientsInfo.unique_regions()` | Returns a Python `set` |
| Full data dictionary | `PatientsInfo.create_dictionary()` | Aggregates parallel lists |
| Printed summary | `PatientsInfo.print_summary()` | Convenience multi-metric output |

## 6. Example (Conceptual) Output Snippet

```
Average Age: 39.2
Average BMI: 30.7
Average Number of Children: 1.1
Smoker Percentage: 20.4%
Smoker to Charge Ratio: 4.13
Average Charge: $13270.42
Unique Regions: {'northwest', 'southeast', 'southwest', 'northeast'}
```

Values will vary slightly if the dataset is modified.

## 7. Running the Notebook

Requirements: Python 3.9+ (any modern 3.x should work) and the standard library only.

On Windows PowerShell:

```powershell
python -m venv .venv
./.venv/Scripts/Activate.ps1
# (No external packages required)
python -c "import csv; print('Environment OK')"
```

Then open the notebook in VS Code / Jupyter and execute cells top-to-bottom.

If you prefer a script version, you can copy class + loader logic into a `.py` file and add a small `if __name__ == "__main__":` harness.

## 8. Extending the Analysis

Potential next steps (all doable first in pure Python; later with pandas for brevity):

- Age distribution: min / max / median / standard deviation
- Charges grouped by smoker status, region, number of children
- BMI categorization (e.g., underweight/normal/overweight/obese) vs average charges
- Correlation exploration (e.g., age vs charges, BMI vs charges)
- Outlier detection for unusually high medical charges
- Transition to pandas DataFrame for richer slicing and plotting

## 9. Transitioning to pandas (Optional)

Once comfortable with the manual approach, replicate the workflow in pandas:

```python
import pandas as pd
df = pd.read_csv('insurance.csv')
df.groupby('smoker')['charges'].mean()
```

This highlights how library abstractions collapse many custom loops into single expressions.

## 10. Testing Ideas (Lightweight)

Because logic is deterministic, you can add a simple test module (e.g., `test_patients_info.py`) asserting:

```python
def test_average_age():
	sample = PatientsInfo(['20','40'], ['male','female'], ['25','30'], ['0','1'], ['no','yes'], ['northwest','southwest'], ['1000','2000'])
	assert abs(sample.average_age() - 30.0) < 1e-9
```

## 11. Performance Considerations

The dataset is small (hundreds to low thousands of rows in typical versions). All operations are O(n) single passes over lists—sufficient without optimization.

## 12. Limitations

- No missing-value handling (assumes a clean CSV)
- No normalization for BMI or charge scaling
- Aggregations are unweighted; no time component considered
- `sex` kept binary as provided—does not model broader gender identity

## 13. License

See `LICENSE` in this repository for distribution terms. The underlying dataset is used for educational/demonstrative purposes; consult the original Kaggle source if redistributing.

## 14. Acknowledgments

- Educational inspiration from CodeCademy and common introductory data analysis exercises.
- Dataset structure aligns with the publicly available “Medical Cost Personal Datasets” (Kaggle).


