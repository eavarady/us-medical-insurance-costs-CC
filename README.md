# us-medical-insurance-costs-CC

## Overview

This notebook explores a dataset of U.S. medical insurance records and summarizes patterns across demographic and lifestyle attributes. The analysis organizes the raw CSV data into Python lists and encapsulates common computations in a small utility class.

The dataset (insurance.csv) contains the following columns:
- age (years)
- sex (female/male)
- bmi (body mass index)
- children (number of dependents)
- smoker (yes/no)
- region (U.S. region)
- charges (annual medical insurance cost in USD)

Results include an average patient age, counts by sex, the set of unique regions represented, and an average annual insurance charge. A consolidated patient dictionary is also produced to facilitate later exploration.
