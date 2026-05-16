# *CareerPulse-USA Interactive Dashboard*

# Problem Statement
Navigating the tech job market is overwhelming for IT professionals. When deciding on a career path (e.g., Data Science vs. Cloud Engineering), individuals often struggle to find a single, reliable source that compares more than just salaries. They face a "data gap" when trying to understand how different roles vary across key U.S. states in terms of:

Financial Reward: What is the actual market value of a role when comparing hourly contracts to annual salaries?

Job Stability: Which titles offer full-time security versus contract-based flexibility?

Total Compensation: Which companies and states provide essential benefits like health insurance?

Barriers to Entry: Where can skills and experience outweigh the need for a traditional university degree?

---

# **Our Solution: Your Interactive Strategic Career Navigator**

**Imagine having a personal GPS for your tech career!**


<img width="1716" height="667" alt="image" src="https://github.com/user-attachments/assets/718557da-3b5d-4d82-993e-c02bfec2d905" />




I’ve built more than just a report; this is a **Interactive Strategic Dashboard** focused on a 360-degree comparison. Whether you are a Data Scientist, an Engineer, or just starting in IT, this tool allows you to:

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
Total Records: 17,788 cleaned rows (after filtering for major states and removing outliers).

Time Scope: Data reflects job postings as of late 2023.

Data Integrity: 100% validity across key columns (Annual_Salary, job_health_insurance) with no nulls in the final transformed set.

Granularity: The data is at the "Individual Job Posting" level.



## 3. Data Modeling - Snowflake Schema 

### Snowflake Schema

<img width="1542" height="512" alt="image" src="https://github.com/user-attachments/assets/4ae6d48d-5d96-4dad-bcad-48d39000a452" />

This was chosen to efficiently handle the Many-to-Many relationship between jobs and skills through a bridge table (skill_job_dim_table), ensuring a highly normalized structure that reduces data redundancy.

### Single Cross-Filter Direction

```
[company_dim_table] (1) ──┐
                                 │
                                 ▼
                           [job_fact] (*) ── (1) ──┐
                                                   │
                                                   ▼
                                        [skill_job_dim_table] (*) ── (*) ── [skills_dim_table] (1)
```


**Single Data Flow**: Snowflake filtering constraints are preserved by establishing 1:N (One-to-Many) relationships using **Bridge Table(skill_job_dim_table)**. The cross-filter direction propagates seamlessly from Dimension tables down to the Fact table, optimizing query execution times within Power BI.

## 4. Data Cleaning: 

a. Empty rows and Errors Removed.

b. Applied filters to scope the data specifically to US Tech Hubs, ensuring the analysis remains relevant to the targeted market.

c. Feature Selection : Unrelevant Columns removed

d. Feature Extraction: Annual Salary calculated from different columns to unify hourly, monthly, and varying compensation structures into a single standardized metric, enabling accurate *cross-functional* analysis.

e. Transformation : 1. Transformed encoded numerical values into human-readable, meaningful labels.

                    2. Geospatial Normalization: Mapped specific cities into their respective US States to enable high-level geographical grouping.
                    
                    3. Standardized various schedule_type entries into unified categories (e.g., Full-time, Contract, Internship).
                    

f. Outliers


## 5. Dashboard


### Example : Filtering on California State

<img width="1721" height="667" alt="image" src="https://github.com/user-attachments/assets/5e5613cd-2c75-447b-ba25-2b5cfa370919" />


<img width="1712" height="712" alt="image" src="https://github.com/user-attachments/assets/21dc3a67-a875-4f9e-91d4-c23098ed3626" />


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


1. High-Level Market Overview
At a glance, the dashboard provides a macro perspective of the industry, allowing you to:

Identify Market Leaders: Pinpoint which job titles dominate the current landscape and which states serve as the primary tech hubs.

Corporate Benchmarking: Discover top-hiring companies filtered by state and industry presence.

Holistic Compensation Analysis: Evaluate "quality of life" metrics, including health insurance availability and work-schedule flexibility (Remote vs. On-site), alongside traditional salary data.

2. Targeted Discovery via Dynamic Slicers
By leveraging the interactive Snowflake Schema architecture, users can perform granular "Deep Dives" using multi-select slicers:

Geographical Analysis (State Filter):

Assess localized earning potential through Average Annual Salary benchmarks.

Extract the Top-Tier Skillsets specifically demanded within a particular region.

Role-Specific Analysis (Job Title Filter):

Compare Salary Distributions to identify the highest-paying career paths.

Map out the Technical Stack required for specific roles to guide upskilling efforts.

Analyze the "Perks Gap" by seeing which roles offer the best benefits and schedule types.

Cross-Dimensional Filtering:

Combine multiple filters (e.g., Data Scientist in California at Large Tech Firms) to spot unique market "cross-sections" and tailor your career strategy to real-world data.


# Recommendation
##### based on your /// but for me as example : i woudl say the highest salaries in california and the most reuired id data scientist which is one of my interisting jobs , and i need to learn these skills (...) and i will try my best to  be ready to applicate in the 3rd quarter to have a higher apportunity and match the most companies like (...)

---

# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Data Analytics Enthusiast**

---
