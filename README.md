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
   - <ins>SFDA Case Actions</ins>: <br>
      The San Francisco case actions dataset is generated and overseen by the city's open data portal, DataSF. When the SFDA files charges against a defendant, relevant data is manually entered into the District Attorney Office's case management system. Approximately on a weekly basis, reports are extracted from this system, undergo cleaning and anonymization processes, and are subsequently integrated into the DataSF portal. Covering cases from January 2014 to the present, the dataset comprises information on over 100 thousand cases presented to the District Attorney's Office. It specifically includes cases where the office initiated prosecution by filing new criminal charges or submitting a motion to revoke probation or parole (MTR). Cases handled by the San Francisco Adult Probation Department or the state Division of Adult Parole Operations, which initiate a motion to revoke, are not included. In instances of new criminal charges, the most serious offense type is designated as the primary offense for prosecution by the SFDA. For MTR cases, the categorization is based on the initial prosecution, as filing an MTR indicates a pursuit of a new sanction within the sentence of a prior criminal conviction, rather than filing new charges for the latest offense. The filing date for MTRs is determined by the date when the SFDA filed the MTR for the new arrest.
   - <ins>SFPD Incident Reports</ins>: <br>
      The dataset includes incident reports documented since January 1, 2018. These reports are recorded by law enforcement officers or through self-reporting by the public, utilizing the San Francisco Police Department's online reporting system. Reports are categorized based on the method of submission and the incident's nature. These categories encompass initial reports, signifying the first filing for a specific incident; coplogic reports, denoting online submissions by the public; and vehicle reports, covering incidents related to stolen and/or recovered vehicles. Subject to daily updates, the data is added to the open dataset only after undergoing review and approval by a supervising Sergeant or Lieutenant. Removal of incident reports from the dataset may occur due to compliance with court orders to seal records or for administrative reasons, such as ongoing internal affairs investigations or criminal inquiries.
   - <ins>SF Neighborhoods</ins>: <br>
      The creation of this dataset involved associating 2010 Census tracts with neighborhoods according to established definitions by the Planning Department and the Mayor’s Office of Housing and Community Development. A qualitative assessment determines the suitable neighborhood for each tract based on factors such as population distribution and landmarks. The dataset remains static, and any alterations to analysis neighborhood boundaries undergo evaluation by the Analysis Neighborhood working group. Led by DataSF and the Planning Department, this group incorporates input from various city departments, making updates as necessary. I exclusively utilize the geospatial data within this dataset when generating year-to-year crime prevalence plots for neighborhoods.
2. Exploratory Data Analysis
   - Temporal & Spatial Aggregation
      - <ins>SFDA Case Actions</ins>: <br>
      Every entry in the San Francisco case actions dataset signifies a distinct action carried out by the district attorney’s office on a particular case involving a defendant. The temporal scope of my analysis is confined to crimes with arrest dates ranging from January 1, 2014, to December 31, 2023. Due to the dataset's detailed granularity, I aggregate the data on a monthly basis. The aggregations are conducted based on arrest dates rather than the dates of SFDA actions since the latter information is not available in the dataset.
      - <ins>SFPD Incident Reports</ins>: <br>
         Similar to the detailed granularity of the SFDA case actions dataset, the SFPD incident reports dataset also necessitates monthly temporal aggregation. Moreover, for visualization purposes, I conduct yearly aggregations across various San Francisco neighborhoods. This approach allows me to depict the year-to-year trends in crime prevalence for each neighborhood.
   - Feature Engineering
   - <ins>SFDA Case Actions</ins>: <br>
      In obtaining synthetic treatment and time-fixed effects for my analysis, I employed various methods. The development of the monthly time-fixed effect was straightforward, as it naturally emerged during the temporal aggregation process. However, acquiring the time-fixed effect associated with the COVID-19 pandemic and the indicator for Chesa Boudin being in office demanded a more nuanced approach. To account for the COVID-19 pandemic, I adopted two different strategies. The first involved a simple cutoff at March 2020, marking the commencement of Shelter-In-Place Orders in California (Friedson et al., 2021). The second approach utilized a timeframe from March 2020 to the end of 2021, aligning with the literature suggesting the transition of COVID-19 to its endemic phase by the close of 2021 (Ioannidis, 2022). As SFDA action dates were unavailable in the case actions dataset, I implemented a lagging strategy to approximate when these actions occurred. Calculating the average Median Number of Days from Arrest to Conviction for the period from 2020 to 2022 revealed approximately 307 days (10 months) for all crimes and 426 days (14 months) for the subset of violent crimes. Consequently, for cases with arrest dates toward the end of Boudin's tenure, it was improbable that any conviction or successful diversion took place during his administration. Thus, the cutoffs for case actions under the Boudin administration are lagged by 10 and 14 months in the datasets for all crimes and violent crimes, respectively.
   - <ins>SFPD Incident Reports</ins>: <br>
      In incorporating month and COVID time-fixed effects, I apply a strategy parallel to the one used for the SFDA case actions dataset. However, for the synthetic treatment, I choose not to use lagging, adopting a similar approach to the one employed when analyzing prosecutions in the case actions dataset. <br>
   <ins>**Note**</ins> For more detailed information on the temporal aggregation and feature engineering for the datasets I use in my analysis, refer to the **Data** section of my paper.
3. Modeling
   - Regression Discontinuity Design Model:
      - (1) \hspace{0.25cm} \(Y_{m,t} = \beta_{0} + \beta_{1} \times \mathbb{1}(Boudin)_{m,t} + \mu_{m} + \pi_{m,t} + \epsilon_{m,t}\)
      - $Y_{m,t} \text{ = Dependent Variable in month m during year t}$
      - $Boudin_{m, t} \text{ = Binary Indicator for whether Chesa Boudin was in office during month m in year t}$
      - $\mu_{m} \text{ = Monthly Fixed-Effects}$
      - $\pi_{m, t} \text{ = COVID Pandemic Fixed-Effect; Either } COVID_1 \text{ or } COVID_2$
      - $COVID_1 \text{ = COVID using simple cuttoff at the start of the CA Shelter-In-Place-Orders, March 2020}$
      - $COVID_2 \text{ = COVID using a range from March 2020 to the end of 2021, when the virus became endemic}$
   - 2SLS Model:
4. References:
   - Andrew I Friedson, Drew McNichols, Joseph J Sabia, and Dhaval Dave. 2021. Shelter-in-place orders and public health: evidence from California
during the Covid-19 pandemic. Journal of Policy Analysis and Management 40, 1 (2021), 258–283.
   - John PA Ioannidis. 2022. The end of the COVID-19 pandemic. European journal of clinical investigation 52, 6 (2022), e13782. 
   
