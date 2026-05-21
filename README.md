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

- That’s why I built this **Interactive Strategic A nalytics dashboard**: a simple way to explore the U.S. tech job market through data.

- Designed with a clean and intuitive **UX/UI** so even **non-technical** users can explore insights comfortably.


<img width="1702" height="736" alt="image" src="https://github.com/user-attachments/assets/eb6b8e26-1b4d-4a00-8201-f4813f3b547e" />

<img width="1706" height="736" alt="image" src="https://github.com/user-attachments/assets/aab1beea-ffd9-4cff-981a-b041b7bf9b79" />


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

<img width="1697" height="768" alt="image" src="https://github.com/user-attachments/assets/8678ceb4-b6f4-4ff8-9b99-27ee77f29e3c" />

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
