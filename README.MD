```


![Click Here](SQL_Result/queries_result_1.png)

## 1. Top Paying Data Analyst Jobs

To identify top paying jobs I filtered Data Analyst positions by average yearly salary and location.

### SQL Query
```sql
SELECT
    job_id,
    job_title,
    company_dim.name,
    job_location,
    job_schedule_type,
    salary_year_avg,
    job_posted_date
FROM
    job_postings_fact
LEFT JOIN company_dim
    ON job_postings_fact.company_id = company_dim.company_id
WHERE
    job_title_short = 'Data Analyst'
    AND job_work_from_home = true
    AND salary_year_avg IS NOT NULL
ORDER BY salary_year_avg DESC
LIMIT 10;
