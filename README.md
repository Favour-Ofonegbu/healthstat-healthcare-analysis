## Project Overview

This project analyzes hospital efficiency using **Power BI and DAX** for HealthStat, a healthcare consulting company.

The analysis uses New York State hospital discharge data for patients who underwent **elective hip replacement surgery**. The primary focus is on **Length of Stay (LOS)** and **hospital costs**, while examining how patient and hospital characteristics relate to differences in these outcomes.

The goal is to identify patterns in hospital stays and costs, understand variation across hospitals, and uncover potential areas for further investigation into healthcare efficiency.

The final deliverable is an **interactive Power BI dashboard** that presents key metrics, comparisons, and insights to support data-informed decision-making.

1. Business Problem and Project Objectives
   Business Problem
   Healthcare organizations need to understand how efficiently hospitals deliver care while managing the costs associated with patient treatment. Differences in hospital length of stay and cost per discharge may indicate opportunities to investigate operational performance, resource utilization, and variations in care delivery.
   HealthStat, a fictitious healthcare consulting company, seeks to analyze hospital inpatient data for patients who underwent elective total hip replacement surgery in New York State. The analysis focuses on understanding variations in length of stay (LOS) and hospital costs across facilities and exploring how patient characteristics and hospital-related factors are associated with these outcomes.
   Project Objectives
   The objectives of this project are to:
   • Analyze the average length of stay and average cost per discharge for elective total hip replacement procedures.
   • Compare hospital performance to identify differences in length of stay and cost across facilities.
   • Examine associations between patient characteristics, clinical factors, and hospital outcomes.
   • Identify hospitals with comparatively high or low average length of stay and costs for further investigation.
   • Develop an interactive Power BI dashboard that presents key performance indicators, hospital comparisons, and patient discharge patterns.
   • Provide data-informed insights that can support further investigation into hospital efficiency and cost management.
   The project aims to highlight patterns and potential areas for improvement rather than establish the causes of differences in hospital performance.

2. Dataset and Data Preparation
   Dataset Overview
   This project uses New York State hospital inpatient discharge data for patients who underwent elective total hip replacement surgery.
   The dataset contains hospital-level and patient-level information about inpatient stays, including length of stay, hospital costs, patient demographics, clinical characteristics, and discharge outcomes.
   Each row represents an individual hospital discharge record.
   Dataset file: hospital_inpatient_discharges_totalhipreplacement.csv
   Analysis tool: Microsoft Power BI
   Key Dataset Fields
   Category Fields Purpose
   Hospital information facility_id, facility_name, hospital_county, health_service_area Identify hospitals and compare performance across facilities and regions.
   Patient demographics age_group, gender, race, ethnicity Examine variations in outcomes across demographic groups.
   Hospital outcomes length_of_stay, total_charges, total_costs, patient_disposition Analyze length of stay, costs, charges, and discharge outcomes.
   Clinical characteristics apr_severity_of_illness_description, apr_risk_of_mortality, ccs_diagnosis_description Explore how clinical characteristics are associated with hospital outcomes.
   Procedure information ccs_procedure_description, apr_drg_description, apr_mdc_description Identify and describe the procedure and related clinical classifications.
   Provider information attending_provider_license_number, operating_provider_license_number Support analysis of provider counts and related operational measures.
   Time information discharge_year Identify the year associated with each discharge record.
   Data Preparation
   Data preparation was performed in Power Query within Power BI.
   The preparation process included:
3. Importing the dataset: Loaded the CSV file into Power BI.
4. Filtering the procedure: Filtered ccs_procedure_description to HIP REPLACEMENT, TOT/PRT to focus the analysis on the selected procedure.
5. Preparing the analysis model: Used the relevant hospital, demographic, clinical, cost, and discharge fields to build measures and visualizations.
6. Creating an age classification: Added an Age Band calculated column to group patients into Age 50+ and Age <50 categories for demographic analysis.
   The prepared data was then used to create DAX measures, hospital comparisons, and interactive dashboard pages.

Data Dictionary
The data dictionary describes the dataset's column names and their meanings to support interpretation of the analysis.
Column Name Meaning
health_service_area Geographic health service area where the hospital is located.
hospital_county County in which the hospital is located.
facility_id Identifier assigned to the hospital facility.
facility_name Name of the hospital facility.
age_group Patient's age category.
zip_code_3_digits First three digits of the patient's ZIP code, used as a geographic indicator.
gender Patient's recorded gender category.
race Patient's recorded racial category.
ethnicity Patient's recorded ethnicity category.
length_of_stay Number of days the patient stayed in the hospital.
type_of_admission Classification of the admission type.
patient_disposition Patient's status or destination at discharge.
ccs_diagnosis_code Clinical Classification Software (CCS) code for the diagnosis category.
ccs_diagnosis_description Description of the CCS diagnosis category.
ccs_procedure_code CCS code identifying the procedure category.
ccs_procedure_description Description of the procedure category.
apr_drg_code All Patient Refined Diagnosis Related Group (APR-DRG) code.
apr_drg_description Description of the APR-DRG classification.
apr_mdc_code All Patient Refined Major Diagnostic Category (APR-MDC) code.
apr_mdc_description Description of the major diagnostic category.
apr_severity_of_illness_code Numeric code representing the severity-of-illness category.
apr_severity_of_illness_description Description of the patient's severity-of-illness category.
apr_risk_of_mortality Classification of the patient's risk of mortality.
apr_medical_surgical_description Classification indicating the medical or surgical category.
attending_provider_license_number License number identifying the attending provider.
operating_provider_license_number License number identifying the operating provider.
operating_certificate_number Certificate number associated with the hospital's operating authority.
total_charges Total charges recorded for the hospital stay.
total_costs Total costs recorded for the hospital stay.
discharge_year Year in which the patient was discharged.
Note: These definitions describe the apparent meaning of the field names. Where precise administrative or clinical definitions matter, they should be checked against the dataset's official data dictionary.

3. Analytical Questions
   The analysis was designed to investigate differences in hospital length of stay and costs for elective total hip replacement procedures across New York State hospitals.
   The following questions guided the analysis.
   3.1 Hospital Performance and Variation
1. How does the average length of stay vary across hospitals?
1. Which hospitals have the highest and lowest average lengths of stay?
1. How does the average cost per discharge vary across hospitals?
1. Which hospitals have the highest and lowest average costs per discharge?
1. How do hospital discharge volumes relate to differences in average length of stay and cost?
   3.2 Patient and Clinical Characteristics
1. How does length of stay vary across patient age groups and gender categories?
1. How are severity of illness and risk of mortality distributed across hospital discharges?
1. How do diagnosis categories and patient discharge dispositions vary across hospitals?
1. Which patient or clinical characteristics are associated with differences in average length of stay and cost per discharge?
   3.3 Cost and Length-of-Stay Benchmarks
1. How do hospital average length of stay and average cost per discharge compare with the overall reference benchmarks?
1. Which hospitals fall above or below the reference benchmarks for length of stay and cost?
1. Which hospitals warrant further investigation because of comparatively high average costs, longer stays, or unusual combinations of both?
   3.4 Interactive Hospital Analysis
1. How do hospital-level metrics and discharge patterns change when a specific hospital is selected?
1. How do comparisons change when the analysis is filtered by health service area?
   Expected Analytical Value
   Answering these questions helps identify patterns in hospital performance, compare facilities using consistent metrics, and highlight potential areas for further investigation into cost management and length-of-stay variation.
   The analysis is exploratory. Differences between hospitals do not, by themselves, establish that a hospital is inefficient or explain why its outcomes differ.

Total Hospitals
Total Hospitals =
DISTINCTCOUNT(hospital_discharges[facility_id])
Counts the number of unique hospital facilities represented in the filtered dataset.
Purpose: Measures the number of hospitals included in the analysis.
Total Discharges
Total Discharges =
COUNTROWS(hospital_discharges)
Counts the number of rows in the hospital discharge table.
Purpose: Measures the number of discharge records included in the analysis. This assumes each row represents one discharge record.
Average LOS Days
Average LOS Days =
AVERAGE(hospital_discharges[length_of_stay])
Calculates the average length of hospital stay in days.
Purpose: Supports comparisons of length of stay across hospitals and other selected categories.
Total Surgeons
Total Surgeons =
DISTINCTCOUNT(
hospital_discharges[operating_provider_license_number]
)
Counts the distinct operating provider license numbers in the filtered data.
Purpose: Provides a measure of the number of distinct operating providers represented in the records. The result should be interpreted carefully if provider license numbers are missing.
Average Cost Per Discharge
Average Cost Per Discharge =
AVERAGE(hospital_discharges[total_costs])
Calculates the average recorded hospital cost per discharge.
Purpose: Enables comparisons of average costs across facilities and other categories.
4.2 Overall Benchmark Measures
The project uses overall reference measures to compare hospital performance against the broader dataset.
Average Cost Per Discharge ALL
Average Cost Per Discharge ALL =
CALCULATE(
[Average Cost Per Discharge],
ALL(hospital_discharges)
)
Calculates the average cost per discharge after removing filters from the hospital_discharges table.
Purpose: Provides an overall cost reference for comparison with filtered hospital results.
Average LOS Days ALL
Average LOS Days ALL =
CALCULATE(
[Average LOS Days],
ALL(hospital_discharges)
)
Calculates the average length of stay after removing filters from the hospital_discharges table.
Purpose: Provides an overall LOS reference for comparison with filtered hospital results.
Benchmark interpretation: The course-provided reference values are $20,910 for average cost per discharge and 2.65 days for average length of stay. These should be distinguished from values dynamically recalculated by the DAX measures. Because ALL(hospital_discharges) removes filters from the entire table, these measures do not retain filters applied to that table.
4.3 Percentage Variance Measures
These measures quantify how far a selected result is above or below its overall reference value.
Percentage Variance in Average Cost per Discharge
% Var Average Cost per Discharge =
DIVIDE(
[Average Cost Per Discharge] -
[Average Cost Per Discharge ALL],
[Average Cost Per Discharge ALL]
)
Calculates the relative difference between the selected average cost and the overall average cost.
Interpretation:
• A positive result indicates a cost above the overall reference.
• A negative result indicates a cost below the overall reference.
• A result of zero indicates equality with the reference.
Percentage Variance in Average LOS
% Var Average LOS Days =
DIVIDE(
[Average LOS Days] -
[Average LOS Days ALL],
[Average LOS Days ALL]
)
Calculates the relative difference between the selected average length of stay and the overall average length of stay.
Interpretation:
• A positive result indicates a longer average stay than the reference.
• A negative result indicates a shorter average stay than the reference.
• A result of zero indicates equality with the reference.
The DIVIDE function handles division by zero more safely than the standard division operator. Format these measures as percentages in Power BI.
4.4 Percentile Measure
90th Percentile Average Cost
90th Percentile Average Cost =
PERCENTILEX.INC(
VALUES(hospital_discharges[facility_name]),
[Average Cost Per Discharge],
0.9
)
Calculates the 90th percentile of hospital average costs across the distinct facility names in the current evaluation context.
Purpose: Provides a reference point for identifying hospitals with comparatively high average costs.
Interpretation: The 90th percentile is the value at or below which approximately 90% of the evaluated hospital average-cost values fall. It is not the same as the average cost, and it does not by itself establish that a hospital is inefficient.
4.5 Dynamic Hospital Profile Title
Title Selected Facility
Title Selected Facility =
"Hospital Profile: " &
CONCATENATEX(
VALUES(hospital_discharges[facility_name]),
hospital_discharges[facility_name],
", "
)
Creates a title from the hospital name or names in the current filter context.
Purpose: Makes the Hospital Profile page more informative by displaying the selected facility name dynamically.
4.6 Calculated Column: Age Band
Although this is not a measure, the project also uses a calculated column to group age categories.
Age Band =
IF(
hospital_discharges[age_group]
IN {"50-59", "60-69", "70-79", "80+"},
"Age 50+",
"Age <50"
)
Groups the age categories 50-59, 60-69, 70-79, and 80+ into Age 50+. All other values are assigned to Age <50.
Purpose: Simplifies age-group comparisons in the demographic analysis.
Summary
The DAX measures support five main analytical functions:

1. Performance measurement: Counts hospitals and discharge records, and calculates average length of stay and cost.
2. Benchmarking: Compares selected results against overall reference measures.
3. Variance analysis: Quantifies differences from the reference values.
4. Distribution analysis: Uses the 90th percentile to assess the distribution of hospital average costs.
5. Dynamic reporting: Updates the hospital profile title based on the selected facility.
   These calculations power the KPI cards, hospital comparisons, scatter plot reference lines, rankings, and hospital profile visuals in the Power BI report.

6. Dashboard Pages and Interactive Features
   The HealthStat Power BI report consists of four main pages: Home, LOS Comparison, Cost Comparison, and Hospital Profile. Each page serves a distinct purpose in exploring hospital length of stay, costs, and discharge patterns.
   5.1 Home
   The Home page serves as the landing page for the report.
   Features:
   • HealthStat dashboard branding and project title.
   • Page navigation to the main analytical sections.
   • A central entry point for exploring hospital performance and cost comparisons.
   Purpose: Provides a clear starting point and allows users to navigate between the report's analytical pages.
   5.2 LOS Comparison
   The LOS Comparison page focuses on differences in average length of stay across hospitals.
   Key visualizations:
   • KPI cards: Display average length of stay, total hospitals, and total discharges.
   • Combo chart: Compares average length of stay and total discharge volume across selected hospitals.
   • Top-three and bottom-three charts: Identify hospitals with the highest and lowest average length of stay.
   • Key Influencers visual: Explores factors associated with variation in average length of stay.
   • Health service area slicer: Allows users to filter the analysis by geographic health service area.
   Purpose: Helps users examine hospital-level variation in length of stay, compare facilities, and identify patterns for further investigation.
   5.3 Cost Comparison
   The Cost Comparison page examines variation in average cost per discharge and its relationship with length of stay.
   Key visualizations:
   • KPI cards: Display average length of stay, average cost per discharge, total hospitals, and total discharges.
   • Scatter plot: Compares average length of stay against average cost per discharge for individual hospitals.
   • Bubble size: Represents total discharges, helping users distinguish hospitals by discharge volume.
   • Color legend: Differentiates hospitals by health service area.
   • Reference lines: Provide average length-of-stay and average-cost benchmarks, alongside a 90th-percentile average-cost reference.
   • Top-three and bottom-three charts: Highlight hospitals with the highest and lowest average costs per discharge.
   • Key Influencers visual: Explores factors associated with differences in average cost per discharge.
   • Health service area slicer: Filters the hospital comparison analysis by health service area.
   Purpose: Helps users investigate how hospital costs vary, how cost patterns relate to length of stay, and which facilities may warrant closer examination.
   5.4 Hospital Profile
   The Hospital Profile page provides a more detailed view of an individual hospital.
   Key visualizations:
   • Average LOS gauge: Compares the selected hospital's average length of stay with an overall reference value.
   • Average cost gauge: Compares the selected hospital's average cost per discharge with an overall reference value.
   • Severity-of-illness chart: Displays discharge counts across severity categories.
   • Risk-of-mortality chart: Displays discharge counts across risk-of-mortality categories.
   • Diagnosis donut chart: Shows the distribution of discharges by diagnosis description.
   • Patient-disposition donut chart: Shows the distribution of discharges by discharge disposition.
   • Hospital selector: Allows users to select a facility for individual analysis.
   • Dynamic title: Displays the selected hospital name.
   Purpose: Enables users to explore hospital-specific performance measures and understand the composition of its discharge records.
   5.5 Interactive Features
   The report includes several features that support interactive analysis:
   • Page navigation: Moves between the four main dashboard pages.
   • Slicers: Filter hospital comparisons by health service area or select an individual hospital profile.
   • Synchronized filtering: The health service area slicer is synchronized between the LOS Comparison and Cost Comparison pages.
   • Tooltips: Provide additional information when users hover over supported visual elements, including variance measures and discharge volume.
   • Dynamic measures and titles: Update displayed metrics and the hospital profile title according to the current selection.
   • Comparative reference lines: Help users assess hospital metrics against the configured overall benchmarks.
   Together, these features allow users to move from an overall view of hospital performance to more focused comparisons and individual hospital analysis.

7. Findings from the Analysis
   The analysis of New York State hospital inpatient discharge data for elective total hip replacement procedures was designed to examine variations in hospital length of stay (LOS), average cost per discharge, discharge volume, and patient characteristics.
   The Power BI dashboard enables comparisons across hospitals and health service areas, as well as more detailed examination of individual facilities. The following findings summarize the patterns observed in the dashboard and their implications for further investigation.
   6.1 Overall Length of Stay and Cost Benchmarks
   The dashboard uses the following overall reference values:
   Performance Indicator Reference Value
   Average Length of Stay 2.65 days
   Average Cost per Discharge $20,910
   These reference values provide a basis for comparing hospital-level performance. The LOS benchmark represents the reference average duration of a hospital stay, while the cost benchmark represents the reference average cost associated with a discharge.
   Hospitals can be compared against these values to determine whether their average LOS and average cost per discharge are above or below the reference levels.
   However, a value above either benchmark does not automatically indicate poor performance. Differences may be associated with patient characteristics, clinical complexity, hospital operations, and other factors not fully measured by the dashboard.
   Analytical implication: Benchmarks are useful for identifying facilities that warrant further investigation, but they should be interpreted alongside discharge volume and patient characteristics.
   6.2 Variation in Length of Stay Across Hospitals
   The LOS Comparison page shows differences in average length of stay across hospitals. The dashboard uses a combination chart to display average LOS alongside total discharge volume for selected facilities. Additional charts identify hospitals with the highest and lowest average LOS values.
   The Key Influencers visual also explores characteristics associated with variation in average LOS. Among the factors displayed during the analysis were severity of illness, risk of mortality, health service area, and patient disposition.
   These observations suggest that hospital stays vary across facilities and that clinical and hospital-related characteristics may be relevant to understanding those differences.
   The dashboard also demonstrates the importance of evaluating average LOS together with the number of discharges. An average based on a small number of records may be less stable than one based on a much larger number of records.
   Analytical implication: Hospitals with comparatively long stays should be investigated further, particularly where the pattern persists among facilities with sufficient discharge volume. The current analysis identifies differences but does not establish the reasons for them.
   6.3 Variation in Average Cost per Discharge
   The Cost Comparison page reveals differences in average cost per discharge across hospitals. The dashboard includes KPI cards, top-three and bottom-three comparisons, and a scatter plot that positions hospitals according to their average LOS and average cost.
   The top-three and bottom-three charts provide a convenient way to identify facilities at the higher and lower ends of the average-cost distribution. The 90th-percentile average-cost reference also provides a way to identify comparatively high-cost values.
   These comparisons are useful for directing attention toward hospitals whose average costs differ substantially from the overall reference.
   Nevertheless, a higher average cost does not necessarily mean that a hospital is inefficient. A difference may reflect the characteristics of the patients treated, the severity of their conditions, or other factors that the current dashboard does not fully account for.
   Analytical implication: Hospitals with comparatively high average costs should be prioritized for further examination rather than immediately classified as inefficient.
   6.4 Relationship Between Length of Stay and Cost
   The scatter plot on the Cost Comparison page examines the relationship between average LOS and average cost per discharge across hospitals.
   Each point represents a hospital, while bubble size represents total discharge volume. Color distinguishes hospitals by health service area. Reference lines provide a basis for comparing hospitals with the configured LOS and cost benchmarks.
   The visualization allows four broad patterns to be investigated:
   • Higher cost and longer LOS: Facilities in this category may warrant investigation into clinical complexity, discharge processes, and operational practices.
   • Higher cost and shorter LOS: These facilities may have higher costs despite shorter stays, suggesting that length of stay alone does not explain cost differences.
   • Lower cost and longer LOS: These facilities may warrant investigation into the relationship between resource utilization and duration of admission.
   • Lower cost and shorter LOS: These facilities may provide useful comparison cases, provided that patient characteristics and relevant clinical outcomes are also considered.
   These categories describe possible interpretations of the scatter plot, not verified classifications of particular hospitals.
   The recording does not provide sufficient evidence to quantify the strength of the relationship between average LOS and average cost. A correlation analysis using the underlying hospital-level data would be needed to measure that relationship more precisely.
   Analytical implication: Examining cost and LOS together provides more information than ranking hospitals on either measure alone. However, neither measure independently establishes clinical quality or operational efficiency.
   6.5 Differences Across Health Service Areas
   The interactive health service area slicer allows the analysis to be narrowed to specific geographic areas. The recording demonstrates that the displayed KPIs and hospital comparisons change when different areas are selected.
   For example, the following values were visible in the recording under different filter selections:
   Selected Filter Average LOS Hospitals Discharges
   Western NY 2.56 days 18 Approximately 3,000
   Southern Tier 2.43 days 4 296
   These figures represent filtered results shown during the recording, not statewide totals. They should be confirmed against the final Power BI report before being treated as definitive published statistics.
   The observed difference between the two displayed LOS averages demonstrates how regional filtering can reveal variation that may be obscured by an overall benchmark.
   However, these figures alone do not establish that one health service area performs better than another. The areas may differ in their number of hospitals, discharge volumes, and patient characteristics.
   Analytical implication: Regional comparisons can help identify geographic patterns, but conclusions should account for differences in the hospitals and patients represented in each area.
   6.6 Hospital-Level Analysis and Discharge Patterns
   The Hospital Profile page provides a more detailed view of an individual facility. It includes average LOS, average cost per discharge, discharge counts by severity of illness, discharge counts by risk of mortality, diagnosis categories, and patient disposition.
   During the recording, Memorial Hospital for Cancer and Allied Diseases was displayed with the following values:
   Indicator Displayed Value
   Average Length of Stay 9.10 days
   Average Cost per Discharge Approximately $64,000
   Discharges represented in the profile charts 51
   These values describe the selected hospital in the recorded filter state. They should not be interpreted as statewide averages.
   The selected hospital's displayed averages are above the project's overall reference values. This makes the facility a potential candidate for further investigation, but the dashboard alone does not establish why its results differ.
   The profile charts also show how discharges are distributed across clinical severity, mortality risk, diagnoses, and discharge dispositions. These distributions provide descriptive context for the hospital's patient records.
   However, the charts display discharge counts rather than average LOS or average cost within each clinical category. They therefore cannot establish whether a particular diagnosis or severity category accounts for the hospital's higher average LOS or cost.
   Analytical implication: Hospital profiles help identify facilities for closer examination and provide descriptive context, but further analysis is needed to determine which characteristics are associated with differences in their outcomes.
   6.7 Importance of Discharge Volume
   Discharge volume is an important consideration when interpreting hospital averages and rankings.
   The dashboard displays discharge counts alongside LOS and cost comparisons, while bubble size in the scatter plot provides another indication of hospital volume. This makes it possible to distinguish facilities with many discharge records from those with relatively few.
   A hospital with a small number of discharges may have an unusually high or low average that is strongly influenced by a few records. Such a result should be interpreted cautiously when comparing hospitals.
   For example, a very narrow selection in the recording displayed an average LOS of 9.33 days for a hospital with only three discharges. Although this value is high relative to the overall reference, three discharges are insufficient to support a strong conclusion about the hospital's typical performance.
   Analytical implication: Hospital rankings should be evaluated alongside discharge counts. Applying a minimum-volume threshold would make comparisons more meaningful and reduce the risk of overinterpreting small samples.
   6.8 Interpretation of Key Influencers
   The LOS and Cost Comparison pages include Key Influencers visuals to explore factors associated with variation in the selected outcome.
   During the analysis, the visuals displayed factors including health service area, severity of illness, risk of mortality, diagnosis, and patient disposition.
   These outputs can help identify variables for further investigation. However, the factors highlighted by the visual depend on the selected outcome, the data available, the filter context, and the visual's analytical settings.
   The results should therefore be interpreted as exploratory associations rather than evidence of causation. Where the visual reports no influencers for a particular selection, this means it did not identify qualifying influencers under those settings; it does not prove that no relevant relationships exist in the wider dataset.
   Analytical implication: Key Influencers can guide further analysis, but their results should be validated with appropriate statistical methods and domain knowledge before being used to support operational decisions.
   6.9 Summary of Findings
   The dashboard supports the following overall conclusions:
8. Hospital outcomes vary: Average LOS and average cost per discharge differ across the hospitals represented in the analysis.
9. Cost and LOS should be examined together: Their joint comparison helps identify different hospital performance patterns that cannot be understood from a single metric.
10. Regional filtering adds context: Health service area comparisons reveal how hospital averages change across selected geographic subsets.
11. Patient characteristics matter to interpretation: Clinical severity, mortality risk, diagnosis, and discharge disposition provide useful context for investigating hospital differences.
12. Discharge volume affects confidence in comparisons: Results based on small numbers of discharges require particular caution.
13. Further analysis is needed to explain differences: The current dashboard identifies patterns and potential investigation areas but does not establish the causes of hospital-level variation.
    Overall Conclusion
    The HealthStat dashboard demonstrates how Power BI can be used to explore hospital performance, compare average LOS and costs, examine discharge patterns, and identify facilities for further investigation.
    The analysis provides a foundation for evidence-informed discussions about hospital efficiency and cost management. More detailed statistical analysis, appropriate adjustment for patient characteristics, and additional clinical outcome data would be required before making definitive claims about efficiency or recommending operational changes at specific hospitals.
    The dashboard is designed to support comparative analysis and highlight potential opportunities for further investigation. Differences in hospital metrics may reflect several factors, including patient characteristics, clinical complexity, discharge patterns, and hospital operations.
    The analysis alone does not establish the causes of these differences or prove that a hospital is inefficient.

14. Recommendations, Limitations, and Tools Used
    7.1 Recommendations
    Based on the patterns explored in the HealthStat dashboard, the following recommendations are proposed for further investigation and data-informed decision-making.
15. Investigate Hospitals with Higher Average Costs
    Hospitals with average costs per discharge substantially above the overall reference should be reviewed to understand the factors associated with their higher costs.
    The investigation should consider patient characteristics, clinical complexity, discharge patterns, and operational processes before attributing cost differences to hospital efficiency.
16. Review Hospitals with Longer Average Lengths of Stay
    Hospitals with comparatively long average LOS should be examined to understand whether the differences are associated with patient needs, severity of illness, discharge planning, or other factors.
    Any proposed changes to discharge processes should prioritize patient safety and appropriate clinical care rather than simply reducing the number of hospital days.
17. Analyze Cost and Length of Stay Together
    Hospital performance should not be evaluated using average cost or LOS in isolation.
    The scatter plot provides a starting point for identifying hospitals with different combinations of cost and LOS. Further analysis should examine whether these patterns persist after accounting for discharge volume and patient characteristics.
18. Consider Discharge Volume When Comparing Hospitals
    Hospital rankings should be interpreted alongside the number of discharges used to calculate each average.
    A minimum discharge-volume threshold should be considered before ranking facilities or identifying outliers. This would help reduce the risk of drawing strong conclusions from hospitals with very few records.
19. Investigate Clinical Characteristics in Greater Detail
    The current dashboard describes discharge distributions by severity of illness, risk of mortality, diagnosis, and patient disposition.
    A useful next step would be to calculate average LOS and average cost across these categories. This would help determine whether differences in hospital performance are associated with differences in clinical characteristics.
20. Strengthen Statistical Validation
    Further analysis should quantify the relationship between average LOS and average cost rather than relying on visual inspection alone.
    Correlation analysis, outlier analysis, and suitable comparisons across patient groups could provide stronger evidence. Where the data supports it, risk adjustment should be considered before comparing hospitals as though they treat equivalent patient populations.
21. Extend the Analysis with Additional Outcome Data
    The current project focuses on LOS, costs, discharge volume, and descriptive patient characteristics.
    Where suitable data is available, future work could incorporate readmissions, complications, mortality outcomes, and other measures of clinical quality. These additions would help ensure that cost and LOS comparisons are interpreted alongside patient outcomes.
    7.2 Limitations
    The findings from this project should be interpreted in light of the following limitations.
22. Descriptive and Exploratory Analysis
    The dashboard identifies patterns, differences, and associations in the available data. It does not establish that a particular factor causes higher costs or longer hospital stays.
23. Limited Measures of Hospital Efficiency
    Average LOS and average cost per discharge are useful indicators, but they do not independently measure overall hospital efficiency or quality of care.
    A hospital with a shorter stay or lower cost is not necessarily more efficient if differences in clinical complexity and patient outcomes are not considered.
24. Patient and Clinical Differences
    Hospitals may treat patients with different demographic characteristics, severity of illness, mortality risk, and diagnoses.
    The dashboard displays some of these characteristics, but the current comparisons do not establish that hospital-level results have been fully adjusted for differences in patient populations.
25. Small Discharge Counts
    Hospitals or filtered subsets with few discharge records may produce averages that are strongly influenced by individual cases.
    Such results should be interpreted cautiously, particularly when identifying high-performing or low-performing hospitals.
26. Benchmark and Filter Context
    The interpretation of the statewide reference values depends on how the benchmark measures are configured and how filters are applied.
    The DAX measures using ALL(hospital_discharges) remove filters from the entire table. Consequently, their results may not preserve a selected health service area or other table-level filters. The benchmark values should be validated against the final report configuration before publication.
27. Limited Time-Based Analysis
    Although the dataset includes a discharge-year field, the final dashboard primarily focuses on comparisons across hospitals and selected groups.
    The current report does not establish long-term trends or demonstrate how hospital performance changes over time.
28. Data Coverage and Scope
    The analysis focuses on the selected elective total hip replacement procedure in New York State. Its findings should not automatically be generalized to other procedures, healthcare systems, geographic areas, or patient populations.
29. Dependence on Available Data
    The analysis is limited to the variables and records available in the dataset. Additional information about operational processes, clinical outcomes, resource utilization, and patient complexity could provide further context for interpreting hospital differences.
    7.3 Tools and Technologies Used
    The following tools and technologies were used in the project.
    Tool or Technology Application
    Microsoft Power BI Desktop Developed the interactive dashboard and report pages.
    Power Query Imported and prepared the hospital discharge dataset and applied the procedure filter.
    DAX (Data Analysis Expressions) Created measures for hospital counts, discharge counts, average LOS, average costs, percentage variance, percentile analysis, and dynamic titles.
    CSV Served as the source format for the hospital inpatient discharge dataset.
    Git Supported version control and tracking of project changes.
    GitHub Hosted the project repository, documentation, dataset, dashboard file, and supporting assets.
    7.4 Skills Demonstrated
    This project demonstrates practical experience in:
    • Data import and preparation using Power Query.
    • Data modeling and calculated columns in Power BI.
    • Writing DAX measures for performance indicators and comparative analysis.
    • Designing interactive dashboards and KPI cards.
    • Comparing hospital metrics against reference benchmarks.
    • Exploring relationships between length of stay, costs, and discharge volume.
    • Using slicers, tooltips, dynamic titles, and Key Influencers visuals.
    • Communicating analytical observations, limitations, and potential areas for further investigation.
    • Documenting and publishing an analytics project using Git and GitHub.
    Final Conclusion
    The HealthStat Healthcare Analysis project demonstrates how business intelligence tools can transform hospital discharge data into an interactive analytical report.
    By comparing length of stay, average cost per discharge, discharge volume, and selected patient characteristics, the dashboard provides a structured way to explore differences across hospitals and identify areas that may warrant further investigation.
    The project also highlights the importance of interpreting performance metrics in context. Reliable conclusions about hospital efficiency require consideration of patient characteristics, clinical outcomes, discharge volume, and the limitations of the available data.
