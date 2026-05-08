# Project Title

## Overview

This paper [...]

## File Structure

The repo is structured as follows (change as needed):

### `data/`
-   `00-simulated_data` contains simulated data used to test the analysis pipeline.
-   `01-raw_data` contains the raw data as obtained from [City of Toronto Open Data](https://open.toronto.ca/).
-   `02-analysis_data` contains the cleaned datasets that were constructed.
-   `03-table_data` contains formatted data tables used to generate Quarto outputs.

#### Data Strategy

This project draws on Lee (2024), "Electoral Turnover and Government Efficiency: Evidence from Federal Procurement," and focuses on constructing a proxy for political connectedness among federal procurement suppliers.

#### Sources

| Source | Purpose |
| --- | --- |
| Registry of Lobbyists / revolving-door records | Identify individuals registered to lobby on behalf of supplier firms |
| LinkedIn and public biographies | Reconstruct individual employment histories (roles, dates, seniority, organization) |
| GEDS (Government Electronic Directory Services) | Verify and supplement government employment records |

#### Construction Procedure

1. Extract names of individuals linked to supplier firms from revolving-door and lobbying records.
2. Search each individual's LinkedIn profile or public biography to reconstruct their prior employment history.
3. Record role title, organization, dates held, and seniority level.
4. Classify each prior role into one of the following categories: ministerial staff, elected office, senior public servant, policy adviser, regulator, procurement official, or lobbyist.
5. Match the timing of each government role to the party in power at the time.
6. Link the individual back to the corresponding supplier or lobbying firm.
7. Code the firm as politically connected if at least one associated individual held a qualifying role.

#### Operationalization

A firm is coded as *politically connected* if at least one individual linked to it previously held a government, ministerial, political, regulatory, or procurement-related role. Revolving-door and lobbying records serve as the primary entry point; LinkedIn, public biographies, and GEDS are used to fill in and verify employment histories. This coding does not establish causal influence — it provides a systematic proxy for political access, insider knowledge, and potential government networks.

### `scripts/`  
-   `00.0-run_pipeline.py` executes the entire data processing pipeline from simulation to final outputs.
-   `01.0-simulate_data.py` generates synthetic datasets to test logic.
-   `01.1-simulated_data_test.py` tests the structure of the simulated data.
-   `02.0-download_data.py`  downloads the raw neighbourhood crime counts (2019–2024) and Census socioeconomic indicators (2021) from the City of Toronto's Open Data Portal.
-   `03.0-clean_crime_data.py` preprocesses the raw crime data.
-   `03.1-clean_profile_data.py` preprocesses the raw Census data.
-   `04.0-merge_crime_profile.py` join the cleaned crime and profile datasets on neighbourhood identifiers.
-   `04.1-merged_test.py` tests the structure of the simulated data
-   `05-0-eda_neighbourhood_clusters.py` performs exploratory data analysis on socioeconomic proxies, calculates descriptive statistics, and inspects clustering diagnostics.
-   `06.0-table_crime_clusters.py` aggregates annual crime rates by cluster (Low-, Medium-, High-Opportunity) and exports formatted tables.
-   `07.0-plot_crime_clusters.py` creates visualizations of crime trajectories over time for each cluster.
-   `08.0-model_evaluation.py` compares clustering algorithms (K-means vs. Gaussian Mixture Models) using metrics Silhouette Score, Davies–Bouldin Index, and Calinski–Harabasz Score.

### `paper/` 
-   `paper.qmd` Quarto manuscript.  
-   `references.bib` Citations. 
-   `paper.pdf` Compiled PDF.  
-   `fonts/` LaTex font assets (CM Serif).
-   `styles/` APA 7 style formatting for Quarto.  

### `other/`
-   Supplementary materials including figures, literature, notes, and development sketches.

## Statement on LLM usage

This project was developed with the assistance of LLMs. 

**1. AI-assisted code completion** (e.g., GitHub Copilot, Qodo Gen) was used throughout development.  
   - Error messaging and debugging within selected scripts;  
   - Refining mathematical notation and function documentation;  
   - Formatting the Quarto manuscript.

## Pre-requisites
-   Install required Python packages as specified in `uv.lock`.  
-   Run all tests with `pytest`.

## Acknowledgements
- [...]
