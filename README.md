# CareerPulse-USA: IT Market Intelligence Dashboard

# Problem Statement
Navigating the tech job market is overwhelming for IT professionals. When deciding on a career path (e.g., Data Science vs. Cloud Engineering), individuals often struggle to find a single, reliable source that compares more than just salaries. They face a "data gap" when trying to understand how different roles vary across key U.S. states in terms of:

Financial Reward: What is the actual market value of a role when comparing hourly contracts to annual salaries?

Job Stability: Which titles offer full-time security versus contract-based flexibility?

Total Compensation: Which companies and states provide essential benefits like health insurance?

Barriers to Entry: Where can skills and experience outweigh the need for a traditional university degree?



# **Our Solution: Your Interactive Strategic Career Navigator**

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

### Data Source: https://www.lukebarousse.com/sql

| Feature Name | Source Table | Data Type | Description |
| :--- | :--- | :--- | :--- |
| `Jobs` | `job_fact` | Integer | Unique identifier for each job posting (Primary Key). |
| `Companies` | `job_fact` | Integer | Foreign Key linking Companies to Jobs. |
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

Data Integrity: 100% validity across key columns (Annual_Salary, job_health_insurance) with no nulls in the final transformed set.

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


<img width="1707" height="660" alt="image" src="https://github.com/user-attachments/assets/f11683a7-4ea7-47b0-9f39-af98e63fad5f" />


### Example : Filtering on California State
<img width="1705" height="662" alt="image" src="https://github.com/user-attachments/assets/2fe61f0c-6b0f-4c2f-9297-2206f8b3468a" />


### Ideas :
- [ ]  you can take a quick look to see what the most required Job title, which state contain the most tech jobs, which companies in each state, the privileges like health insurance, the flexibility of the schule type across jobs, states, companies, and the annual salary

### and using the slicers:
- [ ] you can filter on State:
      - see the average annual salary in total or across  jobs
      - the most required skills

- [ ] You can filter on Jobs:
      - the highest annusl salary
      - the required skills
      - priveleges (scheule type and health insurance)
      - the most states contains that job
- [ ] you can filter over both or between any mix to spot the cross you want to  discover.



# Recommendation
##### based on your ///


# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Data Analytics Enthusiast**

---
