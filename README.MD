
```
SELECT
    ci.course_id,
    ci.course_title,
    sl_summary.total_learners,
    sl_summary.total_hours_watched,
    cr_summary.avg_course_rating
FROM course_info ci
LEFT JOIN (
    SELECT
        course_id,
        COUNT(DISTINCT student_id) AS total_learners,
        round(SUM(minutes_watched) / 60, 2) AS total_hours_watched
    FROM student_learning
    GROUP BY course_id
) sl_summary ON ci.course_id = sl_summary.course_id
LEFT JOIN (
    SELECT
        course_id,
        ROUND(AVG(course_rating), 2) AS avg_course_rating
    FROM course_ratings
    GROUP BY course_id
) cr_summary ON ci.course_id = cr_summary.course_id
ORDER BY
    sl_summary.total_hours_watched DESC,
    cr_summary.avg_course_rating DESC;

## Output:

![Click Here](SQL_Result/queries_result_1.png)

