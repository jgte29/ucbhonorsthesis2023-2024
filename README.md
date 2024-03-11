# Impact Analysis of the Chesa Boudin Administration

Jordan G. Taqi-Eddin

University of California - Berkeley

CDSS Data Science Honors Program 2024

## Overview
The ousting of Chesa Boudin as the district attorney of San Francisco was fueled by claims of lenient prosecutorial policies and rising crime rates. Yet, there is limited empirical research validating these accusations against Boudin. Employing a regression discontinuity design (RDD), my analysis reveals that under the Boudin administration, there was a notable 36% reduction in monthly prosecutions and a 21% decrease in convictions across all crimes. Furthermore, successful monthly case diversions surged by 58%. For violent crimes during Boudin's tenure, the San Francisco District Attorney's office experienced a 36% decline in monthly prosecutions, a 7% drop in convictions, and a significant 47% increase in successful case diversions. Notably, the dip in monthly convictions for violent crimes did not reach statistical significance. While I did observe a potential causal link between fewer prosecutions and heightened criminal activity, these findings fell short of statistical significance. In conclusion, utilizing machine learning algorithms like neural networks and k-nearest neighbors, as substitutes for ordinary least squares regression in estimating the reduced form equation, may potentially reduce the standard errors of the parameters in the structural equation. Nevertheless, further research is imperative to validate these promising initial results in this space.

## Accessing the Repository
1. Clone the repository on your local device:
   ```bash
   git clone https://github.com/jgte29/ucbhonorsthesis2023-2024.git
2. Repository Structure:
   ```
   └───analysis
      ├───ic_data
         ├───ica_by_month_master.csv
         ├───icv_by_month_master.csv
         ├───ic_noqol_by_month_master.csv
         ├───incident_counts_a_master.csv
         ├───incident_counts_by_crime_master.csv
         └───incident_counts_v_master.csv
      ├───model_performances
         ├───first_stage_mses.csv
         ├───ica_c1_knn_model_performance.csv
         ├───ica_c1_nn_model_performance.csv
         ├───ica_c2_knn_model_performance.csv
         ├───ica_c2_nn_model_performance.csv
         ├───icnoqol_c1_knn_model_performance.csv
         ├───icnoqol_c1_nn_model_performance.csv
         ├───icnoqol_c2_knn_model_performance.csv
         ├───icnoqol_c2_nn_model_performance.csv
         ├───icv_c1_knn_model_performance.csv
         ├───icv_c1_nn_model_performance.csv
         ├───icv_c2_knn_model_performance.csv
         └───icv_c2_nn_model_performance.csv
      ├───regressions
         ├───log_conviction_regressions.csv
         ├───log_incident_tots_regressions.csv
         ├───log_incident_tots_regressions_kmeans.csv
         ├───log_incident_tots_regressions_nn.csv
         ├───log_prosecutions_lag1_regressions.csv
         ├───log_prosecutions_regressions.csv
         └───log_successful_diversion_regressions.csv
      └───sf_data
         ├───Case_Resoultions_All_Crimes.csv
         ├───Case_Resoultions_Violent_Crimes.csv
         ├───DA_Actions_On_Arrests_All_Crimes.csv
         ├───DA_Actions_On_Arrests_Violent_Crimes.csv
         ├───District_Attorney_Cases_Prosecuted.csv
         └───Outcomes_of_SFPD_Incidents_All_Crimes.csv
   ```

## Data Processing Pipeline
1. Data Retrieval <br>
   In my analysis, I depend on three distinct data sources: information on SFDA case actions, SFPD incident reports, and geospatial data for San Francisco neighborhoods.
   - <u>SFDA Case Actions</u>: <br>
      The San Francisco case actions dataset is generated and overseen by the city's open data portal, DataSF. When the SFDA files charges against a defendant, relevant data is manually entered into the District Attorney Office's case management system. Approximately on a weekly basis, reports are extracted from this system, undergo cleaning and anonymization processes, and are subsequently integrated into the DataSF portal. Covering cases from January 2014 to the present, the dataset comprises information on over 100 thousand cases presented to the District Attorney's Office. It specifically includes cases where the office initiated prosecution by filing new criminal charges or submitting a motion to revoke probation or parole (MTR). Cases handled by the San Francisco Adult Probation Department or the state Division of Adult Parole Operations, which initiate a motion to revoke, are not included. In instances of new criminal charges, the most serious offense type is designated as the primary offense for prosecution by the SFDA. For MTR cases, the categorization is based on the initial prosecution, as filing an MTR indicates a pursuit of a new sanction within the sentence of a prior criminal conviction, rather than filing new charges for the latest offense. The filing date for MTRs is determined by the date when the SFDA filed the MTR for the new arrest.
   - <u>SFPD Incident Reports</u>: <br>
      The dataset includes incident reports documented since January 1, 2018. These reports are recorded by law enforcement officers or through self-reporting by the public, utilizing the San Francisco Police Department's online reporting system. Reports are categorized based on the method of submission and the incident's nature. These categories encompass initial reports, signifying the first filing for a specific incident; coplogic reports, denoting online submissions by the public; and vehicle reports, covering incidents related to stolen and/or recovered vehicles. Subject to daily updates, the data is added to the open dataset only after undergoing review and approval by a supervising Sergeant or Lieutenant. Removal of incident reports from the dataset may occur due to compliance with court orders to seal records or for administrative reasons, such as ongoing internal affairs investigations or criminal inquiries.
   - <u>SF Neighborhoods</u>: <br>
      The creation of this dataset involved associating 2010 Census tracts with neighborhoods according to established definitions by the Planning Department and the Mayor’s Office of Housing and Community Development. A qualitative assessment determines the suitable neighborhood for each tract based on factors such as population distribution and landmarks. The dataset remains static, and any alterations to analysis neighborhood boundaries undergo evaluation by the Analysis Neighborhood working group. Led by DataSF and the Planning Department, this group incorporates input from various city departments, making updates as necessary. I exclusively utilize the geospatial data within this dataset when generating year-to-year crime prevalence plots for neighborhoods.
2. Exploratory Data Analysis
   - Temporal & Spatial Aggregation
      - <u>SFDA Case Actions</u>: <br>
      Every entry in the San Francisco case actions dataset corresponds to a particular action executed by the district attorney's office for an individual case involving a defendant. My analysis focuses on crimes with arrest dates spanning from January 1, 2014, to December 31, 2023.
      - <u>SFPD Incident Reports</u>: <br>
   - Feature Engineering
3. Modeling
   - Model A:
   - Model B:
   
