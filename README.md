# IMPROVING PATIENT WAIT TIME IN A CLINIC
Exploring patient appointment data to evaluate wait times, attendance behavior, demographic factors, and the impact of SMS reminders to optimize clinic scheduling and reduce no-shows
# Tools and Concepts Used
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
# Dataset Overview
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
# KPIs computed
Total patient 
Total appointment 
Total patient that showed up
Total  patient that did not show up
Total appointment attended to
Total appointment not ment
Avg wait time.

This project provides evidence-based insights on improving scheduling efficiency, targeting communication (e.g., SMS reminders), and reducing patient no-shows.

### Total Patients
`````sql
SELECT COUNT (DISTINCT(PatientId))
AS Total_patients 
FROM "Appointments"
|Total_patients|
|-------------|
|62299|
