# Windows Functions and Ordered Data in SQL

## Project Description

This project explores advanced SQL window functions and ordered data operations, enabling powerful analytics and comparisons within grouped data. These functions, such as `RANK`, `ROW_NUMBER`, `LAG`, and `LEAD`, provide insights into relative positions, trends, and patterns across partitions. They are indispensable for advanced reporting and analysis tasks.

---

## Key Concepts and Examples

### **1. Partitioned Aggregations**
- **Objective:** Compare individual rows against group-level aggregations using `PARTITION BY`.
- **Examples:**
  - Employee salary vs. average salary in their department:
    ```sql
    SELECT 
        department, 
        last_name, 
        salary,
        AVG(salary) OVER (PARTITION BY department) AS department_avg_salary
    FROM staff;
    ```
  - Employee salary vs. minimum salary in their company region:
    ```sql
    SELECT 
        company_regions, 
        last_name, 
        salary,
        MIN(salary) OVER (PARTITION BY company_regions) AS region_min_salary
    FROM vw_staff_div_reg;
    ```

---

### **2. First and Last Values**
- **Objective:** Retrieve the first or last value in a group using `FIRST_VALUE` or `LAST_VALUE`.
- **Examples:**
  - Get the highest salary in each department:
    ```sql
    SELECT
        department,
        last_name,
        salary,
        FIRST_VALUE(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS highest_salary
    FROM staff;
    ```
  - Compare salaries against the first alphabetical last name in the department:
    ```sql
    SELECT
        department,
        last_name,
        salary,
        FIRST_VALUE(salary) OVER (PARTITION BY department ORDER BY last_name ASC) AS first_alphabetical_salary
    FROM staff;
    ```

---

### **3. Ranking Functions**
- **Objective:** Rank employees based on specific criteria within groups.
- **Examples:**
  - Rank employees by salary within their departments:
    ```sql
    SELECT
        department,
        last_name,
        salary,
        RANK() OVER (PARTITION BY department ORDER BY salary DESC) AS salary_rank
    FROM staff;
    ```
  - Assign unique row numbers by salary in each department:
    ```sql
    SELECT
        department,
        last_name,
        salary,
        ROW_NUMBER() OVER (PARTITION BY department ORDER BY salary DESC) AS row_number
    FROM staff;
    ```

---

### **4. LAG and LEAD Functions**
- **Objective:** Compare a row’s values to the previous or next row within a group.
- **Examples:**
  - Compare salaries with the previous row in the department:
    ```sql
    SELECT 
        department,
        last_name,
        salary,
        LAG(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS previous_salary
    FROM staff;
    ```
  - Compare salaries with the next row in the department:
    ```sql
    SELECT 
        department,
        last_name,
        salary,
        LEAD(salary) OVER (PARTITION BY department ORDER BY salary DESC) AS next_salary
    FROM staff;
    ```

---

### **5. NTILE for Binning**
- **Objective:** Divide rows into equal-sized buckets based on a specific ordering.
- **Examples:**
  - Assign employees to 10 salary bins within their departments:
    ```sql
    SELECT 
        department,
        last_name,
        salary,
        NTILE(10) OVER (PARTITION BY department ORDER BY salary DESC) AS salary_bin
    FROM staff;
    ```

---

## Tools and Environment
- **Database Management Systems:** PostgreSQL, MySQL
- **Setup Requirements:**
  - Load the relevant tables (`staff`, `vw_staff_div_reg`) into your database.
  - Execute the queries sequentially to explore window functions and their outputs.

---

## Learning Outcomes
- Master window functions like `PARTITION BY`, `RANK`, `ROW_NUMBER`, `LAG`, and `LEAD`.
- Gain insights into ordered data through aggregation, ranking, and comparisons.
- Use advanced binning techniques with `NTILE` for clustering data points.

---

## Use Cases
- **Performance Analysis:** Rank employees or compare their performance within departments or regions.
- **Trend Analysis:** Identify patterns in ordered data using relative comparisons.
- **Clustering:** Group data points into meaningful categories using binning techniques.

---

## Acknowledgments
This repository highlights essential SQL window functions and their applications, empowering users to tackle advanced data analytics challenges effectively.
