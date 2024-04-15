# Career-Track-Analysis
## Project Overview
The project aims to analyze enrollment and achievement data of students in 365's career tracks using SQL and Tableau. By examining enrollment patterns, course completion rates, and exam performance, the objective is to identify trends and insights that can inform improvements to the career track programs. Ultimately, the project seeks to optimize the learning experience and enhance student success in obtaining career certificates.

## Data Sources
The dataset includes following files:
- career_track_info
- career_track_student_enrollment
  
Here is a preview of the data.
  
  ``` {sql}
  select * from sql_and_tableau.career_track_info;
  ```
  ![1](https://github.com/alinah1214/Career-Track-Analysis/assets/149886043/0c39d575-cdc1-4550-af08-4d7d182c138f)

  ``` {sql}
  select * from sql_and_tableau.career_track_info
  limit 10;
  ```
  
![2](https://github.com/alinah1214/Career-Track-Analysis/assets/149886043/30354671-6490-4cf2-994d-c316a0600932)


## Tools Used
- SQL - Data Preparation
- Tableau- Data Visualization
  
## Data Preparation
To analyze the data, it is necessary to join data from different tables and perform calculations, which is done in SQL.

  ``` {sql}
  select
student_track_id,
student_id,
track_name,
date_enrolled,
track_completed,
days_for_completion,
 case
WHEN days_for_completion = 0 THEN 'Same day' 
when days_for_completion between 1 and 7 then  '1 to 7 days'
when days_for_completion between 8 and 30 then  '8 to 30 days'
when days_for_completion between 31 and 60 then  '31 to 60 days'
when days_for_completion between 61 and 90 then  '61 to 90 days'
when days_for_completion between 91 and 365 then  '91 to 365 days'
when days_for_completion > 365 then  '365+ days'
end as completion_bucket
 from 
(
select
ROW_NUMBER() OVER () AS student_track_id,student_id,
 t.track_id,
 t.track_name,
date_enrolled,
if(date_completed is NULL, 0,1) as track_completed,
DATEDIFF(date_completed, date_enrolled) as days_for_completion from sql_and_tableau.career_track_info as t 
left join  sql_and_tableau.career_track_student_enrollments as st
on t.track_id=st.track_id
) as sub
  ```

Here is a preview of the data that is then analyzed in Tableau.
![tableau](https://github.com/alinah1214/Career-Track-Analysis/assets/149886043/b0b9863b-5d3a-438d-9835-a2b97ab36c3d)

## Findings


![3](https://github.com/alinah1214/Career-Track-Analysis/assets/149886043/47ae74a3-1adf-4ea8-bf3b-c4cac5ba972f)

- Less than 3% of people are completing the course each month, as shown by the graph, in comparison to the enrollment rate.
- The enrollment rate is higher in the month of August.
- More people are enrolling in the data analysis course.




![4](https://github.com/alinah1214/Career-Track-Analysis/assets/149886043/0c28f3ce-d173-4504-a312-e51fa846c374)

The graph shows that for most students, it takes 91-365 days to complete the course.










  
