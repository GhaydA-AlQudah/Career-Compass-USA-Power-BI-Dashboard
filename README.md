# CareerPulse-USA: IT Market Intelligence Dashboard

# Problem Statement
Navigating the tech job market is overwhelming for IT professionals. When deciding on a career path (e.g., Data Science vs. Cloud Engineering), individuals often struggle to find a single, reliable source that compares more than just salaries. They face a "data gap" when trying to understand how different roles vary across key U.S. states in terms of:

Financial Reward: What is the actual market value of a role when comparing hourly contracts to annual salaries?

Job Stability: Which titles offer full-time security versus contract-based flexibility?

Total Compensation: Which companies and states provide essential benefits like health insurance?

Barriers to Entry: Where can skills and experience outweigh the need for a traditional university degree?



# **Our Solution: Your Strategic Career Navigator**

**Imagine having a personal GPS for your tech career!**

I’ve built more than just a report; this is a **Strategic Dashboard** focused on a 360-degree comparison. Whether you are a Data Scientist, an Engineer, or just starting in IT, this tool allows you to:

1. See the Full Spectrum: Compare salaries, skills, and benefits across the top tech hubs in the US.

2. Make Smarter Moves: Use data-driven insights to decide your next career step based on facts, not guesses.

3. Simplicity for Everyone: While the backend is complex, the **UX/UI** is designed to be intuitive for **Non-Technical** users, making advanced analytics accessible to all.


🛠️ What’s under the hood?
To make this "simple" experience possible, I handled the heavy engineering tasks:

Data Engineering (Python & Pandas): I cleaned and transformed raw datasets to ensure high-quality, reliable information.

Advanced Modeling (OLAP & Snowflake Schema): I designed an efficient OLAP Batch Solution using a Snowflake Schema to handle complex relationships between jobs, companies, and skills.

Visual Storytelling (Power BI): Using Power Query and **DAX**, I built a dynamic model that updates and responds to user needs instantly.

 
## 1. Metadata

| Feature Name | Source Table | Data Type | Description |
| :--- | :--- | :--- | :--- |
| `job_id` | `job_fact` | Integer | Unique identifier for each job posting (Primary Key). |
| `Annual_Salary` | `job_fact` | Decimal | Normalized annual compensation in USD. |
| `job_location_state` | `job_fact` | String | US State filtered for major Tech Hubs (e.g., CA, NY, TX). |
| `job_title_short` | `job_fact` | String | Categorized job roles (e.g., Data Engineer, Data Analyst). |
| `job_health_insurance` | `job_fact` | String | Benefit status: "Includes Health Insurance" vs "No Health Insurance". |
| `job_schedule_type` | `job_fact` | String | Harmonized work schedules (Full-time, Contract, etc.). |
| `skill_id` | `skills_dim_table` | Integer | Unique identifier for technical skills. |
| `skills` | `skills_dim_table` | String | Specific technical skill name (e.g., Python, SQL, Azure). |
| `type` | `skills_dim_table` |String | Categorization of the skill (e.g., Programming, Cloud, Databases). |
| `name` | `company_dim_table` | String | The name of the hiring organization. |
| `company_id` | `company_dim_table` |Integer | Unique identifier for each hiring organization (Primary Key). |
| `job_id` | `skill_job_dim_table` | Integer | Foreign Key linking jobs to their required skills. |
| `skill_id` | `skill_job_dim_table` | Integer | Foreign Key linking skills to specific job postings. |


## 2. EDA
Total Records: ~17,788 cleaned rows (after filtering for major states and removing outliers).

Time Scope: Data reflects job postings as of late 2023.

Data Integrity: 100% validity across key columns (Standardized_Annual_Salary, job_health_insurance) with no nulls in the final transformed set.

Granularity: The data is at the "Individual Job Posting" level.

## 3. Data Modeling - Snowflake Schema 


<img width="1577" height="587" alt="image" src="https://github.com/user-attachments/assets/bc401a32-da99-4338-abab-c0badda572a5" />


"The data model follows a Snowflake Schema architecture. This was chosen to efficiently handle the Many-to-Many relationship between jobs and skills through a bridge table (skill_job_dim_table), ensuring a highly normalized structure that reduces data redundancy."


## 4. Data Cleaning: 
#### Empty rows and Errors Removed.

#### Feature Selection : Unrelevant Columns removed

#### Feature Extraction: salay rate


#### Transformation : 1. Transformed encoded numerical values into human-readable, meaningful labels.
####                  2. Geospatial Normalization: Mapped specific cities into their respective US States to enable high-level geographical grouping.
####                  3. Standardized various schedule_type entries into unified categories (e.g., Full-time, Contract, Internship).
#### Applied filters to scope the data specifically to US Tech Hubs, ensuring the analysis remains relevant to the targeted market.
#### Outliers

## 5. Dashboard

<img width="1266" height="742" alt="image" src="https://github.com/user-attachments/assets/162a7a5e-1ef3-4468-b200-2df56731e265" />

<img width="1381" height="686" alt="image" src="https://github.com/user-attachments/assets/5cadb0f0-f7e7-44ec-b3ca-4cf52f16f28d" />

<img width="1321" height="597" alt="image" src="https://github.com/user-attachments/assets/0e67a106-2089-4ee8-85de-9c36f6219ac5" />

<img width="1317" height="605" alt="image" src="https://github.com/user-attachments/assets/25a353cf-e50b-4cbf-8eca-7448aa2974d5" />

<img width="1317" height="605" alt="image" src="https://github.com/user-attachments/assets/0a574a73-ad24-4206-affb-631b78bc465c" />

<img width="1316" height="602" alt="image" src="https://github.com/user-attachments/assets/4e122d4a-ac69-4b44-aa42-7d9d0c08dc57" />


#### each chart


#### Descriptive - Power Query and Dashboard (Analytics - Batch)


#### Diagnostic - Why


#### Prescriptivs - Actionable Insight

##### based on your ///



# Demo and Storytelling


# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Analytics Engineering Enthusiast**

---


