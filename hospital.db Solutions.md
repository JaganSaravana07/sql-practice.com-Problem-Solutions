# hospital.db Problems Solutions

### You can use the Entity Relationship Diagram (ERD) to figure out what data to store, the entities, their attributes, and how entities relate to other entities.
![hospital_ERD](https://github.com/user-attachments/assets/e2867c20-6adf-4bf2-8a6b-782a531e0857)

## Solutions
### Level - EASY
#### Questions 1 - 17
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



