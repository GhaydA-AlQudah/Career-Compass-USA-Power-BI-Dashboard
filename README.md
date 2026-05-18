# *CareerPulse-USA Interactive Dashboard*
across dgo far diagnostic
# Problem Statement
Navigating the tech job market is overwhelming for IT professionals. When deciding on a career path (e.g., Data Science vs. Cloud Engineering), individuals often struggle to find a single, reliable source that compares more than just salaries. They face a "data gap" when trying to understand how different roles vary across key U.S. states in terms of:

Financial Reward: What is the actual market value of a role when comparing hourly contracts to annual salaries?

Job Stability: Which titles offer full-time security versus contract-based flexibility?

Total Compensation: Which companies and states provide essential benefits like health insurance?

Barriers to Entry: Where can skills and experience outweigh the need for a traditional university degree?

---

# **Our Solution: Your Interactive Strategic Career Navigator**

**Imagine having a personal GPS for your tech career!**


<img width="1582" height="685" alt="image" src="https://github.com/user-attachments/assets/d01f10c9-1c2b-4c7d-8228-a898d0627450" />


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
| `name` | `company_dim_table` | String | The name of the hiring organization. |
| `company_id` | `company_dim_table` |Integer | Unique identifier for each hiring organization (Primary Key). |


## 2. EDA
Total Records: 17,788 cleaned rows (after filtering for major states and removing outliers).

Time Scope: Data reflects job postings as of late 2023.

Data Integrity: 100% validity across key columns (Annual_Salary, job_health_insurance) with no nulls in the final transformed set.

Granularity: The data is at the "Individual Job Posting" level.



## 3. Data Modeling 

### Star Schema

<img width="1046" height="646" alt="image" src="https://github.com/user-attachments/assets/c8b58989-15f8-4685-a74c-5b4b5d4bbb09" />

Designed and optimized a high-performance Star Schema architectural model in Power BI, centralizing key market metrics within a core fact table connected directly to normalized dimensions (company_dim)."

### Single Cross-Filter Direction

```
[company_dim_table] (1)   ──┐
                            │
                            ▼
                      [job_fact] (*) ── (1) 
```


**Single Data Flow**: Snowflake filtering constraints are preserved by establishing 1:N (One-to-Many) relationships. The cross-filter direction propagates seamlessly from Dimension tables down to the Fact table, optimizing query execution times within Power BI.

## 4. Data Cleaning: 

a. Empty rows and Errors Removed.

b. Applied filters to scope the data specifically to US Tech Hubs, ensuring the analysis remains relevant to the targeted market.

c. Feature Selection : Unrelevant Columns removed

d. Feature Extraction: Annual Salary calculated from different columns to unify hourly, monthly, and varying compensation structures into a single standardized metric, enabling accurate *cross-functional* analysis.


e. Transformation: 
1. Transformed encoded numerical values into human-readable, meaningful labels.
2. Geospatial Normalization: Mapped specific cities into their respective US States to enable high-level geographical grouping.
3. Standardized various schedule_type entries into unified categories (e.g., Full-time, Contract, Internship).

f. Outliers: Identified and handled statistical anomalies and extreme wage values to prevent distortion in descriptive metrics and average charts.

## 5. Dashboard and Storyteling

### 1 : Without Filtering

<img width="1589" height="699" alt="image" src="https://github.com/user-attachments/assets/d3d46919-c772-4b75-94d7-9684bd4f167e" />


<img width="1710" height="692" alt="image" src="https://github.com/user-attachments/assets/4705cd8e-e55a-401e-9a6b-99ab0afbacbc" />

- [ ]  you can take a quick look to see what the most required Job title, which state contain the most tech jobs, which companies in each state, the privileges like health insurance, the flexibility of the schule type across jobs, states, companies, and the annual salary

1. High-Level Market Overview
At a glance, the dashboard provides a macro perspective of the industry, allowing you to:

Identify Market Leaders: Pinpoint which job titles dominate the current landscape and which states serve as the primary tech hubs.

Corporate Benchmarking: Discover top-hiring companies filtered by state and industry presence.

Holistic Compensation Analysis: Evaluate "quality of life" metrics, including health insurance availability and work-schedule flexibility (Remote vs. On-site), alongside traditional salary data.

### Example 2 : Filtering on California State

<img width="1582" height="691" alt="image" src="https://github.com/user-attachments/assets/5f6a8c60-0bdf-4ab6-a9a0-0188eadf8f69" />

<img width="1581" height="704" alt="image" src="https://github.com/user-attachments/assets/95e1a63f-5b3e-4d46-baf8-ed7276b8f232" />


<img width="1711" height="674" alt="image" src="https://github.com/user-attachments/assets/dd1448b7-caf2-4f51-a8a3-7cadba65fb4e" />

- [ ] you can filter on State:
      - see the average annual salary in total or across  jobs
      - the most required skills
2. Targeted Discovery via Dynamic Slicers
By leveraging the interactive Snowflake Schema architecture, users can perform granular "Deep Dives" using multi-select slicers:

Geographical Analysis (State Filter):

Assess localized earning potential through Average Annual Salary benchmarks.

Extract the Top-Tier Skillsets specifically demanded within a particular region.

### Filtering on Job Title - Data Engineer
<img width="1592" height="723" alt="image" src="https://github.com/user-attachments/assets/cd6dfdcf-e800-4337-9049-20d199fa2ca1" />

<img width="1601" height="712" alt="image" src="https://github.com/user-attachments/assets/2075ecdb-2dbf-4009-852a-fbc98ceeb075" />


<img width="1722" height="702" alt="image" src="https://github.com/user-attachments/assets/e65d3ae2-5c42-4dd3-ae37-2568f1edc3af" />

- [ ] You can filter on Jobs:
      - the highest annusl salary
      - the required skills
      - priveleges (scheule type and health insurance)
      - the most states contains that job

Role-Specific Analysis (Job Title Filter):

Compare Salary Distributions to identify the highest-paying career paths.

Map out the Technical Stack required for specific roles to guide upskilling efforts.

Analyze the "Perks Gap" by seeing which roles offer the best benefits and schedule types.

Cross-Dimensional Filtering:

### 2 Filters

![Uploading image.png…]()


<img width="1716" height="666" alt="image" src="https://github.com/user-attachments/assets/3218048a-73c6-4acd-82e6-50efa2bcb009" />
<img width="1716" height="679" alt="image" src="https://github.com/user-attachments/assets/7f38fa00-95bd-4db9-a52a-34c2ce129d1f" />

- [ ] you can filter over both or between any mix to spot the cross you want to  discover.

Combine multiple filters (e.g., Data Scientist in California at Large Tech Firms) to spot unique market "cross-sections" and tailor your career strategy to real-world data.


### Recommendation
##### based on your /// but for me as example : i woudl say the highest salaries in california and the most reuired id data scientist which is one of my interisting jobs , and i need to learn these skills (...) and i will try my best to  be ready to applicate in the 3rd quarter to have a higher apportunity and match the most companies like (...)

---

# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Data Analytics Enthusiast**

---
