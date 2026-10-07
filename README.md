# SWYNEX-Healthcare-Data-Analytics-Project
End-to-end healthcare data analytics project: data cleaning, EDA, Power BI dashboard and case study on 54,966 hospital admissions
# Healthcare Data Analytics Project | Cleaning, EDA and Power BI Dashboard

An end-to-end data analytics project on 54,966 hospital admissions (2019 to 2024). It covers data cleaning and preparation, exploratory data analysis, an interactive Power BI dashboard, and a final case study with recommendations for hospital management.

Built as part of the **SWYNEX Technologies** data analytics program (Task 1: Data Cleaning, Task 2: EDA, Task 3: Interactive Dashboard, Task 4: Final Case Study).

---

## Project Documents

| Item | Link |
|---|---|
| Final case study (PDF) | [docs/Final_Data_Analytics_Case_Study.pdf](docs/Final_Data_Analytics_Case_Study.pdf) |
| Power BI dashboard file | [powerbi/SWYNEX_Hospital_Advisory_Dashboard.pbix](powerbi/SWYNEX_Hospital_Advisory_Dashboard.pbix)

---

## Business Problem

Hospital management needs to plan staff, beds, emergency capacity and revenue months in advance. This project analyses 54,966 patient records to find:

- In which months patient volume and emergency load are highest
- Which age groups and conditions drive admissions
- When billing per patient and total revenue peak
- What concrete actions a hospital can take each month

---

## Project Workflow

| Stage | What was done | Output |
|---|---|---|
| Task 1: Data Cleaning and Preparation | Quality checks, flagged problem rows, new analysis columns | Prepared dataset |
| Task 2: Exploratory Data Analysis | Patterns in volume, patient groups, emergencies, billing and trends | Key insights |
| Task 3: Interactive Dashboard | 6 Power BI pages, DAX measures, 5 synced slicers | .pbix dashboard |
| Task 4: Final Case Study | Combined everything into recommendations for hospital management | Case study (PDF) |

---

## Dataset

| Item | Detail |
|---|---|
| Records | 54,966 patient admissions |
| Period | 2019 to 2024 (2024 is a partial year) |
| Columns | 15 (Name, Age, Gender, Blood Type, Medical Condition, Date of Admission, Doctor, Hospital, Insurance Provider, Billing Amount, Room Number, Admission Type, Discharge Date, Medication, Test Results) |
| Conditions | Arthritis, Asthma, Cancer, Diabetes, Hypertension, Obesity |
| Source | [add dataset source link] |

**Note:** The class balance (every condition about 9,100 patients, test results about one-third each, nearly flat billing) suggests this is a synthetic practice dataset. Findings show analysis technique and should not be read as real-world clinical conclusions.

---

## Tools Used

- **Microsoft Excel**: source data
- **Power Query**: cleaning checks and new columns
- **DAX**: calculated measures
- **Power BI Desktop**: dashboard, slicers, sync slicers

---

## Task 1: Data Cleaning and Preparation

**Checks performed**

- No missing values across all 15 columns
- No exact duplicate rows
- Discharge date is never before admission date
- No negative or zero-day stays
- No billing outliers (IQR method)
- Categorical columns (Gender, Blood Type, Admission Type, Medication, Test Results) are consistent

**Data quality flag**

- About 9,955 rows share the same Name and Date of Admission but have different Ages. These were **flagged, not removed**, so age-based figures should be read with that in mind.

**Columns added in Power Query**

| Column | Purpose |
|---|---|
| Length of Stay | Days between admission and discharge |
| Age Group | Under 18, 18 to 35, 35 to 50, 50 to 65, Over 65 |
| Age Sort | Keeps age groups in the correct order |
| Admission Year / Admission Month | Trend analysis |
| Month Num | Sorts months January to December |

---

## Task 2: Exploratory Data Analysis (Key Insights)

| Area | Finding |
|---|---|
| Volume | August is the busiest month (4,785 patients) |
| Emergency load | July has the most emergencies (1,573) |
| Emergency rate | February has the fewest patients but the highest emergency rate (34.5%), so the emergency ward cannot be scaled down |
| Overall emergency share | 32.9% of admissions (18,102 patients) |
| Age | Over 65 is the largest group: 16,923 patients (30.8%) |
| Condition | Arthritis has the most patients (9,218) and the highest abnormal-test rate (34.2%) |
| Emergency by condition | Obesity has the highest emergency rate (33.9%) |
| Billing per patient | October is highest ($26,020), then June ($25,913); September is lowest ($25,256) |
| Total revenue | About $1.4B in total; August is highest ($121.6M), February lowest ($106.7M) |
| Insurance | Medicare has the highest average bill ($25,630); Cigna has the highest total revenue ($284M) |
| Trend | Admissions rose from 7,300 (2019) to 11,172 (2020), a 53% jump, then stayed near 10,900 a year through 2023 |

---

## Task 3: Interactive Dashboard

| Page | Question it answers | Main visuals |
|---|---|---|
| **Overview** | What is the big picture? | KPI cards, monthly volume, yearly admissions, admission type split, condition and age distribution |
| **When** | When are patients and revenue highest? | Monthly admissions, monthly emergencies, average billing by month, average length of stay by month |
| **Who** | Who is being admitted? | Age group by month, condition by age group, Over 65 and 18 to 35 monthly trends |
| **Emergency** | When and for whom is emergency demand highest? | Emergency count by month, emergency rate by month, condition and age group |
| **Revenue** | When and from whom does revenue come? | Total revenue by month, average billing by month, revenue by condition and insurer |
| **Hospital Advisory** | What should management do and when? | Recommendation cards, month-by-month preparation calendar, key business trends |

**Interactivity:** five slicers (Medical Condition, Gender, Admission Type, Admission Year, Insurance Provider) are synced across pages, so one selection filters the whole report.

---

## Task 4: Recommendations (Final Case Study)

| Period | Action |
|---|---|
| January | Keep the emergency ward fully staffed (1,547 emergencies, winter spike) |
| February | Use low volume for training and maintenance, but do not reduce emergency cover |
| March to May | Routine operations, preventive health camps |
| June | Revenue focus: promote elective procedures and health packages |
| July to August | Peak season: maximum staffing, beds and emergency readiness |
| September | Lowest billing per patient: focus on claims processing and collections |
| October | Highest billing per patient: launch premium services |
| November to December | Budget planning and annual health packages |

**Standing priorities:** a senior-care unit (Over 65 is 30.8% of admissions), obesity emergency readiness (highest emergency rate), and insurance partnerships (Medicare for average bill, Cigna for total revenue).

---

## DAX Measures

Replace `HealthcareData` with your table name.

```DAX
Emergency Rate % =
DIVIDE(
    COUNTROWS(FILTER('HealthcareData', 'HealthcareData'[Admission Type] = "Emergency")),
    COUNTROWS('HealthcareData'),
    0
) * 100

Abnormal Rate % =
DIVIDE(
    COUNTROWS(FILTER('HealthcareData', 'HealthcareData'[Test Results] = "Abnormal")),
    COUNTROWS('HealthcareData'),
    0
) * 100

Total Revenue = SUM('HealthcareData'[Billing Amount])

Revenue $M = DIVIDE(SUM('HealthcareData'[Billing Amount]), 1000000)
```

---

## How to Open the Dashboard

1. Download **SWYNEX_Hospital_Advisory_Dashboard.pbix** from the `powerbi/` folder.
2. Open it in **Power BI Desktop** (free, Windows).
3. Use the slicers on any page to filter the whole report.

---

## Repository Structure

```
SWYNEX-Healthcare-Data-Analytics-Project/
├── README.md
├── data/
│   └── Healthcare_dataset_cleaned.xlsx
├── powerbi/
│   └── SWYNEX_Hospital_Advisory_Dashboard.pbix
└── docs/
    └── Final_Data_Analytics_Case_Study.pdf
```

---

## Limitations

- Likely synthetic data, so patterns are cleaner than real hospital data.
- 2024 contains only part of the year (3,827 records), so yearly comparisons exclude it.
- Month-to-month differences are modest (roughly 5 to 10% between best and worst months); treat them as planning signals, not dramatic swings.
- Figures describe this dataset only and show association, not cause.

---

## Author

**Pradeep Kumar Yadav**, Aspiring Data Analyst
Email: yadavpradeepkumar007@gmail.com
LinkedIn: https://www.linkedin.com/in/pradeep-yadav-89493a191/?isSelfProfile=true
