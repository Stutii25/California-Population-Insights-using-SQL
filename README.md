# 📊 California Population Insights using SQL

## 1. Introduction

This project focuses on the analysis of California's projected population data. It uses **MySQL** to create a database, load population data, and extract valuable insights. The dataset includes breakdowns by county, race, gender, and age group for various years between 2010 and 2060.

---

## 2. Data Source

| Source Description             | URL                                                                 |
|-------------------------------|----------------------------------------------------------------------|
| California Open Data Portal   | [Link](https://data.ca.gov/dataset)                                 |
| Dataset used in this project  | [Link](https://data.ca.gov/dataset/ca-educational-attainment-personal-income) |

---

## 3. Tools Used

| Tool         | Purpose                                      |
|--------------|----------------------------------------------|
| MySQL        | Creating schema, loading and analyzing data  |
| SQL Queries  | Extracting specific insights from the data   |

---

## 4. Step-by-Step Project Workflow

### A. Database Creation & Data Loading

| Step              | Description                                                                 |
|-------------------|-----------------------------------------------------------------------------|
| Schema Creation   | A new schema named `ca_population` was created.                            |
| Table Definition  | Table `pop_proj` was created with columns for county code, name, race, gender, age, year, and population. |
| Data Insertion    | Data was loaded from a CSV file using `LOAD DATA LOCAL INFILE`.            |
| Data Sample       | Queried first 10 rows to verify successful loading.                         |

> **SQL Code Used**:  
> ```sql  
> CREATE DATABASE ca_population;  
> USE ca_population;  
> CREATE TABLE pop_proj (...);  
> LOAD DATA LOCAL INFILE 'filename.csv' INTO TABLE pop_proj ...;  
> SELECT * FROM pop_proj LIMIT 10;  
> ```

---

### B. Data Analysis (Using SQL Queries)
![image](https://github.com/user-attachments/assets/6ad3e598-813b-4815-b2fa-bba9cbd5b388)


#### 1. Creating Index for Better Performance

| Index Name   | Indexed Column |
|--------------|----------------|
| county_name  | county_name    |

> **SQL**:  
> ```sql
> CREATE INDEX county_name ON pop_proj(county_name);
> ```

#### 2. Population Summary by Gender for the Year 2014

**Purpose**: To get the population of males and females in each county in 2014.

| Query Action | Description                                |
|--------------|--------------------------------------------|
| Grouping     | Population is grouped by county and gender |
| Filtering    | Data is filtered for the year 2014         |
| Aggregation  | Total population for each gender is calculated |

> **SQL Query**:  
> ```sql
> SELECT county_name, gender, SUM(population) AS total_population  
> FROM pop_proj  
> WHERE date_year = 2014  
> GROUP BY county_name, gender  
> ORDER BY county_name;
> ```

#### 3. Male vs Female Population Table (2014)

| Column       | Description                        |
|--------------|------------------------------------|
| county_name  | Name of the county                 |
| Male         | Total male population in 2014      |
| Female       | Total female population in 2014    |

![image](https://github.com/user-attachments/assets/32bfa3c0-2e38-48cd-9a35-19e916576a73)


> Combine male and female population data side-by-side using conditional aggregation or subqueries.

---

## 5. Challenges Faced

| Challenge                          | Resolution                                              |
|-----------------------------------|---------------------------------------------------------|
| `LOCAL INFILE` disabled           | Enabled it via MySQL command line configuration         |
| Large dataset load & optimization | Used indexing on `county_name` to improve performance   |

---

## 6. Key Learnings

- Learned how to create and structure a database schema for population data.
- Gained skills in loading CSV data into MySQL using efficient methods.
- Practiced SQL aggregate functions and filtering to extract targeted information.
- Learned how indexing improves performance in real-world analysis.

---

## 7. Conclusion

This project demonstrates how **SQL** can be used to efficiently manage and analyse large-scale demographic datasets. It helps in identifying population trends across counties by gender and year — which is useful for **government planning**, **public services**, and **research**.
