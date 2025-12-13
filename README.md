# Project 2: Exploratory Data Analysis (EDA)
## Wellbeing and Retention Patterns at GlobalWorks

**Consultant:** Mohamed Bucheeri  
**Client:** GlobalWorks (fictional)  
**Role:** People Data Analytics Consultant (External)
**Industry:** Legal Operations, Compliance Services, and Audit Risk Management

### Introduction
This project analyses GlobalWorks’ HR, engagement, and training data to understand how employee wellbeing varies across the organisation. The analysis focuses on engagement, satisfaction, and work–life balance, and explores how these patterns differ across divisions and relate to employee exit behaviour.

*GlobalWorks is a fictional organisation, and the dataset used in this project is synthetic and adapted for educational purposes.*

## Problem Statement
GlobalWorks’ most recent HR and engagement data reveal a wide gap in wellbeing, with average engagement ranging from about 2.1 to 4.0 and work–life balance from roughly 2.5 to 3.4 on the 1–5 scale, while exit rates range from around 41% to nearly 100%, and remains high even after excluding retirements. The organisation seeks to link these disparities to employee exits to identify which divisions are at heightened risk of avoidable turnover.

## Project Aim
To assess how employee wellbeing varies across divisions at GlobalWorks and explore how these differences relate to exit behaviour in order to identify divisions facing elevated retention risk.

## EDA Objectives
1. Summarise overall engagement, satisfaction, and work–life balance across the workforce.  
2. Compare division-level wellbeing to identify divisions with notably lower sentiment.  
3. Examine how divisional wellbeing patterns differ between areas with higher and lower exit rates.
4. Distinguish avoidable vs non-avoidable exits and assess how each relates to wellbeing by division.  
5. Identify divisions that show weaker wellbeing and higher (avoidable) exit rates to prioritise retention support.

## Executive Summary
This analysis provides an evidence-based view of wellbeing and retention patterns across GlobalWorks. The data shows that wellbeing levels differ significantly across divisions, and several teams display both lower wellbeing and higher exit rates. These patterns suggest that retention challenges are linked most strongly to **divisional working conditions** rather than organisation-wide issues.

Key findings include:
- Wellbeing scores vary widely across divisions, confirming uneven employee experience.  
- Divisions with lower work–life balance and satisfaction tend to have higher exit rates.  
- Exit rates remain high even after excluding retirements, indicating that most turnover is avoidable.  
- No single wellbeing measure explains exits on its own; retention risk reflects broader divisional conditions.  
- A small set of divisions emerges as clear priorities for targeted support.

## Motivation
Employee wellbeing is a central factor in workforce stability. In regulated and operationally intensive environments, uneven workload pressures can create significant differences in employee experience across teams. Understanding these patterns through data enables organisations to identify where support is most needed, improve retention, and strengthen operational continuity.

## Audience
This analysis is designed for:
- Senior leadership focusing on workforce strategy and retention  
- HR and People Operations teams  
- Learning and Development teams  
- Divisional managers responsible for workload, employee support, and team climate  

All insights are presented in a clear and accessible format for non-technical decision-makers.

## Data Sources
The project uses four synthetic datasets based on a fictional company scenario. These datasets support a structured review of sentiment trends, training activity, and exit behaviour.

- **`employee_data.csv`**: Core HR information such as division, department, job title, dates, and employment status.  
- **`employee_engagement_survey_data.csv`**: Engagement, satisfaction, and work–life balance survey scores.  
- **`training_and_development_data.csv`**: Training duration, outcome, and cost for each employee.  
- **`recruitment_data.csv`**: Applicant data included for context only.

## Methodology
The project follows a structured and reproducible EDA workflow:

1. **Import and inspect datasets** to assess structure, missingness, and identifier consistency.  
2. **Clean and standardise fields**, including column names, date formats, and categorical labels.  
3. **Merge datasets** into a single employee-level analytical table.  
4. **Engineer key variables**, such as exit flags, sentiment averages, and training exposure metrics.  
5. **Conduct EDA** using visual and descriptive techniques to explore wellbeing distributions, divisional differences, and exit patterns.  
6. **Analyse exit behaviour**, distinguishing avoidable and non-avoidable exits and examining age at exit.  
7. **Link divisional wellbeing to exit rates** using regression plots and multivariate visualisations.  
8. **Identify priority divisions** requiring targeted retention support.

## Workflow Summary
1. Loaded and inspected datasets.  
2. Standardised column names and identifiers.  
3. Cleaned missing data and parsed date fields.  
4. Merged HR, engagement, and training data.  
5. Created engineered features such as exit flags, sentiment averages, and avoidable exit indicators.  
6. Analysed wellbeing patterns across divisions.  
7. Examined exit reasons, age at exit, and avoidable vs non-avoidable exits.  
8. Linked divisional wellbeing patterns to exit rates.  
9. Identified divisions requiring targeted support.

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

### 5. employee_full
The `employee_full` dataset is the final employee-level table created during EDA.  
It is produced by merging `employee_data.csv`, `employee_engagement_survey_data.csv`, and `training_and_development_data.csv`, followed by feature engineering.  
All analysis and visualisations in this project are based on this dataset.

### Variables in employee_full

| Variable Name              | Data Type | Description |
|---------------------------|-----------|-------------|
| empid                     | int64     | Unique employee identifier |
| Division                  | object    | Employee division |
| DepartmentType            | object    | Department or team category |
| StartDate                 | datetime  | Employment start date |
| ExitDate                  | datetime  | Employment end date (null if active) |
| effective_end_date        | datetime  | ExitDate for leavers; analysis date for active employees |
| tenureyears               | float64   | Length of employment in years |
| Engagement Score          | int64     | Engagement survey score (1–5) |
| Satisfaction Score        | int64     | Satisfaction survey score (1–5) |
| Work-Life Balance Score   | int64     | Work–life balance survey score (1–5) |
| sentiment_average         | float64   | Mean of the three wellbeing scores |
| Exit Flag                 | int64     | 1 if employee has exited; 0 if active |
| Avoidable Exit            | int64     | 1 if exit is avoidable; 0 if non-avoidable |
| total_trainings           | int64     | Total number of recorded training events |
| training_intensity        | float64   | Trainings per year of tenure |

### 6. Engineered Variables (Created During EDA)
| Variable Name         | Data Type | Description |
|-----------------------|-----------|-------------|
| effective_end_date    | datetime  | ExitDate for leavers; today’s date for active employees. |
| exit_flag             | int64     | Indicator equal to 1 if the employee has exited the organisation; 0 if active. |
| sentiment_average     | float64   | Mean of engagement, satisfaction, and work–life balance scores. |
| training_completed    | int64     | Indicator equal to 1 if training outcome is Completed or Passed; 0 otherwise. |
| training_duration     | float64   | Duration of the employee’s recorded training programme (days). |
| training_cost         | float64   | Cost of the employee’s recorded training programme. |

## Conclusion
This analysis shows clear differences in wellbeing across divisions at GlobalWorks and demonstrates that these patterns align with variation in exit rates. Divisions with lower work–life balance and satisfaction tend to experience higher and largely avoidable turnover, indicating that retention challenges are driven mainly by divisional working conditions rather than organisation-wide issues. A small set of divisions emerges as clear priorities for intervention, while others show more stable wellbeing and retention profiles. Overall, the findings provide a clear, data-driven basis for targeted retention action.

## Recommendations
Based on the findings, GlobalWorks should consider the following actions:

### 1. Prioritise Support for High-Risk Divisions
Safety, Project Management – Engineering, and Finance and Accounting show the strongest combination of weaker wellbeing and higher avoidable exit rates. These divisions would benefit from:
- Reviewing workload distribution and staffing levels  
- Assessing team culture and management practices  
- Introducing focused wellbeing initiatives such as regular check-ins or workload planning reviews  

### 2. Strengthen Work–Life Balance Policies
Work–life balance shows the clearest relationship with exit behaviour. GlobalWorks should:
- Promote flexible scheduling where operationally possible  
- Review expectations around response times and out-of-hours availability  
- Encourage managers to monitor early signs of overload  

### 3. Monitor Moderate-Risk Divisions
Divisions such as Technology / IT, Field Operations, People Services, Aerial, and Engineers show mixed sentiment patterns. These teams should be monitored regularly to prevent further decline. Short, periodic sentiment reviews may help detect emerging issues.

### 4. Maintain Best Practices in Stable Divisions
General – SGA, General – ENG, Sales and Marketing, Splicing, and Wireless show stronger wellbeing and lower exit rates. GlobalWorks should:
- Document effective workload and management practices in these areas  
- Share successful approaches across other divisions  

### 5. Continue Using Data to Guide Retention Strategy
The analysis shows that wellbeing and retention challenges are uneven across divisions. Ongoing data reviews, combined with managerial feedback, will help ensure that interventions remain targeted and effective.

## Areas for Further Research
Several issues could not be fully explored with the available data and would benefit from additional investigation:

1. **Workload and scheduling data**  
   Information on working hours, overtime, or project load would help confirm whether workload is the main driver of lower work–life balance.

2. **Team-level variation**  
   Current analysis is division-level. Exploring differences at team or manager level may reveal more specific drivers of wellbeing and turnover.

3. **Longitudinal analysis**  
   Wellbeing and exit data over multiple years would help distinguish short-term issues from persistent structural problems.

4. **Qualitative insights**  
   Interviews or focus groups could help explain why certain divisions perform worse and what employees believe would improve conditions.

## Limitations and Improvements
This analysis provides a clear overview of wellbeing and retention patterns at GlobalWorks, but several limitations restrict the depth of the findings.

### Limitations
1. **Single time-point data**  
   The datasets represent one snapshot in time, limiting the ability to assess trends or causality.

2. **Self-reported wellbeing measures**  
   Engagement, satisfaction, and work–life balance scores are subjective and may not fully reflect actual workload or team dynamics.

3. **Incomplete training coverage**  
   Some learning and development activity may occur outside recorded programmes, limiting conclusions about training effects.

4. **Lack of qualitative context**  
   Variables such as leadership style, workload intensity, and team culture are not directly observed.

5. **Division-level aggregation**  
   Using averages may mask variation within divisions across teams or managers.

### Improvements for Future Work
1. **Collect multi-year data**  
   This would allow trend analysis and earlier detection of emerging risks.

2. **Include workload indicators**  
   Metrics such as hours worked or project demand would strengthen conclusions around work–life balance.

3. **Expand development data**  
   Including mentoring, coaching, and informal learning would improve understanding of development and retention.

4. **Add team or manager identifiers**  
   This would enable more targeted and actionable insights.

5. **Incorporate qualitative feedback**  
   Employee narratives could provide valuable context for interpreting quantitative results.

Together, these improvements would support a deeper understanding of wellbeing and retention and help GlobalWorks design more effective, division-specific interventions.

## Sources
The datasets in this project were adapted from the following publicly available resource:

Rana, Ravindra Singh. "Employee Dataset." Kaggle, 2023.  
Available at: https://www.kaggle.com/datasets/ravindrasinghrana/employeedataset/

The data has been modified and expanded to create a synthetic HR dataset for educational purposes within General Assembly’s Data Science curriculum. All names, identifiers, and organisational details (including the fictional company GlobalWorks) are artificial and do not represent real individuals or entities.
