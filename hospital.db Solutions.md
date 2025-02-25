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




























