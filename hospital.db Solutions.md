# hospital.db Problems Solutions

You can use the Entity Relationship Diagram (ERD) to figure out what data to store, the entities, their attributes, and how entities relate to other entities.

![hospital_ERD](https://github.com/user-attachments/assets/e2867c20-6adf-4bf2-8a6b-782a531e0857)

## Solutions
### Level - EASY
#### Questions: 1 - 16
1. Show first name, last name, and gender of patients whose gender is 'M'
```SQL
SELECT first_name, last_name, gender from patients
WHERE gender = 'M';
```
2. Show first name and last name of patients who does not have allergies. (null)
```SQL
SELECT first_name, last_name from patients
WHERE allergies IS NULL;
```
3. Show first name of patients that start with the letter 'C'
```SQL
SELECT first_name from patients
WHERE first_name LIKE 'C%';
```
4. Show first name and last name of patients that weight within the range of 100 to 120 (inclusive)
```SQL
SELECT first_name, last_name from patients
WHERE weight between 100 AND 120;
```
5. Update the patients table for the allergies column. If the patient's allergies is null then replace it with 'NKA'
```SQL
update patients
SET allergies='NKA'
where allergies IS null;
```
6. Show first name and last name concatinated into one column to show their full name.
```SQL
SELECT concat(first_name,' ', last_name) AS full_name
FROM patients;
```
7. Show first name, last name, and the full province name of each patient.
Example: 'Ontario' instead of 'ON'
```SQL
SELECT patients.first_name, patients.last_name, province_names.province_name
FROM patients
join province_names ON province_names.province_id= patients.province_id;
```
8. Show how many patients have a birth_date with 2010 as the birth year.
```SQL
SELECT COUNT(patient_id) FROM patients
WHERE YEAR(birth_date) = 2010;
```
9. Show the first_name, last_name, and height of the patient with the greatest height.
```SQL
SELECT first_name,last_name,MAX(height) FROM patients;
```
10. Show all columns for patients who have one of the following patient_ids: 1,45,534,879,1000
```SQL
SELECT * FROM patients
where patient_id IN (1, 45, 534, 879, 1000);
```
11. Show the total number of admissions
```SQL
SELECT COUNT(patient_id) AS total_admissions FROM admissions;
```
12. Show all the columns from admissions where the patient was admitted and discharged on the same day.
```SQL
SELECT * FROM admissions
WHERE admission_date = discharge_date;
```
13. Show the patient id and the total number of admissions for patient_id 579.
```SQL
SELECT patient_id, count(*) AS total_admissions
FROM admissions
WHERE patient_id = 579;
```
14. Based on the cities that our patients live in, show unique cities that are in province_id 'NS'.
```SQL
SELECT distinct(city) AS unique_cities FROM patients
WHERE province_id = 'NS';
```
15. Write a query to find the first_name, last name and birth date of patients who has height greater than 160 and weight greater than 70
```SQL
SELECT first_name,last_name,birth_date FROM patients
where height > 160 AND weight > 70;
```
16. Write a query to find list of patients first_name, last_name, and allergies where allergies are not null and are from the city of 'Hamilton'
```SQl
SELECT first_name, last_name, allergies FROM patients
WHERE city = 'Hamilton' AND allergies is not null;
```

## Level - MEDIUM
### Questions: 1 - 26
1. Show unique birth years from patients and order them by ascending.
```SQL
SELECT DISTINCT(year(birth_date)) AS birth_year FROM patients
order by birth_date asc;
```
2. Show unique first names from the patients table which only occurs once in the list.
For example, if two or more people are named 'John' in the first_name column then don't include their name in the output list. If only 1 person is named 'Leo' then include them in the output.
```SQL
SELECT first_name from patients
group by first_name having count(first_name) = 1;
```
3. Show patient_id and first_name from patients where their first_name start and ends with 's' and is at least 6 characters long.
```SQL
SELECT patient_id, first_name from patients
where first_name LIKE 'S____%s';
```
4. Show patient_id, first_name, last_name from patients whos diagnosis is 'Dementia'.
Primary diagnosis is stored in the admissions table.
```SQL
SELECT patients.patient_id, first_name, last_name 
from patients
JOIN admissions ON admissions.patient_id = patients.patient_id
WHERE diagnosis = 'Dementia';
```
5. Display every patient's first_name. Order the list by the length of each name and then by alphabetically.
```SQL
SELECT first_name FROM patients
order by len(first_name), first_name;
```
6. Show the total amount of male patients and the total amount of female patients in the patients table.
Display the two results in the same row.
```SQL
SELECT 
   (select count(*) from patients WHERE gender = 'M') AS male_count,
   (SELECT count(*) from patients WHERE gender = 'F') AS female_count;
```
7. Show first and last name, allergies from patients which have allergies to either 'Penicillin' or 'Morphine'. Show results ordered ascending by allergies then by first_name then by last_name.
```SQL
SELECT first_name, last_name, allergies from patients
WHERE allergies = 'Penicillin' OR allergies = 'Morphine'
order by allergies, first_name, last_name;
```
8. Show patient_id, diagnosis from admissions. Find patients admitted multiple times for the same diagnosis.
```SQL
SELECT patient_id, diagnosis from admissions
group by patient_id, diagnosis
having count(*) > 1
```
9. Show the city and the total number of patients in the city.
Order from most to least patients and then by city name ascending.
```SQL
SELECT city, COUNT(*) AS num_patients
FROM patients
group by city
order by num_patients DESC, city asc;
```
10. Show first name, last name and role of every person that is either patient or doctor.
The roles are either "Patient" or "Doctor"
```SQL
SELECT first_name, last_name, 'Patient' AS role from patients
union ALL
select first_name, last_name, 'Doctor' FROM doctors
```
11. Show all allergies ordered by popularity. Remove NULL values from query.
```SQL
SELECT allergies, count(*) AS total_diagnosis FROM patients
where allergies IS NOT NULL
group by allergies
order by total_diagnosis DESC;
```
12. Show all patient's first_name, last_name, and birth_date who were born in the 1970s decade. Sort the list starting from the earliest birth_date.
```SQL
SELECT first_name, last_name, birth_date FROM patients
where YEAR(birth_date) between 1970 AND 1979
order by birth_date Asc;
```
13. We want to display each patient's full name in a single column. Their last_name in all upper letters must appear first, then first_name in all lower case letters. Separate the last_name and first_name with a comma. Order the list by the first_name in decending order
EX: SMITH,jane
```SQL
SELECT concat(upper(last_name),',',lower(first_name)) FROM patients
order by first_name DESC;
```
14. Show the province_id(s), sum of height; where the total sum of its patient's height is greater than or equal to 7,000.
```SQL
SELECT province_id, SUM(height) as sum_height FROM patients
group by province_id
having sum_height >= 7000;
```
15. Show the difference between the largest weight and smallest weight for patients with the last name 'Maroni'
```SQL
SELECT (
  max(weight) - min(weight)) as weight_delta FROM patients
where last_name = 'Maroni';
```
16. Show all of the days of the month (1-31) and how many admission_dates occurred on that day. Sort by the day with most admissions to least admissions.
```SQL
SELECT day(admission_date) AS day_number, count(admission_date) AS no_of_admissions
FROM admissions
group by day_number
order by no_of_admissions DESC;
```
17. Show all columns for patient_id 542's most recent admission_date.
```SQL
SELECT * FROM admissions
where patient_id = 542
order by admission_date desc
LIMIT 1;
```
18. Show patient_id, attending_doctor_id, and diagnosis for admissions that match one of the two criteria:
    - patient_id is an odd number and attending_doctor_id is either 1, 5, or 19.
    - attending_doctor_id contains a 2 and the length of patient_id is 3 characters.
```SQL
SELECT patient_id, attending_doctor_id, diagnosis from admissions
where(patient_id % 2 != 0 AND attending_doctor_id IN (1,5,19))
or
(attending_doctor_id LIKE '%2%' and len(patient_id) = 3)
```
19. Show first_name, last_name, and the total number of admissions attended for each doctor.
Every admission has been attended by a doctor.
```SQL
SELECT first_name, last_name,COUNT(patient_id) as admission_total 
FROM admissions a
join doctors d ON d.doctor_id = a.attending_doctor_id
group by attending_doctor_id;
```
20. For each doctor, display their id, full name, and the first and last admission date they attended.
```SQL
SELECT doctor_id, concat(first_name,' ', last_name) as Full_Name,
MIN(admission_date) AS First_admission_date, mAX(admission_date) as Last_admission_date 
FROM admissions a
JOIN doctors d ON a.attending_doctor_id = d.doctor_id
group by doctor_id;
```
21. Display the total amount of patients for each province. Order by descending.
```SQL
SELECT province_name, count(patient_id) AS patient_count
FROM patients p
JOIN province_names pr ON p.province_id = pr.province_id
group by province_name
order by patient_count DESC;
```
22. For every admission, display the patient's full name, their admission diagnosis, and their doctor's full name who diagnosed their problem.
```SQL
SELECT concat(p.first_name,' ', p.last_name) AS patient_name,
diagnosis, CONCAT(d.first_name,' ', d.last_name) FROM patients p
JOIN admissions a ON p.patient_id = a.patient_id
JOIN doctors d ON a.attending_doctor_id = d.doctor_id
```
23. display the first name, last name and number of duplicate patients based on their first name and last name.
Ex: A patient with an identical name can be considered a duplicate.
```SQL
SELECT first_name, last_name, count(*) as no_of_duplicates FROM patients
group by first_name, last_name
having no_of_duplicates > 1;
```
24. Display patient's full name,
height in the units feet rounded to 1 decimal,
weight in the unit pounds rounded to 0 decimals,
birth_date,
gender non abbreviated.

Convert CM to feet by dividing by 30.48.
Convert KG to pounds by multiplying by 2.205.
```SQL
SELECT concat(first_name,' ', last_name) as 'patient_name', 
ROUND(height/30.48,1) AS 'height "feet"', round(weight*2.205,0) AS 'weight "pounds"', 
birth_date, 
CASE
    WHEN gender = 'M' THEN 'MALE'
    else 'FEMALE'
END 'gender_type'
from patients;
```
25. Show patient_id, first_name, last_name from patients whose does not have any records in the admissions table. (Their patient_id does not exist in any admissions.patient_id rows.)
```SQl
SELECT p.patient_id, first_name, last_name 
FROM patients p
LEFT JOIN admissions a ON p.patient_id = a.patient_id
where a.patient_id IS null
```
26. Display a single row with max_visits, min_visits, average_visits where the maximum, minimum and average number of admissions per day is calculated. Average is rounded to 2 decimal places.
```SQL
SELECT MAX(no_of_visits) AS max_visits, 
MIN(no_of_visits) AS min_visits,
ROUND(avg(no_of_visits),2) AS average_visits FROM(
  SELECT admission_date, COUNT(*) AS no_of_visits FROM admissions
group by admission_date
)
```
## Level - HARD
### Questions: 1 - 11
1. Show all of the patients grouped into weight groups.
   Show the total amount of patients in each weight group.
   Order the list by the weight group decending.

   For example, if they weight 100 to 109 they are placed in the 100 weight group, 110-119 = 110 weight group, etc.
```SQL
SELECT COUNT(patient_id) AS patients_in_group, 
FLOOR(weight/10)*10 AS weight_group FROM patients
group by weight_group
order by weight_group DESC;
```
2. Show the provinces that has more patients identified as 'M' than 'F'. Must only show full province_name
```SQl
SELECT pr.province_name AS province 
FROM patients p
JOIN province_names pr ON pr.province_id = p.province_id
group by province
HAVING	
	COUNT(CASE WHEN gender = 'M' THEn 1 END) > COUNT(CASE WHEN gender = 'F' THEN 1 END)
```
3. Show patient_id, weight, height, isObese from the patients table.
   Display isObese as a boolean 0 or 1.	
   Obese is defined as weight(kg)/(height(m)2) >= 30.
	
   weight is in units kg.	
   height is in units cm.
```SQL
SELECT patient_id, weight, height,
	(
      CASE
      WHEN weight/(power(height/100.0,2)) >= 30 THEN 
      1
      ELSE
      0
      END
     ) AS isObese
FROM patients
```
4. All patients who have gone through admissions, can see their medical documents on our site. Those patients are given a temporary password after their first admission. Show the patient_id and temp_password.

   The password must be the following, in order:
   1. patient_id
   2. the numerical length of patient's last_name
   3. year of patient's birth_date
```SQL
SELECT distinct p.patient_id,
concat(p.patient_id,len(last_name),year(birth_date)) AS temp_password
FROM patients p
JOIN admissions a ON a.patient_id = p.patient_id;
```
5. We are looking for a specific patient. Pull all columns for the patient who matches the following criteria:
- First_name contains an 'r' after the first two letters.
- Identifies their gender as 'F'
- Born in February, May, or December
- Their weight would be between 60kg and 80kg
- Their patient_id is an odd number
- They are from the city 'Kingston'
```SQL
SELECT * FROM patients
WHERE first_name LIKE '__r%' AND gender = 'F' AND 
month(birth_date) IN (2, 5, 12) AND
weight between 60 AND 80 AND patient_id % 2 = 1
AND city = 'Kingston';
```
6. Show the percent of patients that have 'M' as their gender. Round the answer to the nearest hundreth number and in percent form.
```SQL
select concat(ROUND(SUM(gender = 'M')/ cast(count(*) AS float), 4) * 100, '%')
AS percent_of_male_patients FROM patients
```

















