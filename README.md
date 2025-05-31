# IMPROVING PATIENT WAIT TIME IN A CLINIC
Exploring patient appointment data to evaluate wait times, attendance behavior, demographic factors, and the impact of SMS reminders to optimize clinic scheduling and reduce no-shows
## Tools and Concepts Used
SQL(SQLite)
Microsoft Excel
Aggregation
KPI Calculation
Data Exploration

The dataset aims to answer the following questions:
Measure average patient wait time between the scheduling date and actual appointment date across all records.
Identify patterns and trends in wait times across weekdays, demographics (age, gender), and neighborhood locations.
Examine the relationship between wait time and appointment no-shows.
Evaluate the impact of SMS reminders on patient attendance and appointment compliance.
Compare wait times for patients with chronic conditions (e.g., hypertension, diabetes) to those without to identify disparities.
Highlight the clinic locations (neighbourhoods) with the longest wait times and highest no-show rates.
Provide evidence-based recommendations to improve scheduling efficiency and reduce patient wait time based on data insights.
## Dataset Overview
The dataset contains 17 columns and 110,000+ rows. Each row represents an individual appointment record with associated patient and scheduling information.
Key columns:
Patient ID
Appointment ID
Gender
Schedule Day (Date)
Schedule Time (Time)
Appointment Day (Date)
Appointment Time (Time)
Age
Age Group
Neighbourhood
Chronic Conditions (Hypertension, Diabetes, Alcoholism, Handicap)
Scholarship
SMS_received
No-show (Yes/No)
## KPIs computed
Total patient 
Total appointment 
Total patient that showed up
Total  patient that did not show up
Total appointment attended to
Total appointment not ment
Avg wait time.

This project provides evidence-based insights on improving scheduling efficiency, targeting communication (e.g., SMS reminders), and reducing patient no-shows.

### Total Patients

```sql
SELECT COUNT (DISTINCT(PatientId))
AS Total_patients 
FROM "Appointments"
|Total_patients|
|------------- |
|62299         |
```
### Total Appointments
```sql
SELECT COUNT (DISTINCT(AppointmentID)) 
AS Total_appointments
FROM Appointments
```
|Total_appointments|
|----------------- |
|110527            |

### Total showups
```sql
SELECT COUNT ([No-show]) 
AS Total_showups
FROM Appointments
WHERE [No-show] ='Yes'
```
|Total_showups|
|-------------|
|22319        |

### Total Noshows
```sql
SELECT COUNT (*) 
AS Total_noshow
FROM Appointments 
WHERE[No-show] = 'No'
```
|Total_noshow|
|------------|
|88208|

### Average wait time
```sql
SELECT ROUND(AVG (julianday (AppointmentDay)- julianday (ScheduledDay)))
AS Avg_wait_time
FROM Appointments
```
|Avg_wait_time|
|-------|
|88208|

### Wait time by Gender
```sql
SELECT Gender, ROUND(AVG(Julianday(AppointmentDay)- Julianday (ScheduledDay))) AS wait_time_by_gender
FROM Appointments
group by Gender
```
|Gender|wait_time_by_gender|
|-----|-----|
|F|11|
|M|10|

### Wait Time by Day of Week
```sql
SELECT
CASE STRFTIME('%w', AppointmentDay)
WHEN '1' THEN 'Monday'
WHEN '2' THEN 'Tuesday'
WHEN '3' THEN 'Wednesday'
WHEN '4' THEN 'Thursday'
WHEN '5' THEN 'Friday'
WHEN '6' THEN 'Saturday'
WHEN '0' THEN 'Sunday'
END AS day_of_week, 
ROUND(AVG(JULIANDAY(AppointmentDay) - JULIANDAY(ScheduledDay)))
AS avg_wait_time 
FROM appointments
GROUP BY day_of_week
```
|day_of_week|avg_wait-time|
|----|----|
|Friday|10|
|Monday|11|
|Saturday|4|
|Thursday|10|
|Tuesday|10|
|Wednesday|10|

### Wait Time by neighbourhood
```sql
SELECT Neighbourhood, ROUND(AVG(Julianday(AppointmentDay)-Julianday(ScheduledDay))) AS wait_time
FROM Appointments
GROUP BY Neighbourhood
```
|Neighbourhood|wait_time|
|---|---|
|AEROPORTO	|15|
|ANDORINHAS	|9|
|ANTÔNIO HONÓRIO	|14|
|ARIOVALDO FAVALESSA|	7|
|BARRO VERMELHO|7|
|BELA VISTA	|7|
|BENTO FERREIRA	|10|
|BOA VISTA|	6|
|BONFIM	|8|

view full table https://docs.google.com/spreadsheets/d/1zgbTjNDPCZ6vhDFnfhwLT1eTU5P1D-aVdfT6-IXufYI/edit?usp=sharing
