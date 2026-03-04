# 🧹 Messy Employee Dataset — Data Analytics Project

An end-to-end data analytics project using a messy HR/employee dataset. This project covers data cleaning, SQL data modeling, exploratory data analysis, and an interactive Power BI dashboard to answer real business questions about workforce performance, compensation, and retention.

---

## 📁 Files

| File | Description |
|---|---|
| `Messy_Employee_dataset.csv` | Raw, uncleaned dataset |
| `Messy_Employee_dataset_Cleaned.csv` | Cleaned dataset ready for analysis |
| `Messy_Employee_Dataset_Cleaned.ipynb` | Python notebook for data cleaning |
| `messy_employee - table_queries.sql` | SQL script to create and normalize tables |
| `messy_employee - analysis_queries.sql` | SQL queries to answer business questions |
| `Messy_Employee - ExploratoryDataAnalysis.ipynb` | Python notebook for exploratory data analysis |
| `Messy_Employee - DataVisualization.pbix` | Power BI dashboard file |

---

## 🛠️ Tools Used

- **Excel** — Preliminary data cleaning
- **Python (Pandas)** — Data cleaning and transformation
- **Python (Matplotlib)** — Data visualization
- **Python (Seaborn)** — Data visualization
- **PostgreSQL** — Data modeling and analysis
- **Power BI** — Interactive dashboard and visualization

---

## 🔄 Workflow

### 1. Data Cleaning
The raw dataset contained inconsistencies, formatting issues, and missing values. Cleaned using both **Excel** and **Python (Pandas)**.

### 2. SQL Data Modeling
The cleaned flat CSV was imported into PostgreSQL and normalized into 4 relational tables:
- `employees` — Core employee info with `Department_ID` as foreign key
- `departments` — Department reference table
- `salaries` — Employee salary records
- `performance` — Employee performance scores

### 3. SQL Analysis
Business questions answered using JOINs, CTEs, and aggregate functions across the normalized tables.

### 4. Exploratory Data Analysis (EDA)
Performed in Python using Pandas, Matplotlib, and Seaborn. The EDA covers univariate, bivariate, and multivariate analysis across salary, age, performance, department, remote work, and employee status.

### 5. Power BI Dashboard
An interactive dashboard built on top of the normalized PostgreSQL tables. Includes slicers for remote work filtering and KPI cards for high-level metrics.

---

## 📊 Power BI Dashboard

Connected directly to the normalized PostgreSQL tables via Power BI Desktop. Relationships were set up in Model view with `employees` as the central table.

**Visuals:**
| Visual | Fields Used |
|---|---|
| KPI Card — Total Employees | COUNT(employee_id) |
| KPI Card — Avg Age | AVERAGE(age) |
| Bar Chart — Department Salary (Avg) | department_name, AVG(salary) |
| Bar Chart — Highest Salary | first_name + last_name, AVG(salary) Top 10 |
| Bar Chart — Region Salary (Avg) | region, AVG(salary) |
| Bar Chart — Department Performance | department_name, AVG(performance_score) |
| Donut Chart — Employee Status | status, COUNT(employee_id) |
| Line Chart — Hiring Trend | join_date (Year), COUNT(employee_id) |
| Slicer — Remote Work | Remote / On-Site |

**DAX Measures Used:**
```dax
Avg Salary = AVERAGE(salaries[salary])
Total Employees = DISTINCTCOUNT(employees[employee_id])
Avg Age = AVERAGE(employees[age])
Remote Label = IF(employees[Remote_Work] = 1, Remote, On-Site)
```

---

## ❓ Business Questions Answered

- What is the average salary per department?
- Which department has the most high performers?
- What is the remote work distribution per department?
- How many employees are Active, Pending, and Inactive per department?
- Who are the top 10 highest paid employees?
- Which region pays the most on average?
- How many employees joined per year?

---

## 📊 Dataset Overview

| Column | Description |
|---|---|
| `Employee_ID` | Unique employee identifier |
| `First_Name` / `Last_Name` | Employee name |
| `Age` | Employee age |
| `Department` | Department name |
| `Region` | Work region/state |
| `Status` | Active, Inactive, or Pending |
| `Join_Date` | Date the employee joined |
| `Salary` | Annual salary |
| `Email` / `Phone` | Contact information |
| `Performance_Score` | Score from 1 (lowest) to 4 (highest) |
| `Remote_Work` | 1 = Remote, 0 = On-site |

**Dataset size:** 1,020 employees across 6 departments and 6 regions. Salary ranges from $50,000 to $120,000.

---

## 📈 EDA — Visualizations & Insights

### 1. Salary Distribution
> *Histogram with KDE curve*

The salary distribution is approximately **normal (bell-shaped)**. Most employees earn between **$80,000–$90,000**, representing the peak of the distribution. No significant outliers were detected on either end.

---

### 2. Age Distribution
> *Count plot across age groups: 25, 30, 35, 40*

The age distribution is **right-skewed**, with the majority of employees aged **30**. The workforce is relatively young, with fewer employees in the 35–40 age range, suggesting a younger overall talent pool.

---

### 3. Performance Score Distribution
> *Count plot across scores 1–4*

The majority of employees scored **3 out of 4**, indicating above-average performance is the norm. Very few employees fall at the lowest score of 1, suggesting that poor performance is uncommon in this organization.

---

### 4. Employee Status Breakdown
> *Count plot: Active, Pending, Inactive*

The **Pending** status is the most common, followed by Active and Inactive. The high volume of Pending employees may point to a **recent surge in hiring** or a **slow onboarding process**. The low Inactive count reflects decent overall retention.

---

### 5. Salary per Department
> *Box plot: Department vs. Salary*

**HR** has the highest median salary, while **Finance** has the lowest — which is unexpected, as Finance roles are typically among the higher paid. Most departments show similar medians, suggesting standardized pay. **DevOps** and **Finance** show the widest salary spread, indicating larger internal pay gaps.

---

### 6. Performance per Department
> *Box plot: Department vs. Performance Score*

Most departments share a **median performance score of 3**, showing consistent output across the organization. **Cloud Tech** stands out with the lowest median performance and may benefit from additional management attention or support.

---

### 7. Salary vs. Age
> *Strip plot with jitter*

There is **no clear relationship** between age and salary. Employees across all age groups (25, 30, 35, 40) show a similar salary range of $50,000–$120,000, suggesting compensation is driven by factors other than seniority or age — likely **department or role**.

---

### 8. Remote Work vs. Performance
> *Bar plot: Remote vs. On-Site average performance*

Remote and on-site employees show **nearly identical average performance scores (~2.5)**. Work location has no significant impact on performance, suggesting the organization can confidently **expand remote work policies** without risking a decline in output.

---

### 9. Correlation Heatmap
> *Heatmap of Age, Salary, Performance Score, Remote Work*

No significant correlations exist between any of the four numeric variables. The highest pair — **Age and Salary — correlates at only 0.07**, which is extremely weak. Salary and performance decisions appear to be largely **independent of each other and of age**.

---

### 10. Department × Salary × Performance
> *Box plot with hue: Performance Score*

Across most departments, **high performers (score 4) do not consistently earn more than low performers (score 1)**. This suggests salary is not strongly tied to performance, which could be a **retention risk** — top performers may feel underrewarded over time.

---

## 🔍 Key Findings Summary

| # | Finding |
|---|---|
| 1 | Salary is approximately normally distributed, centered around $80K–$90K |
| 2 | Workforce skews young — majority of employees are aged 30 |
| 3 | Most employees score 3/4 on performance; poor performance is rare |
| 4 | High Pending employee count may signal onboarding bottlenecks |
| 5 | HR has the highest median salary; Finance unexpectedly the lowest |
| 6 | Remote work has no measurable impact on performance |
| 7 | No significant correlation between age, salary, performance, or remote work |
| 8 | Salary is not tied to performance — potential long-term retention concern |
