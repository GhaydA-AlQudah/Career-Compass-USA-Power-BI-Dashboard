# 📊 Career Compass USA — BI Insights Dashboard
 
> **Find the Right Career Path Based on Market Insights**

# Problem Statement

Choosing the right tech career path is becoming increasingly difficult;

1. Different roles offer different salaries, hiring demand, benefits, and growth opportunities across U.S. states.
2. Most available information is **scattered across multiple platforms and difficult to compare effectively**.
3. **The required technical skills also vary significantly across roles, industries, and geographic markets**,
   
   making it hard for job seekers to **identify which skills are most valuable in the market**.



As a result, **many career decisions are made based on assumptions instead of real market data**.

---

# The Solution -  *Interactive Strategic Analytics Dashboard

**Imagine having a personal GPS for your tech career!**

- That’s why I built this **Interactive Strategic Analytics Dashboard**: a simple way to explore the U.S. tech job market through data.

- Designed with a clean and intuitive **UX/UI** experience, enabling both technical and **non-technical stakeholders** to explore insights effectively.
  
- It spans **2 pages**, each serving a distinct analytical purpose — from broad market benchmarking to deep skill-level insights.

- Both pages support interactive filtering by:
  
  **Role** — isolate insights for a specific job title
  
  **State** — narrow down to a target geography
  
  Use **Reset Filters** to return to the full market view.


## Market Overview & Hiring Trends

<img width="1590" height="692" alt="image" src="https://github.com/user-attachments/assets/db174062-fa18-4e75-8d05-5dde5f65c277" />


## Skills & Companies Depth Analysis

<img width="1588" height="693" alt="image" src="https://github.com/user-attachments/assets/d400478e-5d83-4f2b-a9bf-504d3d618aac" />


The dashboard answers key career market questions using **slice-and-dice analysis** through interactive filtering by job role, state, or both combined:

- **Which states and roles offer the highest salary benchmarks?**
- **Which companies are hiring the most, and in which locations?**
- **Which job roles are currently the most in-demand?**
- **What technical skills are driving hiring demand and premium salaries?**
- **How are work models (Onsite vs Remote) distributed across the market?**
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

- Transformed encoded and numerical categorical values into clear, human-readable labels for improved usability and Dashboarding clarity.

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

## 4. Dashboard and Storytelling



### Example - Business Insights
- Around **17.8K job opportunities** are available across **6,220 hiring companies**, with an average market salary of **$118.35K**.  

- The **highest-paying roles** are **ML Engineer, Data Scientist, and Data Engineer**.  
  The **most in-demand roles** are **Data Analyst, Data Scientist, and Data Engineer**.  

- **Washington** and **California** offer the highest salary benchmarks, while **California** and **Texas** show the strongest hiring demand.  

- Hiring activity peaks during **Q3**, especially in **August**, with another strong hiring period in **June (Q2)**.  

- Most job postings include **health insurance benefits**, and the majority of opportunities are **full-time positions**.  

- **Remote jobs account for 27.5%** of total opportunities, while onsite roles remain the dominant work model.  

- **SQL** is the **top in-demand technical skill**, followed by **Python** and **Tableau**.  

- The highest-paying and most valuable skill categories are related to **Libraries, Web Frameworks, Cloud, and DevOps**.  

- Companies such as **Meta, TikTok, and Capital One** provide some of the **highest salary packages** in the market.  

- **Robert Half** is the **top hiring company**, leading recruitment demand across multiple roles.  

- Skill distribution analysis shows that **Programming, Analysis Tools, and Cloud skills** are the most required across career paths.  
---

# Recommendation

**Career decisions vary based on individual priorities and career goals**; however, the following recommendation represents a strategic insight derived from the dashboard analysis:

- For professionals seeking the best balance between salary potential, hiring demand, and long-term career growth, pursuing a **Data Engineer** career path in **California** represents a strong strategic choice. While **Washington** offers the highest salary benchmarks, California combines both competitive compensation and the strongest hiring demand, creating broader market opportunities.

- Candidates with skills in **SQL, Python, Cloud, DevOps, and Tableau** are highly aligned with current market requirements and premium-paying roles. Therefore, professionals possessing these technical skills should target **Data Engineering** and **Data Science** positions, while others are encouraged to develop these competencies to improve employability, salary potential, and access to remote and full-time opportunities.

- Professionals targeting premium compensation packages may consider companies such as **Meta, TikTok, and Capital One**, while candidates prioritizing broader hiring opportunities and market accessibility may benefit from applying to high-volume recruiters such as **Robert Half**.
---

# 👤 Author

**By GhaydA' Al-Qudah**

**Computer Engineer | AI & Data Analytics Enthusiast**

---
