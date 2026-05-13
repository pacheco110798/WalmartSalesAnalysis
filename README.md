# Walmart Sales Analysis

## Project Overview

This project analyzes Walmart weekly sales data using advanced data analysis and feature engineering techniques with Python, Pandas, and Seaborn.

The workflow includes:

- Memory optimization using aggressive downcasting
- Multi-table data merging
- Time series feature engineering
- Lag variable creation
- Multivariable storytelling with FacetGrid
- KPI generation for store performance evaluation

---

# Dataset Files

The project uses three CSV files:

- `train.csv`
- `stores.csv`
- `features.csv`

---

# Objectives

## 1. Memory Optimization

Performed aggressive downcasting to reduce memory usage by:

- converting `int64` → smaller integer types
- converting `float64` → `float32`
- converting low-cardinality `object` columns → `category`

### Result

The final merged DataFrame uses less than 50% of the original memory consumption.

---

# 2. Data Merging

Created a unified **Master DataFrame** by combining:

- sales data (`train.csv`)
- store metadata (`stores.csv`)
- macroeconomic variables (`features.csv`)

# Missing Values Strategy

The `MarkDown` columns contained null values.

### Decision

Null values were replaced with `0` because:

- missing markdowns usually indicate no active promotion,
- using median imputation would distort promotional behavior.
- 
---

# 3. Time Intelligence

Converted `Date` into datetime format and extracted:

- Year
- Month
- Week of Year
- Quarter

### Lag Feature

Created:

```python
Venta_Semana_Anterior
```

This variable stores the previous week's sales for each:

- Store
- Department

using:

```python
groupby().shift(1)
```

---

# 4. Multivariable Storytelling

Used `FacetGrid` to analyze:

- `Fuel_Price`
- `Weekly_Sales`
- `Type`
- `IsHoliday`

### Visualization

Each panel represents a store type:

- A
- B
- C

Color (`hue`) differentiates holiday vs non-holiday weeks.

---

# Findings

The regression trend was almost flat across all store types.

### Interpretation

- Fuel price has weak correlation with weekly sales.
- Store type C does not appear significantly more sensitive to fuel prices than type A.
---

# 5. Feature Engineering — Store Efficiency KPI

Created a performance metric called:

```python
Store_Efficiency
```

### Methodology

1. Calculated average sales per store.
2. Compared each week against the same week from the previous year.
3. Classified weeks as:
   - `Outperformer`
   - `Underperformer`

using a 52-week lag.

---

# Holiday Performance Pivot Table

Calculated the percentage of outperforming weeks during holidays.

## Results

| Type | % Outperformer |
|---|---|
| A | 74.57% |
| B | 74.31% |
| C | 73.55% |

---

# Technologies Used

- Python
- Pandas
- NumPy
- Seaborn
- Matplotlib

---

# Project Structure

```text
project/
│
├── train.csv
├── stores.csv
├── features.csv
├── walmart_analysis.ipynb
└── README.md
```
