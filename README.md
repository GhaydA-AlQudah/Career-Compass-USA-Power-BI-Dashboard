#                                                   **Career Compass USA**

# Problem Statement

Choosing the right tech career path is becoming increasingly difficult;

1. Different roles offer different salaries, hiring demand, benefits, and growth opportunities across U.S. states.
2. Most available information is **scattered across multiple platforms and difficult to compare effectively**.
3. **The required technical skills also vary significantly between roles and states**,
   
   making it hard for job seekers to **identify which skills are most valuable in the market**.

As a result, **many career decisions are made based on assumptions instead of real market data**.

---

# **Our Solution: To Find the Right Career Path Based on Market Insights**

**Imagine having a personal GPS for your tech career!**

- That’s why I built this **Interactive Strategic Analytics Report**: a simple way to explore the U.S. tech job market through data.

- Designed with a clean and intuitive **UX/UI** so even **non-technical** users can explore insights comfortably.

## Market Overview & Hiring Trends
<img width="1706" height="740" alt="image" src="https://github.com/user-attachments/assets/515d3fe6-329c-4adc-ab15-87544aea7ebe" />

## Skills & Companies Depth Analysis
<img width="1706" height="738" alt="image" src="https://github.com/user-attachments/assets/c3ed6e83-56c9-479b-97e2-3a00af9573aa" />

**With this dashboard, users can:**
- Compare career paths by exploring salary benchmarks, hiring demand, work models, and employee benefits across different tech roles.

- Perform **slice-and-dice analysis** through interactive filtering by job role, state, or both combined 
to uncover targeted labor market trends, salary patterns, and high-demand career opportunities.


---
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
| `company_id` | `company_dim_table` |Integer | Unique identifier for each hiring organization (Primary Key). |
| `name` | `company_dim_table` | String | The name of the hiring organization. |
| `skill_id` | `skills_dim_table` | Integer | Unique identifier for each technical skill (Primary Key). |
| `skills` | `skills_dim_table` | String | The name of the specific skill (e.g., Python, Azure, SQL). |
| `type` | `skills_dim_table` | String | Categorization of the skill (e.g., Programming, Cloud, Databases). |
| `job_id` | `skill_job_dim_table` | Integer | Foreign Key linking each job to its required technical skills (corresponds to `Jobs` in `job_fact`). |
| `skill_id` | `skill_job_dim_table` | Integer | Foreign Key linking the job record to the specific skill details in `skills_dim_table`. |

### Dataset Overview
Total Records: 17,788 cleaned rows (after filtering for major states and removing outliers).

Time Scope: Data reflects job postings as of late 2023.

Data Integrity: 100% validity across key columns with no nulls in the final transformed set.

Granularity: The data is at the "Individual Job Posting" level.

---
## 2. Data Cleaning & Transformation
Applied data transformation and preprocessing using **Power Query (M Language)**, while leveraging **DAX** for dynamic calculations and analytical measures within Power BI.
- Removed empty rows, null values, and data inconsistencies to improve data quality and analytical accuracy.
   
- Applied geospatial normalization by mapping cities to their corresponding US states and filtered the dataset
  
   to focus specifically on US tech-related jobs and major tech hub locations.


- Performed feature selection by removing irrelevant and redundant columns to optimize the data model.

- Engineered a unified Annual Salary metric by standardizing hourly, monthly, and varying salary structures into a single comparable measure.

- Transformed encoded and numerical categorical values into clear, human-readable labels for improved usability and reporting clarity.

- Standardized multiple work schedule formats into unified categories such as Full-time, Contract, and Internship.
---
## 3. Data Modeling 

### Star Schema with a Bridge Table for Many-to-Many Relationships


<img width="1431" height="496" alt="image" src="https://github.com/user-attachments/assets/6f86e66e-67b2-43fb-aab9-5102db7afdd2" />


### Cross-Filter Direction

```
[company_dim_table] (1)
                   │
                   ▼ (Single Direction)
               [job_fact] (*)
                   │
                   ▲
                   ▼ (Both Directions)
        [skill_job_dim_table] (*)
                   ▲
                   │ (Single Direction)
        [skills_dim_table] (1)
```
---

## 4. Dashboard and Storyteling



### Example

Key Insights — Career Compass USA
1. Data Engineering Leads in Salary
Data Engineering roles have the highest average salary at approximately 147.8K USD.
This is significantly higher than:
Business Analysis (~105K)
Data Analysis (~98K)
Indicates strong market value for advanced data infrastructure and pipeline skills.
2. Data Analyst Roles Have the Highest Hiring Demand
Data Analysis positions dominate hiring demand with the largest number of open opportunities.
Suggests lower entry barriers and broader adoption across industries.
While salaries are lower than engineering roles, job accessibility is significantly higher.
3. California Dominates Hiring Opportunities
California has the highest hiring demand among analyzed states.
Indicates it remains the strongest tech employment hub despite salary competition from other states.
4. Washington Offers the Highest Salaries
Washington shows the highest average salary levels across tech jobs.
Likely influenced by concentration of major tech companies and cloud infrastructure roles.
5. Hiring Activity Peaks Mid-Year
Hiring trends increase noticeably around:
June
August
Suggests companies expand recruitment during mid-year growth cycles and Q3 planning periods.
6. Full-Time Roles Dominate the Market
Nearly 80% of postings are full-time positions.
Contract, internship, and part-time opportunities represent a much smaller share.
Indicates market stability for long-term tech careers.
7. Health Benefits Are Common but Not Universal
Slightly more than half of job postings include health insurance benefits.
A considerable portion still offers no listed healthcare coverage, highlighting variation in employer compensation packages.
8. Strong Relationship Between Skills and Compensation
Higher-paying roles such as Data Engineering are typically associated with specialized technical skills.
Roles with broader hiring demand tend to require more general analytical toolsets.
This suggests that skill specialization directly impacts earning potential.
Strategic Takeaways
Candidates seeking higher salaries should focus on advanced engineering and cloud/data infrastructure skills.
Candidates prioritizing job availability may benefit from pursuing analytical and reporting-focused roles.
Geographic location significantly affects both compensation and opportunity volume.
Skill development is a key differentiator in long-term tech career growth.
---
# Recommendation
**Career decisions vary based on individual priorities and career goals**; however, these examples represent strategic insights derived from the dashboard analysis:

1. Candidates prioritizing **compensation optimization and long-term career value** should consider Data Engineering roles in Washington, where the dashboard indicates a combination of premium salary benchmarks, stable full-time demand, and strong employer investment in benefits — signaling a mature and competitive talent market.
   
2. Professionals seeking **a balanced career path between accessibility, hiring volume, and geographic flexibility** may find Data Analyst roles more strategic, especially within California and remote-friendly markets, where high demand, scalable hiring activity, and flexible workforce distribution create stronger entry and growth opportunities.
---

# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Data Analytics Enthusiast**

---
