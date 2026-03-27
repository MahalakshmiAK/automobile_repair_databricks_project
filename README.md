AUTOMOBILE REPAIR PROJECT

CASESTUDY OVERVIEW 
This dataset represents a multi-location vehicle repair business where vehicles are repaired, billed, and delivered back to customers. The business tracks repair timelines, estimates, revenue, staff performance, and customer feedback across stores to analyse operational efficiency, financial performance, and customer experience over time. 

LIST OF KEY PERFORMANCE INDICATORS (KPIs)

1.	MTD Performance vs Previous MTD: 
Month-to-date revenue and number of completed orders compared with previous month-to-date, by store and manager. 
1.	Average Days in Shop: 
Average days a vehicle spends in the shop, by store and service type. 
2.	Survey Coverage: 
For each store, number of surveys sent versus number of surveys responded. 
4.	Survey Scores Summary: 
Overall customer survey metrics by store and ranking of stores by overall satisfaction. 
5.	Revenue vs Budget: 
Monthly revenue compared against budget by manager, and ranking of managers by budget achievement. 
6.	Top Technicians by Completion Time Accuracy: 
For each store, top 5 technicians based on accuracy of meeting promised completion dates. 
7.	Year-to-Date Revenue Growth: 
Year-to-date revenue compared with previous year YTD, and ranking of stores by YTD growth. 
8.	Stage-wise Day Cycle Time: 
Average days spent in each stage (vehicle-in to work-start, work-start to completion, completion to delivery), by store and service type. 
9.	Estimator Accuracy: 
Accuracy of estimates (initial vs final) by estimator and ranking of estimators by highest accuracy. 
10.	Technician Workload: 
Number of orders handled and total days in shop per technician per month and ranking of technicians by workload. 
 
TECH STACK USED:
•	Databricks
•	GitHub
•	Microsoft Azure (Storage Account)
•	Fivetran


ARCHITECTURE OVERVIEW
The Medallion Pattern
A medallion architecture is a data design pattern used to logically organize data, with the goal of incrementally and progressively improving the structure and quality of data as it flows through each layer of the architecture (from Bronze ⇒ Silver ⇒ Gold layer tables).
1.	Bronze Layer :

Acts as a landing zone for raw data from Azure blob storage and will be full load based on the sync time given in Fivetran.

1.	Catalog: 
•	customer_survey
•	estimate
•	invoice
•	ns_budget 
•	order 
•	store 
2.	Workspace:
•	data_ingestion


2.	Silver Layer :

Transforms raw data into validated, clean data such as handling nulls, casting datatypes.
1.	Catalog: 
•	customer_survey
•	estimate
•	invoice
•	ns_budget 
•	order 
•	store 
2.	Workspace:
•	data_cleaning

3.	Gold layer :

Data here is stored in a star schema format as dimensional and fact tables.
Delivers curated data (cube data table) is create, which help in optimizing the performance.  
1.	Catalog: 
•	dim_customer_survey
•	dim_order
•	dim_store
•	fact_budget
•	fact_invoice_details
•	data_cube
2.	Workspace:
•	fact_dim_tables
•	kpi

Data Ingestion 
Detail how you brought the raw data into your environment. 
•	Source Details: CSV file are taken from Azure blob storage into separate folder called azure_blob_storage. From azure_blob_storage the data in pulled into bronze layer as such (raw data).
•	Ingestion Method: Using Fivetran, the data is ingested into Databricks from Azure.
 Data Processing (Cleansing & Transformation)
Use the Medallion Architecture as a framework for the project. 
•	Cleansing Logic (Silver Layer): Specific steps taken to handle nulls, duplicates, and data type casting.
•	Business Logic (Gold Layer): Transformations applied to prepare data for the KPIs, such as aggregations or joins.
•	Data Quality Checks: List the "tests" you ran, such as uniqueness and not-null constraints. 

 Data Analysis & KPI Cube
Explain the final structure that users will query for insights. 
•	KPI Definitions: Explicitly define the formula for each KPI and the queries.
•	Cube Model: Describe the table relationships (Star schema) and the dimensions available for filtering.

Orchestration & Pipeline Management
How the project was automated, the entire workflow to run without manual intervention. 
•	Workflow Design: Use a DAG diagram to show task dependencies (e.g., Job B only starts after Job A succeeds).
•	Tools Used:  used Databricks Workflows
•	Schedule & Monitoring: The frequency of the runs was set for everyday.
 

Technical Standards & Standards
•	Naming Conventions: Have used the snake_case naming conventions
•	Code Documentation: Have given meaningful comments notebooks for readability 
•	Version Control: Have used GitHub for version controlling. 

GitHub link:  
https://github.com/MahalakshmiAK/automobile_repair_databricks_project.git

