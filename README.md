# *CareerPulse-USA Interactive Dashboard*

# Problem Statement
Choosing the right tech career path is becoming increasingly difficult.
Different roles offer different salaries, hiring demand, benefits, and growth opportunities across U.S. states.

For students, job seekers, and professionals, finding reliable and easy-to-understand market insights can be challenging. Most available information is scattered across multiple platforms and difficult to compare effectively.

As a result, many career decisions are made **based on assumptions instead of real market data**.

---

# **Our Solution: Your Interactive Strategic Career Navigator**

**Imagine having a personal GPS for your tech career!**

That’s why I built this **Interactive Strategic A nalytics dashboard**: a simple way to explore the U.S. tech job market through data.



<img width="1582" height="687" alt="image" src="https://github.com/user-attachments/assets/becdb76b-f2d8-4ddb-96ce-4f0fa1789855" />

## *With this dashboard, users can:*

• Compare career paths

  Explore salaries, hiring demand, benefits, and work types across different tech roles.

• Analyze opportunities by state

  See which locations offer better compensation and stronger market demand.

• Make data-driven career decisions

  Use real market insights instead of assumptions when planning the next career move.

• Navigate easily

  The dashboard is designed with a clean and intuitive **UX/UI** so even **non-technical** users can explore insights comfortably.


## *What’s Behind the Dashboard?*

While the experience is designed to feel simple, the project involved several data engineering and analytics steps behind the scenes:

• Data Preparation (Python(Pandas) )

  Cleaned and transformed raw datasets to improve data quality and consistency.

• Data Modeling (**OLAP** & Star Schema)

  Built a structured analytical model using a **Star Schema** design to support scalable and efficient analysis.

• **Business Intelligence** (Power BI, Power Query & DAX)

  Created an interactive dashboard with **dynamic filtering** and responsive visual insights.
  **Power Query (M Language)** was used for data transformation and preprocessing, 
  while **DAX** was used to create dynamic measures and analytical calculations within the Power BI model.


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

Data Integrity: 100% validity across key columns with no nulls in the final transformed set.

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

<img width="1584" height="705" alt="image" src="https://github.com/user-attachments/assets/f5d6dfa8-db32-47af-ae69-d91b1c15e6b6" />


- [ ]  you can take a quick look to see what the most required Job title, which state contain the most tech jobs, which companies in each state, the privileges like health insurance, the flexibility of the schule type across jobs, states, companies, and the annual salary

1. High-Level Market Overview
At a glance, the dashboard provides a macro perspective of the industry, allowing you to:

Identify Market Leaders: Pinpoint which job titles dominate the current landscape and which states serve as the primary tech hubs.

Corporate Benchmarking: Discover top-hiring companies filtered by state and industry presence.

Holistic Compensation Analysis: Evaluate "quality of life" metrics, including health insurance availability and work-schedule flexibility (Remote vs. On-site), alongside traditional salary data.

### Example 2 : Filtering on California State

<img width="1588" height="706" alt="image" src="https://github.com/user-attachments/assets/26d94757-a366-4fb9-8e3f-d85a90b0dacb" />

<img width="1587" height="709" alt="image" src="https://github.com/user-attachments/assets/4124111a-b7bf-41a9-83f6-de569ea3be5b" />

- [ ] you can filter on State:
      - see the average annual salary in total or across  jobs
      - the most required skills
2. Targeted Discovery via Dynamic Slicers
By leveraging the interactive Snowflake Schema architecture, users can perform granular "Deep Dives" using multi-select slicers:

Geographical Analysis (State Filter):

Assess localized earning potential through Average Annual Salary benchmarks.

Extract the Top-Tier Skillsets specifically demanded within a particular region.

### Filtering on Job Title - Data Engineer

<img width="1585" height="720" alt="image" src="https://github.com/user-attachments/assets/17cef522-1c0e-416c-9847-172c5a60973a" />


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

<img width="1581" height="704" alt="both_filters" src="https://github.com/user-attachments/assets/fe155709-84a8-451a-88cc-2063b22b132a" />



- [ ] you can filter over both or between any mix to spot the cross you want to  discover.

Combine multiple filters (e.g., Data Scientist in California at Large Tech Firms) to spot unique market "cross-sections" and tailor your career strategy to real-world data.


### Recommendation
##### based on your /// but for me as example : i woudl say the highest salaries in california and the most reuired id data scientist which is one of my interisting jobs , and i need to learn these skills (...) and i will try my best to  be ready to applicate in the 3rd quarter to have a higher apportunity and match the most companies like (...)

---

# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Data Analytics Enthusiast**

---
