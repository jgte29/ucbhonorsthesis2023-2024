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
1. Data Retrieval
   -  *Insert Text Here*
2. Exploratory Data Analysis
   - Temporal & Spatial Aggregation
   - Feature Engineering
3. Modeling
   - Model A:
   - Model B:
   
