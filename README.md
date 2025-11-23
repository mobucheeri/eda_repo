# Project 2: Exploratory Data Analysis (EDA)
## Burnout Risk Assessment of Mid-Career Employees at GlobalWorks

**Consultant:** Mohamed Bucheeri  
**Client:** GlobalWorks  
**Role:** People Data Analytics Consultant (External)  
**Industry:** Legal Operations, Compliance Services, and Audit Risk Management

## Problem Statement
GlobalWorks has seen a decline in engagement, satisfaction, and work-life balance scores among employees with 2–5 years of tenure, a 1,207-person cohort representing 40.2% of the workforce. Leadership wants to understand whether these declines signal early-stage burnout and which groups are most affected.

### Executive Summary
This project explores early indicators of burnout among GlobalWorks’ mid-career employees with 2–5 years of tenure, a 1,207-person cohort representing more than 40% of the workforce. Using HR records, engagement surveys, training data, and recruitment information, the analysis builds a clear picture of wellbeing pressures that may be contributing to declining engagement and operational strain across key legal, audit, and compliance functions.

The exploratory work focused on creating clean, consistent datasets, generating descriptive statistics, and examining relationships between sentiment, tenure, and training participation. Visualisations were used to identify departments with lower sentiment and to highlight employees showing multiple early-risk markers. These findings provide leadership with an evidence-based view of where burnout vulnerability is emerging and where targeted wellbeing or development interventions may help strengthen retention and performance.

## Project Aim
The aim of this project is to analyse HR records, engagement surveys, and training data to identify early indicators of burnout among mid-career employees and highlight where risks are most concentrated. The analysis will support leadership in prioritising targeted interventions to improve wellbeing and retention.

## Motivation
Burnout is a growing concern in professional services, where sustained workloads and regulatory expectations place ongoing pressure on employees. Mid-career staff are particularly at risk as they balance increasing responsibility with limited progression opportunities, making declines in engagement or satisfaction especially costly for performance and retention.

Understanding these pressures through data allows organisations to identify early warning signs before they affect wider business outcomes. This project provides GlobalWorks with an evidence-based view of where burnout risk may be emerging and how targeted interventions can support wellbeing and continuity across critical teams.

## Audience
This analysis is intended for GlobalWorks’ senior leadership team, which has responsibility for workforce strategy, employee wellbeing, and retention. The findings are also relevant to HR business partners, learning and development teams, and operational managers who work closely with mid career employees across legal, audit, and compliance functions. The results are presented in a clear and accessible format so that non technical decision makers can use the insights to inform practical and targeted interventions.

## Data Sources
This project uses four internal datasets provided by GlobalWorks. These datasets contain HR records, employee sentiment data, professional development activity, and applicant background information. Together they support a structured review of sentiment trends, tenure characteristics, and training patterns among mid-career employees.

- **`employee_data.csv`**  
  Contains HR information including employee identifiers, job titles, business units, department categories, employment status, and start and exit dates. It is used to calculate tenure and to segment employees by organisational structure.

- **`employee_engagement_survey_data.csv`**  
  Includes engagement, satisfaction, and work-life balance scores linked to employee IDs. It is used to assess sentiment levels and to identify potential early indicators of burnout.

- **`training_and_development_data.csv`**  
  Provides details on training activity, including programme names, training types, duration, outcomes, and costs. It is used to examine development patterns and the relationship between training exposure and sentiment indicators.

- **`recruitment_data.csv`**  
  Contains applicant information such as education, experience, desired salary, and application status. It is included for general context but is not a central part of the burnout analysis.

## Methodology
The analysis followed a structured workflow that began with consolidating the four internal datasets provided by GlobalWorks. Once the data was imported, initial checks were carried out to confirm that identifiers were consistent, date fields were correctly formatted, and categorical variables were labelled in a uniform way. After this review, the datasets were cleaned, aligned by employee ID, and merged into a single analytical table that allowed sentiment, tenure, and training variables to be examined together.

Descriptive statistics were produced to establish an initial understanding of engagement, satisfaction, work life balance, tenure distribution, and training participation. Visualisations were then created to explore relationships between these variables and to highlight departments and business units where sentiment scores were lower. Additional engineered variables were introduced, such as tenure groups and burnout flags, to support the identification of employees who displayed more than one early warning indicator.

## Workflow Summary
1. Imported all datasets and reviewed their structure.  
2. Standardised column names, ID fields, date formats, and category labels.  
3. Cleaned missing values and resolved inconsistencies across datasets.  
4. Merged HR, engagement, and training data into a unified analytical table.  
5. Produced descriptive statistics for sentiment, training, and tenure measures.  
6. Created engineered variables to support deeper analysis.  
7. Generated visualisations to highlight departments with lower sentiment.  
8. Flagged employees showing multiple early burnout indicators.  
9. Prepared results for interpretation and reporting.

## EDA Objectives
1. Measure baseline engagement, satisfaction, and work-life balance using descriptive statistics for the 2–5-year tenure cohort.
2. Assess data quality by checking identifier alignment, missing values, and typing consistency across HR, survey, and training datasets.
3. Compare sentiment scores across departments and job functions to identify low-sentiment groups.
4. Analyse how sentiment varies across the 2–5-year tenure range.
5. Evaluate training participation and outcomes, and test their association with sentiment indicators.
6. Flag employees who meet multiple early-risk conditions such as low sentiment, reduced work-life balance, limited training, or long time in role.
7. Compare business units to identify whether structural workload patterns align with higher burnout-risk indicators.

## File Directory
project-2-burnout-eda/
│
├── README.md
│
├── data/
│   ├── employee_data.csv
│   ├── employee_engagement_survey_data.csv
│   ├── training_and_development_data.csv
│   └── recruitment_data.csv
│
├── notebooks/
│   └── 01_eda_burnout.ipynb
│
├── presentation/
│   └── burnout_analysis_presentation.pdf
│
└── images/
    └── visualisations/

## Data Dictionary
The following tables describe the raw variables used in the burnout risk analysis.  
Data types reflect values extracted directly from the source CSV files before cleaning.  
Additional engineered variables, such as tenureyears and burnout flags, will be created during EDA.

### 1. employee_data.csv
| Column Name                 | Data Type | Description |
|-----------------------------|-----------|-------------|
| EmpID                       | int64     | Unique employee ID |
| FirstName                   | object    | Employee first name |
| LastName                    | object    | Employee last name |
| StartDate                   | object    | Employment start date (string before parsing) |
| ExitDate                    | object    | Employment end date (string before parsing; may be empty or null) |
| Title                       | object    | Job title |
| Supervisor                  | object    | Direct manager or supervisor |
| ADEmail                     | object    | Company email address |
| BusinessUnit                | object    | Assigned business unit |
| EmployeeStatus              | object    | Employment status (active, terminated, on leave) |
| EmployeeType                | object    | Employment type (full time, part time) |
| PayZone                     | object    | Pay band or compensation zone |
| EmployeeClassificationType  | object    | Internal classification category |
| TerminationType             | object    | Type of employment termination |
| TerminationDescription      | object    | Additional notes on termination |
| DepartmentType              | object    | Department or team category |
| Location                    | object    | Work location |
| HireSource                  | object    | Recruitment source |
| Rehire                      | object    | Indicates whether the employee is a rehire |
| EngagementSurveyStatus      | object    | Survey participation status |
| TimeInPosition              | float64   | Time spent in current position (years) |
| PerformanceScore            | object    | Performance review score category |

**Engineered variables to be created during EDA:**  
- StartDate_parsed (datetime64)  
- ExitDate_parsed (datetime64)  
- EffectiveEndDate  
- tenureyears (float)

### 2. employee_engagement_survey_data.csv
| Column Name          | Data Type | Description |
|----------------------|-----------|-------------|
| EmpID                | int64     | Unique employee ID |
| EngagementScore      | int64     | Engagement score reported by employee, from 1 to 5 |
| SatisfactionScore    | int64     | Satisfaction score reported by employee, from 1 to 5 |
| WorkLifeBalanceScore | int64     | Work life balance score reported by employee, from 1 to 5 |
| SurveyYear           | int64     | Year the survey was completed |

### 3. training_and_development_data.csv
| Column Name           | Data Type | Description |
|-----------------------|-----------|-------------|
| EmployeeID            | int64     | Employee ID |
| TrainingProgramName   | object    | Name of training programme |
| TrainingType          | object    | Type or category of training |
| TrainingDurationHours | int64     | Duration of training in hours |
| TrainingOutcome       | object    | Result of the training (Completed, Passed, Failed) |
| TrainingCost          | float64   | Cost of the training programme |

**Engineered variables:**  
- TotalTrainings (count per employee)  
- MostCommonOutcome (mode)

### 4. recruitment_data.csv
| Column Name         | Data Type | Description |
|---------------------|-----------|-------------|
| Candidate ID        | int64     | Unique applicant ID |
| Gender              | object    | Gender of applicant |
| Age                 | int64     | Age of applicant |
| Education Level     | object    | Highest education level |
| Years of Experience | int64     | Total years of work experience |
| Desired Salary      | float64   | Expected salary |
| Job Title           | object    | Role applied for |
| Status              | object    | Application stage (Interviewing, Rejected, etc.) |

### 5. Engineered Variables (Created During EDA)
| Variable Name      | Data Type | Description |
|--------------------|-----------|-------------|
| tenureyears        | float64   | Total tenure in years based on start and end dates |
| burnout_flag       | int64     | Flag equal to 1 if employee meets multiple burnout risk criteria |
| training_intensity | float64   | Number of trainings per year of tenure |
| sentiment_average  | float64   | Average of engagement, satisfaction, and work life balance scores |
| tenure_group       | object    | Tenure category: Early (0 to 1), Mid (2 to 5), Late (6 or more) |

## Conclusions (To Be Completed After EDA)

## Recommendations (To Be Completed After EDA)

## Areas for Further Research (To Be Completed After EDA)

## Limitations
The analysis draws on data from the most recent HR, survey, and training cycles, meaning that findings reflect a specific point in time rather than a long term trend. Sentiment scores are self reported and may not capture the full complexity of employee experience. Training records vary in depth, and some development activity may take place outside formal programmes. Recruitment data is included for context but is not directly linked to burnout outcomes.

The merged dataset provides a strong basis for exploratory work, but it does not include qualitative variables such as workload distribution, team culture, leadership style, or detailed performance metrics. These factors may also influence burnout risk and would require additional investigation in future research stages.

## Sources
The datasets in this project were adapted from the following publicly available resource:

Rana, Ravindra Singh. "Employee Dataset." Kaggle, 2023.  
Available at: https://www.kaggle.com/datasets/ravindrasinghrana/employeedataset/

The data has been modified and expanded to create a synthetic HR dataset for educational purposes within General Assembly’s Data Science curriculum. All names, identifiers, and organisational details (including the fictional company GlobalWorks) are entirely artificial and do not represent real individuals or entities.
