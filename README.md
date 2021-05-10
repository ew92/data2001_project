# data2001_project

Semester 1 2021 DATA2001 Project Assignment

Assignment Group F14 - 3

Eugene & Matt

## Brief Notes

### Aim
Integrate multiple datasets to produce a **bushfire risk score** that accounts for

### Datasets
* Census based datasets
  * Population density, Dwelling (`Neighbourhoods.csv`)
  * Dwelling (`StatisticalAreas.csv`)
  * Business locations (`BusinessStats.csv`)
* NSW RFS dataset
  * Vegetation & risk categories (`RFSNSW_BFPL.zip`)
* ABS Shape Files
  * *Yet to personally investigate* (`1270055001_mb_2016_nsw_shape.zip`)
More datasets can be integrated. Some ideas:
* Prevalence of waterways
* Some measure of moisture content in different areas
  * Source: [dataset](http://www.bom.gov.au/water/landscape/#/sm/Actual/day/-28.4/130.4/3/Point////2021/5/9/) [inspiration] (https://www.gislounge.com/fire-danger-reanalysis-dataset/)
*N.B. Not 100% sure which datasets align with which tasks. Need to take a closer look later.*

### Tasks

1. Build a PostgreSQL database that integrates `Neighbourhoods.csv`, `1270055001_mb_2016_nsw_shape.zip`, `StatisticalAreas.csv`, `BusinessStats.csv`, `RFSNSW_BFPL.zip` + 1 extra dataset (full points).
2. Risk Analysis
  * Compute **risk score** based on formula:
  `fire_risk=S(z(population_density)+z(dwelling_&_business_density)+z(bfpl_density)-z(assistive_serve_density))`
    * `S` is sigmoid
    * `z` is standard score
    *
  | Measure                   | Definition                                                      | Risk | Data Source        |
  |---------------------------|-----------------------------------------------------------------|------|--------------------|
  | population_density        | population divided by neighbourhood's land area                 | +    | Neighbourhoods.csv |
  | dwelling_density          | number of dwellings divided by neighbourhood land area          | +    | Neighbourhoods.csv |
  | business_density          | number of businesses divided by neighbourhood land area         | +    | BusinessStats.csv  |
  | bfpl_density              | area and category of BFPL divided by neighbourhood land area    | +    | RFSNSW_BFPL.shp    |
  | assistive_service_density | number of assistive services divided by neighbourhood land area | -    | BusinessStats.csv  |

  * Store computed measures and scores for each neighborhood. Create at least one index which is helpful for data integration or fire risk score computation.
  * Perform correlation analysis between **risk score** and ABS data on **median income & rent costs** in each neighborhood.
3. Documentation (Jupyter/Word/PDF, <=5pp+appendix)
  * Dataset description (data sources, how obtained, what preprocessing)
  * Database description (what schema - use diagram, what indexes and why)
  * Fire risk score analysis (write fire risk score formula, overview of fire risk results, preferred graphical representation on map)
  * Correlation analysis (Some correlation indicators, comparison to household incomes and rental prices for each region)
