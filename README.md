# Rainfall Analysis and Planting Advisory

**Author:** Chala Wakshuma

## Project summary

A farmer-support NGO sends SMS advice on planting windows to farmers in five counties (Nairobi, Nakuru, Kisumu, Mombasa and Machakos). It has monthly rainfall readings from local weather stations, but the Machakos data was typed in by hand and contained errors. This project cleans that data, analyses the rainfall patterns with NumPy (annual totals, monthly averages, wettest months, dry months and the best two-month planting window per county), saves a summary to `rainfall_summary.csv`, and ends with a short planting advisory.

## How to run

**In Google Colab (no setup):** [![Open In Colab](https://colab.research.google.com/assets/colab-badge.svg)](https://colab.research.google.com/github/Chala-prog/plp-da-a2-rainfall-advisory/blob/main/rainfall_analysis.ipynb), then choose **Runtime > Restart session and run all**.

**Locally:**
```bash
pip install -r requirements.txt notebook
jupyter notebook rainfall_analysis.ipynb      # then Kernel > Restart & Run All
```
Running the notebook recreates `rainfall_summary.csv` in the same folder. Only `numpy` and Python's built-in `csv` module are used.

## Planting advisory

- Plant in **April–May** in Nairobi (395 mm), Nakuru (265 mm), Kisumu (420 mm) and Mombasa (390 mm), the two-month window with the most combined rainfall in each county, and send the SMS advice about a month earlier, in March.
- Machakos is different: its best window is **November–December** (278 mm) and not April–May, so its advice should go out in October, with drought-tolerant crop guidance because it has 6 dry months (below 50 mm).
- Treat the Machakos advice as **provisional**: two of its twelve readings (April and September) were unreadable and were estimated at 68 mm (about 17% of its 811 mm annual total), and all counties are based on a single year of data.

## Results

| County | Annual total (mm) | Wettest month | Dry months (<50 mm) | Planting window |
| --- | ---: | --- | ---: | --- |
| Nairobi | 1,045 | Apr | 4 | Apr-May |
| Nakuru | 916 | Apr | 3 | Apr-May |
| Kisumu | 1,371 | Apr | 0 | Apr-May |
| Mombasa | 1,075 | May | 2 | Apr-May |
| Machakos | 811 | Nov | 6 | Nov-Dec |

## Files

| File | What it is |
| --- | --- |
| `README.md` | This file |
| `rainfall_analysis.ipynb` | The full analysis (Tasks 1 to 8), with all outputs visible |
| `rainfall_summary.csv` | One row per county: `county, annual_total_mm, wettest_month, dry_months, planting_window` |
| `requirements.txt` | Python libraries needed (`numpy`) |

## How the Machakos row was cleaned

Each raw value is converted with `int()` inside `try/except ValueError`. `" 20 "` (extra spaces) is a valid number and is kept as 20; `"N/A"` and the empty string are invalid. The two invalid months (April and September) are filled with 68 mm, the rounded average of the ten valid readings (67.5). The notebook's *Data Quality Notes* section explains why this is only an estimate and how much it could affect the results.
