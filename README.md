#                                                   **Career Compass USA**

# Problem Statement

Choosing the right tech career path is becoming increasingly difficult.

1. Different roles offer different salaries, hiring demand, benefits, and growth opportunities across U.S. states.
2. Most available information is **scattered across multiple platforms and difficult to compare effectively**.

As a result, **many career decisions are made based on assumptions instead of real market data**.

---

# **Our Solution: To Find the Right Career Path Based on Market Insights**

**Imagine having a personal GPS for your tech career!**

- That’s why I built this **Interactive Strategic A nalytics dashboard**: a simple way to explore the U.S. tech job market through data.

- Designed with a clean and intuitive **UX/UI** so even **non-technical** users can explore insights comfortably.



<img width="1582" height="687" alt="image" src="https://github.com/user-attachments/assets/becdb76b-f2d8-4ddb-96ce-4f0fa1789855" />

## *With this dashboard, users can:*

Compare career paths by exploring salary benchmarks, hiring demand, work models, and employee benefits across different tech roles.

Perform **slice-and-dice analysis** through interactive filtering by job role, state, or both combined 
to uncover targeted labor market trends, salary patterns, and high-demand career opportunities.

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

### Snowflake Schema

<img width="1485" height="537" alt="image" src="https://github.com/user-attachments/assets/bce0bbd2-c9b5-47a5-ad73-cf92976811eb" />



### Single Cross-Filter Direction

```
[company_dim_table] (1)  ──┐
                           │
                           ▼
                        [job_fact] (*) ── (1) ──┐
                                                │
                                                ▼
                                        [skill_job_dim_table] (*) ── (*) ── [skills_dim_table] (1)                                      
```

## 4. Data Cleaning: 

a. Empty rows and Errors Removed.

b. Applied filters to scope the data specifically to US Tech Hubs, ensuring the analysis remains relevant to the targeted market.

c. Feature Selection : Unrelevant Columns removed

d. Feature Extraction: Annual Salary calculated from different columns to unify hourly, monthly, and varying compensation structures into a single standardized metric, enabling accurate *cross-functional* analysis.


e. Transformation:  **Power Query (M Language)** was used for data transformation and preprocessing, 
                      while **DAX** was used to create dynamic measures and analytical calculations within the Power BI model.

1. Transformed encoded numerical values into human-readable, meaningful labels.
2. Geospatial Normalization: Mapped specific cities into their respective US States to enable high-level geographical grouping.
3. Standardized various schedule_type entries into unified categories (e.g., Full-time, Contract, Internship).

f. Outliers: Identified and handled statistical anomalies and extreme wage values to prevent distortion in descriptive metrics and average charts.


## 5. Dashboard and Storyteling



### Example 1 : Without Filtering

This view provides **a high-level overview of the US tech job market**, allowing users to quickly identify the most in-demand job roles, top hiring states, hiring trends, compensation benchmarks, work model flexibility, health insurance availability, and overall market distribution across roles, companies, and locations.

<img width="1584" height="705" alt="image" src="https://github.com/user-attachments/assets/f5d6dfa8-db32-47af-ae69-d91b1c15e6b6" />


1. ML Engineer and Data Scientist roles offer the highest average salaries in the market, highlighting the premium value of advanced AI and analytics skills.
   
2. Data Analyst and Data Scientist positions show the highest job demand, indicating that companies are actively hiring for data-driven decision-making roles.

3. Washington has the highest average salary among all states, while California maintains a strong balance between high salaries and high job availability.

4. Full-time positions **dominate** the market, accounting for nearly 76% of all job postings, which reflects employers’ preference for long-term hires.

5. More than half of the listed jobs provide health insurance benefits, showing how companies use benefits packages to attract skilled talent.

6. Hiring activity peaks during Q3, especially around August, before gradually declining toward the end of the year.

7. High-paying roles such as ML Engineer have lower hiring demand compared to roles like Data Analyst, demonstrating the gap between salary level and market demand.
    
8. The presence of “Anywhere” among top hiring locations suggests a strong rise in remote work opportunities across the tech and data industry.
 
9. The dashboard highlights a clear trend: companies prioritize scalable data and AI capabilities, driving both salary growth and hiring demand in analytical roles.

10. Mid-level analytical roles appear more accessible and widely available, while specialized AI-focused positions remain higher-paying but more competitive.


### Example 2 : Both Filters

Apply multiple filters simultaneously **to uncover specific market cross-sections and generate more targeted insights**.
Combining filters such as job role, state, or state enables deeper analysis of hiring demand, compensation patterns, workforce flexibility, and regional opportunities — helping users align career decisions with real market trends.

<img width="1581" height="704" alt="both_filters" src="https://github.com/user-attachments/assets/fe155709-84a8-451a-88cc-2063b22b132a" />


1. The filtered view reveals a more specialized talent market with reduced hiring volume but higher compensation value.

2. Data Engineering remains the premium-paying role, while Data Analyst positions continue to dominate workforce demand.

3. Washington leads salary performance, whereas California drives the highest hiring activity, reflecting different regional market dynamics.

4. The hiring trend shows a sharp Q3 spike, indicating concentrated recruitment cycles and accelerated talent acquisition.

5. The dashboard highlights how niche technical skills increase compensation, even within a smaller hiring pool.

6. Workforce demand is heavily concentrated in full-time opportunities, reinforcing long-term hiring strategies.

7. The analysis demonstrates a clear trade-off between market demand and salary optimization.

8. Filtered insights expose how organizations prioritize specialized data capabilities over workforce scale.

9. The dashboard translates segmented hiring data into targeted labor market intelligence.

10. The selected filters uncover a more competitive and high-value segment of the analytics job market.

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
