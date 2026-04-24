Aircraft Safety Analysis for Insurance Risk Assessment

Project Overview

This project analyzes historical aviation accident data (1948–2023) to identify aircraft makes and models associated with lower risks of catastrophic failure and passenger injury.

The goal is to support airlines and insurance companies in making **data-driven decisions about aircraft safety, risk exposure, and operational reliability.

The dataset was filtered to focus on **modern, professionally built aircraft (1983 onwards)** to ensure relevance to current aviation standards.


Problem Statement

The aviation industry experiences occasional accidents that result in aircraft destruction and passenger injuries or fatalities. Insurance companies and airlines need to understand:

- Which aircraft makes/models are safest?
- What operational conditions increase risk?
- Which aircraft types are more resilient in accidents?

This project aims to identify key factors that influence aircraft safety outcomes using historical accident data.

 Dataset Overview

The dataset contains aviation accident records including:

- Aircraft details (make, model, engine type, number of engines)
- Accident outcomes (fatal, serious, minor injuries, uninjured passengers)
- Operational conditions (weather, flight phase, purpose of flight)
- Aircraft damage classification

Filters Applied:
- Only Airplane category included
- Only professional builds (Amateur.Built = No)
- Only accidents from 1983 onwards
- Removed columns with fewer than **20,000 non-null values**

Data Cleaning & Feature Engineering

The following preprocessing steps were performed:

Data Cleaning:
- Handled missing values in injury-related columns
- Standardized text fields (Make, Model, Weather, etc.)
- Removed irrelevant or low-quality columns
- Filtered dataset for modern aircraft (1983–2023)

Feature Engineering:
- total_passengers - sum of all injuries and uninjured passengers
- injury_rate - proportion of serious + fatal injuries
- is_destroyed - binary indicator of aircraft destruction
- aircraft_type - combination of Make + Model

 Key Findings (Summary)

Aircraft Safety by Make/Model
- Certain large commercial aircraft manufacturers show **lower injury rates on average**
- Smaller general aviation aircraft show **higher variability in safety outcomes**

Weather Impact
- Poor weather conditions are associated with **higher accident severity**
- Visual Meteorological Conditions (VMC) show lower injury severity on average

Flight Phase Risk
- Takeoff and landing phases show the **highest accident severity**
- Cruise phase accidents tend to be less severe

Aircraft Characteristics
- Multi-engine aircraft tend to show **slightly improved survival outcomes**
- Aircraft design and manufacturer significantly influence safety performance

---

Final Recommendations

Safer Large Aircraft Categories (based on observed trends)
- Boeing 737 series
- Airbus A320 family

Safer Small Aircraft Categories (if supported by data)
- Cessna 172 series (general aviation training aircraft)

Higher Risk Conditions
- Adverse weather (IMC conditions)
- Takeoff and landing phases
- Small single-engine aircraft in private operations


Visualizations Used

- Injury rate by aircraft make
- Aircraft destruction rate by model
- Weather conditions vs accident severity
- Flight phase vs injury outcomes

 Limitations

- Missing data in historical records may affect accuracy
- Reporting standards may vary across time periods
- Injury severity is sometimes incomplete or estimated
- Some aircraft models have limited sample sizes

 Conclusion

This analysis provides insights into aircraft safety performance based on historical accident data. The findings can help insurers and airlines assess risk exposure and make informed decisions about aircraft selection and operational safety strategies.

 Technologies Used

- Python
- Pandas
- NumPy
- Matplotlib
- Seaborn


## 📁 Repository Structure
