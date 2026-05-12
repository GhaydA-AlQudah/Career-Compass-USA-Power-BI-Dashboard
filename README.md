# CareerPulse-USA: IT Market Intelligence Dashboard

# Problem Statement
Navigating the tech job market is overwhelming for IT professionals. When deciding on a career path (e.g., Data Science vs. Cloud Engineering), individuals often struggle to find a single, reliable source that compares more than just salaries. They face a "data gap" when trying to understand how different roles vary across key U.S. states in terms of:

Financial Reward: What is the actual market value of a role when comparing hourly contracts to annual salaries?

Job Stability: Which titles offer full-time security versus contract-based flexibility?

Total Compensation: Which companies and states provide essential benefits like health insurance?

Barriers to Entry: Where can skills and experience outweigh the need for a traditional university degree?



# **Our Solution:**

**OLAP Sol. - Batch**

**Strategic Dashboard**

**For Non-Technical**

**UX/ UI**

This dashboard serves as a Strategic Career Navigator. It integrates fragmented data into a unified visual experience, allowing any IT professional to perform a "360-degree comparison." By analyzing salaries, skills, and benefits across top locations, it empowers users to make informed, data-driven decisions about their next career move.
Modeling and PowerBI Dashboard 
OLAP

Technologies 
python: pandas ....
Power BI Desktop : Report, Model, Power Query

steps 
## 1. Metadata
Feature Name,Source Table,Data Type,Description
job_id,job_fact,Integer,Unique identifier for each job posting (Primary Key).
Standardized_Annual_Salary,job_fact,Decimal,Normalized annual compensation in USD.
job_location_state,job_fact,String,"US State filtered for major Tech Hubs (e.g., CA, NY, TX)."
job_title_short,job_fact,String,"Categorized job roles (e.g., Data Engineer, Data Analyst)."
job_health_insurance,job_fact,String,"Benefit status: ""Includes Health Insurance"" vs ""No Health Insurance""."
job_no_degree_mention,job_fact,String,"Barrier to entry: ""Degree Required"" vs ""Degree Not Required""."
job_schedule_type,job_fact,String,"Harmonized work schedules (Full-time, Contract, etc.)."
skill_id,skills_dim_table,Integer,Unique identifier for technical skills.
skills,skills_dim_table,String,"Specific technical skill name (e.g., Python, SQL, Azure)."
name,company_dim_table,String,The name of the hiring organization.

## 2. EDA
Total Records: ~17,788 cleaned rows (after filtering for major states and removing outliers).

Time Scope: Data reflects job postings as of late 2023.

Data Integrity: 100% validity across key columns (Standardized_Annual_Salary, job_health_insurance) with no nulls in the final transformed set.

Granularity: The data is at the "Individual Job Posting" level.

## 3. Data Modeling - Snowflake Schema 


<img width="1605" height="571" alt="image" src="https://github.com/user-attachments/assets/7dc08da7-494f-4acd-9b7d-31f7e01a2bb9" />

"The data model follows a Snowflake Schema architecture. This was chosen to efficiently handle the Many-to-Many relationship between jobs and skills through a bridge table (skill_job_dim_table), ensuring a highly normalized structure that reduces data redundancy."


## 4. Data Cleaning: 
MVs

, Feature Selection 

, Empty Rows, 

Transformation 

📍 Data Scoping & Geographical Filtering

## 5. Dashboard

<img width="1266" height="742" alt="image" src="https://github.com/user-attachments/assets/162a7a5e-1ef3-4468-b200-2df56731e265" />


#### each chart


#### Descriptive - Power Query and Dashboard (Analytics - Batch)


#### Diagnostic - Why


#### Prescriptivs - Actionable Insight



# Demo and Storytelling


# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Analytics Engineering Enthusiast**

---


