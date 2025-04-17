# 🚕 GoodCabs: Tackling Seasonality in Tier-2 Mobility


## 🛺 Background
**GoodCabs**, founded in 2023, is a fast-growing **ride-hailing** startup focused on **India’s tier-2 cities**, providing affordable transport options and **empowering local drivers with sustainable income opportunities**. Operating in 10 cities, the company is working toward ambitious performance and satisfaction goals in 2024.


## 🚧 Problem Statement
As operations scaled, **seasonality** emerged as the biggest roadblock to consistent revenue growth. In **June 2024**, **GoodCabs faced its steepest revenue drop of ₹1.2 million, triggered by a sharp decline in ride demand driven by seasonal shifts**.

Like global players such as Uber and Grab, GoodCabs faces challenges tied to seasonal fluctuations in rider behavior—including academic calendars, holidays, and regional activity patterns—making demand forecasting difficult across smaller urban markets.

**How can GoodCabs design a predictive, data-driven strategy to minimize the effects of seasonality, stabilize revenue, and uphold its mission of empowering local drivers in tier-2 cities?**


## Entity Relationship Diagram (ERD)
The Goodcabs database comprises eight tables: `Dim_city`, `Dim_date`, `Fact_trips`, `Fact_Passenger_summary`,`Dim_repeat_trip_distribution`,`City_target_passenger_rating`, `Monthly_target_new_passengers`,`Monthly_target_trips` among others, totaling approximately 425,000 rows.
![GoodCabs_er_diagram](https://github.com/user-attachments/assets/7f07219a-18fb-45b0-bfce-02e612130a88)
