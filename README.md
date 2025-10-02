# FBI Crime Data Reporting and NIBRS Adoption Rate Analysis

This repository contains an exploratory data analysis of FBI agency-level reporting and the adoption rate of the National Incident-Based Reporting System (NIBRS) across U.S. law enforcement agencies. The analysis investigates how agency types vary across states and the proportion of agencies in each state that report via NIBRS, along with trends in NIBRS adoption over time.

## Research Question

- How do agency types vary across different states in the USA?
- What percentage of agencies in each state participate in NIBRS reporting?
- Are there observable trends in NIBRS adoption over time?

## Dataset

The dataset used in this analysis is sourced from the public TidyTuesday collection (FBI Crime data via the Crime Data Explorer). The primary file in this repo is `data/agencies.csv` and contains agency-level records for agencies that have submitted data to the FBI's Uniform Crime Reporting (UCR) program.

Key variables include:

- `ori`: Unique ID for the agency
- `county`: County of jurisdiction
- `latitude`, `longitude`: Approximate geographic location of the agency
- `state_abbr`, `state`: State code and name
- `agency_name`: Official agency name
- `agency_type`: Category such as City, County, etc.
- `is_nibrs`: Boolean indicating NIBRS participation
- `nibrs_start_date`: Date the agency began reporting to NIBRS

## Data cleaning and preprocessing (summary)

- Missing latitude/longitude values were imputed using state-level averages to preserve geographic coverage.
- Invalid latitude entries were filtered out (latitude <= 0).
- Missing `agency_type` values were inferred from `agency_name` using simple heuristics (e.g., names containing "Sheriff" classified as "County", "Police" as "City", and others as "Other").
- `nibrs_start_date` was parsed to datetime and missing dates were filled using the dataset median start date.

The approach aimed to minimize data loss (dropping rows would remove ~29% of rows with any missing data) and preserve analysis power.

## Exploratory Data Analysis and Visualizations

The main notebook `FBI_Crime_Data_Analysis.ipynb` performs the following analyses and produces visual outputs:

- Distribution of agency types by state (stacked bar chart)
- Overall distribution of agency types (pie chart)
- NIBRS participation rates by state (bar chart showing % of agencies participating)
- Trend of NIBRS adoption over time (time series of agencies adopting by year)
- NIBRS participation by agency type (bar chart)
- Interactive map of agencies (folium) with markers colored by NIBRS participation and clustered for performance; the map is also available as `nibrs_map.html`.

These visualizations help answer the research questions and highlight geographic and temporal patterns in adoption.

## Files in this repository

- `FBI_Crime_Data_Analysis.ipynb` — Main analysis notebook (contains code, text, and plots).
- `data/agencies.csv` — Agency-level dataset used in the notebook.
- `nibrs_map.html` — Exported interactive folium map of agency locations and NIBRS participation.
- `FBI Crime Data Reporting and NIBRS Adoption Rate Analysis.pdf` / `.docx` — Project report and write-up (long-form description and results).
- `NIBRS Adoption Rate Analysis.pptx` — Presentation summarizing findings.
- `LICENSE` — License file for the repository.

## Reproducing the analysis

1. Create (or activate) a Python environment with Python 3.7+.

2. Install dependencies. Example (recommended to run inside the environment):

```powershell
pip install pandas numpy matplotlib plotly folium
```

3. Open `FBI_Crime_Data_Analysis.ipynb` in Jupyter Notebook, JupyterLab, or VS Code and run the cells top-to-bottom to reproduce the figures and the map.

4. The interactive folium map will render in the notebook; to export/open it in a browser, open `nibrs_map.html`.

## Outputs and deliverables

- Notebook with cleaned data, analysis, and figures (`FBI_Crime_Data_Analysis.ipynb`).
- Interactive map of agency locations with NIBRS participation markers (`nibrs_map.html`).
- Written report (`FBI Crime Data Reporting and NIBRS Adoption Rate Analysis.pdf`) and presentation (`NIBRS Adoption Rate Analysis.pptx`).

## Notes and possible next steps

- Perform more rigorous geocoding or external validation for agencies lacking coordinates.
- Explore demographic or crime-rate correlations with NIBRS adoption (e.g., population, agency size, local crime rates).
- Build an automated pipeline to fetch latest CDE/TidyTuesday snapshots and update the analysis.

## License

See `LICENSE` for license details.
