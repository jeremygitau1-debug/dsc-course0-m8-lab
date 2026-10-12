# Aviation Accident Analysis

An analysis of aviation accident data (1983 onwards) for an airline/airplane insurer. The goal is to find which airplane makes and models have a low rate of total destruction and a low likelihood of fatal or serious injuries when an accident happens, with separate recommendations for small aircraft and larger passenger aircraft (more than 20 people on board).

## Repository contents

| File | Description |
|---|---|
| `Aviation_Accidents_Cleaning.ipynb` | Loads and inspects the raw data, cleans it, builds the key measures and saves the cleaned data |
| `Aviation_Accidents_Data_Analysis.ipynb` | Exploratory analysis, make and model comparisons, and the effect of weather and phase of flight |
| `AviationData.csv` | Raw accident data (1948-2022) |
| `USState_Codes.csv` | US state names and abbreviations (not used in the analysis) |
| `Aviation_Data_Cleaned.csv` | Output of the cleaning notebook, used by the analysis notebook |
| `LICENSE.txt` | Apache 2.0 licence |

## How to run

1. Install Python 3 with `pandas`, `numpy`, `matplotlib`, `seaborn` and `scipy`.
2. Run `Aviation_Accidents_Cleaning.ipynb` from top to bottom. It creates `Aviation_Data_Cleaned.csv`.
3. Run `Aviation_Accidents_Data_Analysis.ipynb` from top to bottom.

## Data cleaning summary

- Kept events from 1983 onwards (assuming a 40-year maximum lifetime for a make/model), accident investigations only, and professionally built aircraft only.
- Imputed the aircraft category from other records with the same make and model, then kept airplanes only.
- Estimated the number of people on board from the injury columns and built two measures:
  - **Fatal/serious fraction** = (fatal + serious injuries) / people on board
  - **Destroyed**, a 1/0 flag for whether the aircraft was destroyed
- Standardised make names (for example merging `CESSNA AIRCRAFT CO` into `CESSNA`), kept makes with at least 50 accidents, and built a unique `Plane.Type` from make + model.
- Cleaned the weather, engine, purpose and phase-of-flight columns, and dropped columns that were more than 50% empty.

Final dataset: 54,990 accidents.

## Key findings

**Small aircraft**
- Maule, Stearman, Stinson, Aviat and Diamond combine low fatal/serious fractions or low destroyed rates with a few hundred accidents of evidence. Maule has a mean fraction of 0.157 vs 0.278 for other small makes.
- Cessna is the best of the high-volume makes.
- Best-supported models: Maule M-4-220C and M-7-235, Stearman E75, Stinson 108-1, Great Lakes 2T-1A-2 and Weatherly 201B.

**Large aircraft**
- McDonnell Douglas (0.076) and Bombardier (0.104) have the lowest fatal/serious fractions, with Boeing as a large-sample benchmark (0.190).
- Models with the lowest fractions: McDonnell Douglas MD-88 and MD-11, Bombardier CL-600-2B19, and Boeing 727-200, 737-300 and 747. Older Boeing 737-200 and 737-400 models were the weakest.
- Only eight large makes have enough accidents to compare, so these rankings are suggestive.

**Other factors**
- **Weather:** accidents in instrument conditions (IMC) are far more severe than in visual conditions (fatal/serious fraction 0.677 vs 0.224; 59% vs 17% of aircraft destroyed).
- **Phase of flight:** maneuvering, climb and cruise accidents are the most severe, while landing and taxi accidents are mostly survivable.

## Limitations

The data contain accidents only, with no flight hours or fleet sizes, so the results describe how severe an accident is likely to be, not how likely an accident is.
