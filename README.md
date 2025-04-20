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



## Executive Summary – H1 2024
**Overview of findings** 

After analyzing the market size in India,2024. GoodCabs' market share was less than 2%(assumed target) of the estimated market value in 2024 in India. Actual performance has fallen short, reaching only ₹108.2 million INR in revenue—33% below target. The average revenue growth rate stands at -3.31%, largely due to a significant revenue drop of ₹2.6 million INR in June.

Trip volumes have been on a consistent decline since February, with the exception of a temporary rise in May. Notably, many cities recorded their highest trip counts in April and the lowest in June. Weekend trips, which contribute approximately 56% of total revenue, have been steadily declining since February. Weekday revenue experienced a steep drop in June.

The Repeat Passenger Rate (RPR) plummeted by 11% in June, and new passenger acquisition has been consistently declining since February. These trends are primarily attributed to seasonal fluctuations, subpar passenger and driver ratings, UX/UI design shortcomings, overdependence on two key cities—Jaipur and Kochi—and the absence of a robust conversion strategy.

The following sections will delve deeper into the data, uncover actionable insights, and identify key opportunity areas for improving performance and driving sustainable growth.

### Company's Status?
![P1](https://github.com/user-attachments/assets/1721b836-1b9c-4fcd-880d-b0c12060cbf1)


### Key Insight 1
![P2](https://github.com/user-attachments/assets/5911c77b-adc6-4786-bfe4-af7cf9ad1afd)



### Key Insight 2
![P3](https://github.com/user-attachments/assets/e6c8d225-d382-4c41-8795-01aaa074cc2a)



### Key Insight 3
![P4](https://github.com/user-attachments/assets/4b9ad2be-e7d7-48cd-8ff6-12ac212139be)



### Recommendations 
![P5](https://github.com/user-attachments/assets/a93123e7-e4e2-4ad5-9609-ad8ad2424b08)





