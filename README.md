# EV Charging Analysis

## 1. Overview

This project analyzes the usage patterns of shared electric vehicle (EV) charging stations in residential buildings.

The analysis uses SQL queries executed against a PostgreSQL database to identify demand patterns, user distribution across garages, peak charging periods, and users with unusually long average charging sessions.

The project was developed as part of a practical data analytics study focused on SQL and relational data analysis.

## 2. Business Context

As electric vehicle adoption increases, residential buildings face growing demand for accessible charging infrastructure.

Shared charging stations allow multiple residents to access the same infrastructure, which can create competition for charging availability.

Understanding how these stations are used can help building administrators identify areas of higher demand and periods when charging infrastructure is more heavily utilized.

## 3. Objectives

The analysis focuses on three main questions:

1. Which garages have the highest number of unique users accessing shared charging stations?
2. Which days and hours have the highest number of shared charging sessions?
3. Which shared-station users have an average charging duration greater than 10 hours?

## 4. Data

The analysis uses a PostgreSQL table named `charging_sessions`.

The dataset contains information related to individual charging sessions, including:

| Column              | Description                      | Data Type  |
| ------------------- | -------------------------------- | ---------- |
| `garage_id`         | Garage or building identifier    | `VARCHAR`  |
| `user_id`           | Individual user identifier       | `VARCHAR`  |
| `user_type`         | Shared or private station type   | `VARCHAR`  |
| `start_plugin`      | Session start date and time      | `DATETIME` |
| `start_plugin_hour` | Session start hour               | `NUMERIC`  |
| `end_plugout`       | Session end date and time        | `DATETIME` |
| `end_plugout_hour`  | Session end hour                 | `NUMERIC`  |
| `duration_hours`    | Session duration in hours        | `NUMERIC`  |
| `el_kwh`            | Electricity consumed in kWh      | `NUMERIC`  |
| `month_plugin`      | Month when the session started   | `VARCHAR`  |
| `weekdays_plugin`   | Weekday when the session started | `VARCHAR`  |

## 5. Methodology

The analysis was performed using SQL against the `charging_sessions` table.

### 5.1 Unique Users per Garage

The first analysis calculates the number of distinct users associated with shared charging stations for each garage.

The query uses:

* `COUNT(DISTINCT user_id)` to identify unique users
* `WHERE user_type = 'Shared'` to restrict the analysis to shared stations
* `GROUP BY garage_id` to aggregate users by garage
* `ORDER BY` to rank garages by demand

### 5.2 Peak Charging Periods

The second analysis identifies the most frequent combinations of weekday and starting hour for shared charging sessions.

The analysis groups sessions by:

* Day of the week
* Hour when the charging session started

The results are ordered by the number of charging sessions to identify periods of higher demand.

### 5.3 Long-Duration Charging Sessions

The third analysis identifies shared-station users whose average charging session duration exceeds 10 hours.

The query uses:

* `AVG(duration_hours)` to calculate average session duration
* `GROUP BY user_id` to aggregate sessions by user
* `HAVING` to filter users based on their average duration
* `ORDER BY` to rank users by average charging duration

## 6. Key Findings

### Garage Demand

The garages with the highest number of distinct users accessing shared charging stations were:

| Garage | Unique Users |
| ------ | -----------: |
| Bl2    |           18 |
| AsO2   |           17 |
| UT9    |           16 |

These garages represent the highest observed concentration of users among the shared charging infrastructure analyzed.

### Peak Charging Periods

The highest number of charging sessions occurred during the following periods:

| Day      | Start Hour | Sessions |
| -------- | ---------: | -------: |
| Sunday   |      17:00 |       30 |
| Friday   |      15:00 |       28 |
| Thursday |      16:00 |       26 |
| Thursday |      19:00 |       26 |
| Sunday   |      18:00 |       25 |

Sunday at 17:00 represents the highest observed starting period in the analysis.

### Long-Duration Users

The users with the highest average charging duration among sessions exceeding the 10-hour threshold were:

| User     | Average Duration (hours) |
| -------- | -----------------------: |
| Share-9  |                    16.85 |
| Share-17 |                    12.89 |
| Share-25 |                    12.21 |
| Share-18 |                    12.09 |
| Share-8  |                    11.55 |
| AdO3-1   |                    10.37 |

These results highlight users whose average connection duration is substantially longer than the defined threshold.

## 7. Technologies

* SQL
* PostgreSQL
* Jupyter Notebook
* DataLab

## 8. Repository Structure

```text
ev-charging-analysis/
│
├── assets/
│   └── charging_station.jpg
│
├── notebooks/
│   └── ev_charging_analysis.ipynb
│
└── README.md
```

## 9. How to Explore the Project

The complete analysis is available in:

```text
notebooks/ev_charging_analysis.ipynb
```

The notebook contains the SQL queries and their corresponding executed results.

Because the original analysis was performed against a PostgreSQL database provided through the learning environment, the repository does not currently contain a local copy of the database.

## 10. Data Source

The project uses the Residential EV Charging from Apartment Buildings dataset.

The dataset was provided through Kaggle and is referenced in the original project under the Creative Commons Attribution 4.0 (CC BY 4.0) license.

## 11. Project Scope

This repository represents an introductory SQL analysis project.

The objective is to demonstrate the ability to:

* Understand a relational dataset
* Filter and aggregate data using SQL
* Work with distinct users
* Group data by categorical and temporal dimensions
* Calculate aggregate metrics
* Apply conditions to aggregated results
* Translate business questions into SQL queries
* Communicate analytical findings

Future projects in the portfolio will expand these skills through more advanced SQL, data visualization, statistical analysis, and business-oriented data analysis.

## 12. Author

Developed as part of a practical data analytics learning portfolio, with a focus on SQL and data analysis.
