# 📊 Career Compass USA — BI Insights Report
 
> **Find the Right Career Path Based on Market Insights**

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

- It spans **2 pages**, each serving a distinct analytical purpose — from broad market benchmarking to deep skill-level insights.


## Market Overview & Hiring Trends

<img width="1702" height="736" alt="image" src="https://github.com/user-attachments/assets/ca3cc9ae-3de7-45e2-aad7-dbbd53142104" />

## Skills & Companies Depth Analysis

<img width="1705" height="737" alt="image" src="https://github.com/user-attachments/assets/8b101375-962b-4caf-ad3b-64b39a6031f6" /> 

## Data Filters Available
 
Both pages support interactive filtering by:
- **Role** — isolate insights for a specific job title
- **State** — narrow down to a target geography
  
Use **Reset Filters** to return to the full market view.

The dashboard answers three core business questions using **slice-and-dice analysis** through interactive filtering by job role, state, or both combined :
- **Where is the market paying the most?**
- **Who is hiring, and where?**
- **What skills and work models are driving demand?**

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

Business Insights
The dashboard delivers a multi-dimensional view of the US data and AI job market by combining workforce demand, salary intelligence, skill distribution, hiring behavior, and work model trends into a unified analytical experience.
Cross-page analysis reveals a strong relationship between high-paying career paths and infrastructure-oriented technical skills, where Data Engineering, Cloud, Databases, and SQL-driven capabilities consistently align with premium compensation benchmarks.
Market demand and compensation are not perfectly correlated; while Data Analyst roles dominate hiring volume, more specialized engineering-oriented roles generate stronger salary performance, highlighting the distinction between market accessibility and market value.
The interaction between the “Top In-Demand Technical Skills” and “Salary Benchmarks by Skill Type” visuals demonstrates that foundational technologies such as SQL and Python drive large-scale hiring demand, while advanced infrastructure ecosystems create higher monetization potential.
Recruitment activity is heavily concentrated around enterprise hiring platforms and staffing-driven organizations, indicating a highly competitive and rapidly scaling talent acquisition landscape within the US tech sector.
Workforce flexibility continues to reshape hiring dynamics, as remote opportunities maintain a significant market share, reinforcing the shift toward distributed and hybrid-first operational models.
The dashboard uncovers interconnected skill clusters across career roles, showing that modern data careers increasingly require hybrid competency models rather than isolated technical specialization.
Comparative analysis across hiring demand, compensation benchmarks, and work model distribution suggests that organizations are balancing scalability, technical depth, and workforce flexibility simultaneously when shaping recruitment strategies.
Temporal hiring analysis highlights noticeable hiring acceleration periods across the year, emphasizing the impact of seasonal workforce planning and business expansion cycles on recruitment behavior.
The integration of role-based filtering and geographic analysis enables slice-and-dice exploration across multiple business dimensions, transforming raw labor market data into actionable workforce intelligence.

---
# Recommendation
**Career decisions vary based on individual priorities and career goals**; however, these examples represent strategic insights derived from the dashboard analysis:

1. Candidates prioritizing **compensation optimization and long-term career value** should consider Data Engineering roles in Washington, where the dashboard indicates a combination of premium salary benchmarks, stable full-time demand, and strong employer investment in benefits — signaling a mature and competitive talent market.
   
2. Professionals seeking **a balanced career path between accessibility, hiring volume, and geographic flexibility** may find Data Analyst roles more strategic, especially within California and remote-friendly markets, where high demand, scalable hiring activity, and flexible workforce distribution create stronger entry and growth opportunities.

Professionals seeking a balanced career strategy between hiring accessibility, workforce flexibility, and sustainable career growth may find Data Analyst and analytics-focused roles more strategic, especially within remote-friendly and high-volume markets, where the combination of strong hiring demand, transferable technical skills, and flexible work models creates broader entry and progression opportunities across the data ecosystem.

---

# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Data Analytics Enthusiast**

---
