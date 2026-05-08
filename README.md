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

#### Data Strategy and Context

This project draws on Lee (2025), "Electoral Turnover and Government Efficiency: Evidence from Federal Procurement" (*Journal of Politics* 87(2)), which proxies political connectedness using firms' campaign contribution patterns — specifically, whether a firm directed more than 60% of its total donations to the president's party. The Canadian institutional context requires a different operationalization. Federal contribution limits and disclosure norms differ substantially from the US, and the revolving-door phenomenon — the movement of personnel between government and the private sector — offers a more direct and observable structural proxy for political access in the Canadian federal procurement setting.

The central goal is to construct a binary firm-level indicator of *political connectedness*, defined by the presence of at least one individual linked to the firm who previously held a qualifying government, ministerial, political, regulatory, or procurement-related role.

#### Sources

| Source | Access | Purpose |
| --- | --- | --- |
| Registry of Lobbyists (Office of the Commissioner of Lobbying of Canada) | Public | Primary entry point: identify individuals registered to lobby on behalf of supplier firms |
| Investigative Journalism Foundation (IJF) revolving-door and lobbying databases | Public | Cross-reference personnel with documented government-to-private-sector transitions |
| LinkedIn (via Wharton Research Data Services / WRDS) | Wharton WRDS | Reconstruct individual employment histories; verify role titles, organizations, dates, and seniority |
| Public biographies and organizational websites | Public | Supplement LinkedIn for senior individuals where WRDS coverage is incomplete |
| GEDS (Government Electronic Directory Services) | Public | Verify and supplement current and recent federal government employment records |

#### Construction Procedure

1. Extract names of individuals registered to lobby on behalf of supplier firms from the OCL Registry of Lobbyists and the IJF revolving-door database.
2. Match each individual to their employment history via the WRDS LinkedIn dataset; supplement with public biographies and GEDS where coverage is incomplete.
3. For each individual, record: role title, organization, employment dates, and seniority level for all positions held prior to joining the supplier or lobbying firm.
4. Classify each prior role into one of the following categories: ministerial or political staff, elected official, senior public servant (EX-level or equivalent), policy adviser, regulator, procurement official, or registered lobbyist.
5. Match the timing of each prior government role to the party in power at the time, using federal election dates and parliamentary records.
6. Link the individual back to the corresponding supplier or lobbying firm using registration records and firm identifiers.
7. Code the firm as *politically connected* (binary: 1/0) if at least one associated individual satisfies the role classification criteria above.

#### Operationalization

A firm is coded as *politically connected* if at least one individual linked to it previously held a qualifying role. The timing dimension — matching role tenure to the party in power — permits a distinction between connections to the incumbent government versus prior administrations, paralleling Lee's (2025) use of directional contribution shares to differentiate president-aligned from opposition-aligned firms.

This coding does not establish causal influence. It constructs a systematic, observable proxy for political access, insider knowledge, and potential government networks — the structural conditions under which preferential contracting, if present, would be most likely to occur.

#### Limitations

The revolving-door proxy captures formal, documentable connections and will undercount informal networks. LinkedIn and GEDS coverage is incomplete, particularly for mid-level officials and individuals who left government before digital records were routine. These gaps introduce measurement error that would bias estimates toward zero, making any effects identified a conservative lower bound.

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
