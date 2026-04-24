 Aviation Accident Safety Analysis (1983–2023)

A data science project analysing 40 years of aviation accident records to identify the safest aircraft makes and models, and to understand how environmental and operational factors drive accident severity. Built to support data-driven decision-making for airlines, insurers, and fleet operators.


Project Overview.
The aviation industry accumulates decades of accident records that, when analysed rigorously, reveal meaningful patterns about aircraft safety. This project processes and analyses NTSB aviation accident data from 1983 to 2023 (filtered to professionally built airplanes) to surface actionable safety insights.
The analysis is split into two notebooks:
Aviation_Accident_Cleaning.ipynb; Data loading, filtering, imputation, feature engineering, and Aviation_Accident_Analysis.ipynb; Exploratory analysis, statistical testing, and visualisation

Business Problem
Airlines and insurers need objective, data-driven guidance for aircraft selection and risk assessment. This project answers that need by:

Identifying which aircraft makes and models are associated with the lowest fatal and serious injury rates
Quantifying which aircraft types are least likely to be completely destroyed in an accident
Quantifying how weather conditions and flight phase affect accident severity

Metric of success: Statistically reliable safety comparisons backed by sufficient sample sizes (≥ 50 incidents per make; ≥ 10 per model).

Research Questions

Which aircraft makes and models have the lowest injury and destruction rates?
What aircraft characteristics (make, model, engine type, number of engines) are associated with safer outcomes?
How does weather condition affect the severity of aviation accidents?
Which phase of flight is most associated with fatal or serious injuries?
Are larger (multi-engine) aircraft safer than smaller (single-engine) aircraft?


Repository Structure
Aviation_Accident_Cleaning.ipynb   # Data cleaning and feature engineering
Aviation_Accident_Analysis.ipynb   # EDA, statistical tests, visualisations
AviationData.csv                   # Raw source data (NTSB records, 1948–2023)
aviation_cleaned.csv               # Cleaned dataset output by the cleaning notebook
README.md

Dataset
Source: NTSB Aviation Accident Database (1948–2023)
Filtered scope: Professionally built airplanes, accidents from 1983 onwards
Each row represents a single accident event. Key variables:
Aircraft characteristics

Make — Manufacturer (e.g. Boeing, Cessna, Airbus)
Model — Specific aircraft model
Engine.Type — Propulsion system type
Number.of.Engines — Engine count (used to classify Small vs Large aircraft)

Accident outcomes

Total.Fatal.Injuries, Total.Serious.Injuries, Total.Minor.Injuries, Total.Uninjured
injury_rate (derived) — Proportion of occupants who suffered a fatal or serious injury
is_destroyed (derived) — Binary flag for complete aircraft destruction

Operational conditions

Weather.Condition — VMC (good visibility) or IMC (poor visibility)
Broad.phase.of.flight — Takeoff, Climb, Cruise, Approach, Landing, etc.
Purpose.of.flight — Commercial, private, instructional, etc.


Methodology
1. Data Cleaning (Aviation_Accident_Cleaning.ipynb)

Filtering: Retained only professional-build airplanes with accident dates from 1983 onward
Injury columns: NaN values imputed with 0 (absence of a recorded injury category is treated as zero); injury_rate and total_passengers derived from the four outcome columns
Aircraft damage: Unknown values replaced with NaN; binary is_destroyed flag derived
Make standardisation: Whitespace stripped, title-cased, and known aliases unified (e.g. Cirrus Design Corp → Cirrus); makes with fewer than 50 records dropped to ensure statistical reliability
Model column: Model labels were not unique across manufacturers, so a composite Make_Model key was created
Other columns: Ambiguous/sparse values in Engine.Type, Weather.Condition, Number.of.Engines, Purpose.of.flight, and Broad.phase.of.flight replaced with NaN; columns with fewer than 20,000 non-null values dropped

2. Analysis (Aviation_Accident_Analysis.ipynb)

Aircraft classified into Small (1 engine) and Large (2+ engines) size classes
Safety performance ranked by mean injury_rate and is_destroyed rate per make and model
Visualisations include horizontal bar charts, violin plots, strip plots, and box plots
Statistical significance tested with:

Chi-square test — weather condition vs. aircraft destruction
Mann-Whitney U test — VMC vs. IMC injury rate distributions
Kruskal-Wallis test — injury rate differences across flight phases




Key Findings
Aircraft Make — Small (Single-Engine)
Cessna offers the most statistically robust estimate due to its large sample. Maule and Bellanca lead on both metrics with meaningful sample sizes. Three specific models — Cessna 172SP, Diamond DA 20 C1, and Maule M-5-210C — recorded 0% injury rates across all logged accidents.
Aircraft Make — Large (Multi-Engine)
Boeing provides the single most statistically reliable large-aircraft estimate (n=398). Boeing 777 (μ=0.08%) and Boeing 757 (μ=0.20%) are the top model-level performers. The Bombardier CRJ (CL-600-2B19) follows at 0.41%.
Weather Condition
IMC (poor visibility) accidents are dramatically more deadly than VMC accidents:

VMC median injury rate: 0% — most VMC accidents produce no fatal/serious injuries
IMC median injury rate: 100% — in over half of IMC accidents, every occupant was killed or seriously injured
Chi-square (weather vs. destruction): χ²=859.9, p=5.2×10⁻¹⁸⁹
Mann-Whitney U (VMC < IMC injury rate): p=1.4×10⁻¹⁶⁵

Phase of Flight
Injury rate follows the physical logic of kinetic energy at impact:
Landing is the most common accident phase but by far the most survivable. High-energy phases (Maneuvering, Climb) carry the highest risk. Kruskal-Wallis across all phases: H=348.1, p=1.6×10⁻⁶⁹.

Technologies Used

Python 3
pandas — data loading, cleaning, aggregation
NumPy — numerical operations and derived feature construction
Matplotlib — bar charts, grouped plots
Seaborn — violin plots, strip plots, box plots
SciPy — chi-square, Mann-Whitney U, Kruskal-Wallis hypothesis tests
