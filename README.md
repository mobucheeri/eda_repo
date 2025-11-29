# Project 2: Exploratory Data Analysis (EDA)
## Wellbeing and Retention Patterns at GlobalWorks

**Consultant:** Mohamed Bucheeri  
**Client:** GlobalWorks (fictional)  
**Role:** People Data Analytics Consultant (External)  
**Industry:** Legal Operations, Compliance Services, and Audit Risk Management

## Introduction
This project examines GlobalWorks’ HR, engagement, and training data to understand how employee wellbeing varies across the organisation. The analysis focuses on engagement, satisfaction, and work–life balance, and explores how these patterns differ across divisions and relate to employee exit behaviour.

*GlobalWorks is a fictional organisation, and the dataset used in this project is synthetic and adapted for educational purposes.*

## Problem Statement
GlobalWorks has observed large differences in employee wellbeing across divisions, with engagement and work–life balance scores ranging from very low to strong. These uneven patterns have raised concerns about reduced wellbeing in certain divisions and potential links to workforce stability.

## Project Aim
To analyse wellbeing patterns across the organisation, with a focus on how engagement, satisfaction, and work–life balance vary across divisions and how these sentiment indicators relate to employee exit behaviour.

## EDA Objectives
1. Summarise overall engagement, satisfaction, and work–life balance across the workforce.  
2. Compare wellbeing across divisions to identify areas with notably higher or lower sentiment.  
3. Analyse training duration, cost, and completion patterns across employees.  
4. Examine whether engagement, satisfaction, and work–life balance differ between active and exited employees.  
5. Build a small predictive model to test whether sentiment indicators are associated with exit behaviour.  
6. Highlight divisions or workforce segments that may require targeted wellbeing or retention support.

## Executive Summary
This analysis provides an evidence-based view of wellbeing and retention patterns across GlobalWorks. The data shows that wellbeing levels differ significantly across divisions, and several teams display both lower wellbeing and higher exit rates. These patterns suggest that retention challenges are linked most strongly to divisional environments rather than organisation-wide issues.

Key findings include:
- Wellbeing scores vary widely across divisions, confirming uneven employee experience.  
- Divisions with lower work–life balance and satisfaction tend to have higher exit rates.  
- Training patterns do not show major differences between active and exited employees.  
- A simple predictive model indicates that work–life balance and satisfaction are the strongest sentiment-based predictors of employee exit behaviour.  
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
5. **Conduct EDA** using visual and descriptive techniques to understand sentiment distribution, divisional differences, and exit patterns.  
6. **Model exit behaviour** using a simple logistic regression, focusing on sentiment variables.  
7. **Identify priority divisions** requiring targeted support based on combined evidence.  
8. **Develop conclusions and recommendations** for organisational decision-making.

## Workflow Summary
1. Loaded and inspected datasets.  
2. Standardised column names and identifiers.  
3. Cleaned missing data and parsed date fields.  
4. Merged HR, engagement, and training data.  
5. Created engineered features such as exit flags and sentiment averages.  
6. Analysed wellbeing patterns across the organisation.  
7. Examined training outcomes and their relationship to exit status.  
8. Modelled sentiment’s predictive power for exit behaviour.  
9. Identified divisions requiring targeted support.

## EDA Objectives
1. Summarise overall engagement, satisfaction, and work–life balance across the workforce.  
2. Compare wellbeing across divisions to identify areas with notably higher or lower sentiment.  
3. Analyse training duration, cost, and completion patterns across employees.  
4. Examine whether engagement, satisfaction, and work–life balance differ between active and exited employees.  
5. Build a small predictive model to test whether sentiment indicators are associated with exit behaviour.  
6. Highlight divisions or workforce segments that may require targeted wellbeing or retention support.


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

### 5. Engineered Variables (Created During EDA)
| Variable Name         | Data Type | Description |
|-----------------------|-----------|-------------|
| effective_end_date    | datetime  | ExitDate for leavers; today’s date for active employees. |
| exit_flag             | int64     | Indicator equal to 1 if the employee has exited the organisation; 0 if active. |
| sentiment_average     | float64   | Mean of engagement, satisfaction, and work–life balance scores. |
| training_completed    | int64     | Indicator equal to 1 if training outcome is Completed or Passed; 0 otherwise. |
| training_duration     | float64   | Duration of the employee’s recorded training programme (days). |
| training_cost         | float64   | Cost of the employee’s recorded training programme. |

## Conclusion
The analysis shows clear differences in wellbeing across divisions at GlobalWorks and demonstrates that these patterns align with variation in exit rates. Divisions with lower work–life balance and satisfaction tend to experience higher turnover, suggesting that retention challenges arise from local working conditions rather than organisation-wide issues. A small set of divisions appears to need immediate attention, while others show more stable and positive wellbeing profiles. These results provide a structured, data-driven foundation for prioritising targeted support and improving workforce stability.

## Recommendations
Based on the findings, GlobalWorks should consider the following actions:

### 1. Prioritise Support for High-Risk Divisions
Safety, Project Management – Engineering, and Finance and Accounting show the strongest combination of low wellbeing and higher exit rates. These divisions would benefit from:
- Reviewing workload distribution and staffing levels  
- Assessing team culture and management practices  
- Introducing focused wellbeing initiatives, such as regular check-ins or workload planning reviews  

### 2. Strengthen Work–Life Balance Policies
Work–life balance showed the clearest relationship with exit behaviour. GlobalWorks should:
- Promote flexible scheduling where operationally possible  
- Review expectations around response times and off-hours availability  
- Encourage managers to monitor early signs of overload  

### 3. Monitor Moderate-Risk Divisions
Divisions such as Technology/IT, Field Operations, People Services, Aerial, and Engineers show mixed sentiment patterns. These teams should be monitored regularly to prevent further decline. Short quarterly sentiment checks may help detect emerging issues.

### 4. Maintain Best Practices in High-Stability Divisions
General – SGA, General – ENG, Sales and Marketing, Splicing, and Wireless show stronger wellbeing and lower turnover. GlobalWorks should:
- Record what works well in these divisions  
- Share good management and workload practices across the organisation  

### 5. Continue Using Data to Guide Wellbeing Strategy
The analysis demonstrates that wellbeing and retention challenges are uneven across divisions. Regular data reviews, combined with feedback from team leaders, will help ensure interventions remain targeted and effective.

## Areas for Further Research
Several issues could not be fully explored with the available data and would benefit from additional investigation:

1. **Workload and scheduling data**  
   Actual working hours or project load would help confirm whether workload is the main driver of lower wellbeing in certain divisions.

2. **Team-level variation**  
   The current data aggregates wellbeing at the division level. Exploring differences at team or manager level may reveal more specific drivers of morale and turnover.

3. **Longitudinal analysis**  
   Wellbeing and exit data over multiple years would help identify whether declines are recent or long-standing.

4. **Qualitative insights**  
   Focus groups or structured interviews could provide context for the quantitative patterns observed, especially in high-risk areas.

## Limitations and Improvements
This analysis provides a strong overview of wellbeing and retention patterns at GlobalWorks, but several limitations restrict the depth of the findings. These limitations also point to clear opportunities for improving future analyses.

### Limitations
1. **Single time-point data**  
   The HR, engagement, and training datasets represent one moment in time. Without historical records, it is not possible to determine whether declines in wellbeing or increases in turnover are recent or long-running.

2. **Self-reported sentiment measures**  
   Engagement, satisfaction, and work–life balance scores are subjective and may not fully capture day-to-day experience, workload strain, or team culture.

3. **Incomplete training information**  
   Training records vary in depth. Some development activities may occur outside formal programmes, which limits the ability to link training participation to wellbeing or exit behaviour.

4. **Lack of qualitative context**  
   The dataset does not include variables such as team culture, leadership style, communication quality, or workload distribution, all of which likely influence wellbeing and retention.

5. **Division-level aggregation**  
   Analyses rely on division-level averages, which can mask variation within teams or under specific managers.

### Improvements for Future Work
1. **Collect multi-year data**  
   Tracking wellbeing and exits over several years would allow for trend analysis and clearer identification of developing risks.

2. **Include workload and scheduling metrics**  
   Variables such as hours worked, overtime use, or project load would help determine whether workload is a major driver of low work–life balance.

3. **Capture richer training information**  
   Expanding training data to include coaching, mentoring, informal learning, and internal development activities would support a deeper analysis of learning and retention.

4. **Add team-level or manager-level identifiers**  
   This would enable more granular insights and help identify high-performing or struggling teams beyond divisional averages.

5. **Use qualitative inputs**  
   Focus groups, interviews, or open-text survey responses could help explain why specific divisions score lower and what employees feel would improve their working conditions.

Together, these improvements would support a more complete understanding of the factors shaping wellbeing and retention and help GlobalWorks design more targeted and effective interventions.

## Sources
The datasets in this project were adapted from the following publicly available resource:

Rana, Ravindra Singh. "Employee Dataset." Kaggle, 2023.  
Available at: https://www.kaggle.com/datasets/ravindrasinghrana/employeedataset/

The data has been modified and expanded to create a synthetic HR dataset for educational purposes within General Assembly’s Data Science curriculum. All names, identifiers, and organisational details (including the fictional company GlobalWorks) are artificial and do not represent real individuals or entities.
