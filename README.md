# 🚕 GoodCabs: Tackling Seasonality in Tier-2 Mobility


## 🛺 Background
**GoodCabs**, founded in 2023, is a fast-growing **ride-hailing** startup focused on **India’s tier-2 cities**, providing affordable transport options and **empowering local drivers with sustainable income opportunities**. Operating in 10 cities, the company is working toward ambitious performance and satisfaction goals in 2024.


## 🚧 Problem Statement
As operations scaled, **seasonality** emerged as the biggest roadblock to consistent revenue growth. In **June 2024**, **GoodCabs faced its steepest revenue drop of ₹1.2 million, triggered by a sharp decline in ride demand driven by seasonal shifts**.

Like global players such as Uber and Grab, GoodCabs faces challenges tied to seasonal fluctuations in rider behavior—including academic calendars, holidays, and regional activity patterns—making demand forecasting difficult across smaller urban markets.

**How can GoodCabs design a predictive, data-driven strategy to minimize the effects of seasonality, stabilize revenue, and uphold its mission of empowering local drivers in tier-2 cities?**


## Data Structure & Entity Relationship Diagram (ERD)
The Goodcabs database comprises eight tables: `dim_city`, `dim_date`, `fact_trips`, `fact_Passenger_summary`,`dim_repeat_trip_distribution`,`City_target_passenger_rating`, `monthly_target_new_passengers`,`monthly_target_trips`, with a total row count of 425,000.
![GoodCabs_er_diagram](https://github.com/user-attachments/assets/7f07219a-18fb-45b0-bfce-02e612130a88)

### Relationship between these tables are as follows:
- `dim_city[city_id]` to `City_target_passenger_rating[city_id]` **(one to one)**
 
- `dim_repeat_trip_distribution[city_id]` to `dim_city[city_id]` **(many to one)**
 
- `dim_repeat_trip_distribution[month]` to `dim_date[date]` **(many to one)**
  
- `fact_Passenger_summary[city_id]` to `dim_city[city_id]` **(many to one)**
  
- `fact_Passenger_summary[month]` to `dim_date[date]` **(many to one)**
  
- `fact_trips[city_id]` to `dim_city[city_id]` **(many to one)**
  
- `fact_trips[date]` to `dim_date[date]` **(many to one)**
 
- `monthly_target_new_passengers[city_id]` to `dim_city[city_id]` **(many to one)**
  
- `monthly_target_new_passengers[month]` to `dim_date[date]` **(many to one)**
  
- `monthly_target_trips[city_id]` to `dim_city[city_id]` **(many to one)**
 
- `monthly_target_trips[month]` to `dim_date[date]` **(many to one)**






## 🚿 Data Cleaning 

### 🔧 Automated Error Handling in Power Query

**Objective:**  
Automatically replace errors across all columns (including future ones) with a specified value (e.g. `null` or `"ERROR"`), making my query resilient and scalable.

#### 🧹 M Code Steps

```m
// STEP 1: Create a dynamic list of {ColumnName, ReplacementValue} pairs
let
    ColumnReplacement = List.Transform(
        Table.ColumnNames(#"Changed Type"),
        each { _, null }  // Replace `null` with any custom error value like "ERROR"
    )
in
    ColumnReplacement


// STEP 2: Apply dynamic error replacement across all columns
= Table.ReplaceErrorValues(
    #"Changed Type",
    ColumnReplacement
)
```




## Data Transformation

### 1.🗓️ Added `date_type` Column (Weekday/Weekend) in `dim_date` table

#### 🧾 M Code

```m
= Table.AddColumn(
    dim_date,
    "date_type",
    each if Date.DayOfWeek([date], Day.Monday) >= 5 then "Weekend" else "Weekday",
    type text
)

```



### 2. Shortcut names for months for compact visualizations, especially for KPI's
- A calculated Column in the **`dim_date`** table
### DAX
``` 
month_short = SWITCH(MONTH(dim_date[date]),
                        1,"J",
                        2,"F",
                        3,"M",
                        4,"A",
                        5,"M" & UNICHAR(8201),
                        6,"J" & UNICHAR(8201)
              )
```




## Insights
1. 
![Screenshot (59)](https://github.com/user-attachments/assets/9753f731-6bf3-46ce-a239-abf1a440fd14)

2.
![Screenshot (60)](https://github.com/user-attachments/assets/7e155c09-4584-4d9b-8ae8-f5995b4a4c31)
