# 🚖 Ride Analytics Dashboard (Power BI)

Interactive Power BI dashboard built using a dataset of 150K ride bookings.  
The project replicates analytics used by ride‑hailing companies (Uber/Bolt/Uklon) and focuses on demand patterns, ride status performance, cancellations, and operational issues.

---

## 📊 Key Features

- Ride demand by **hour** and **day of week**
- Ride status distribution (Completed, Cancelled, No Driver Found, Incomplete)
- Vehicle type popularity
- Problematic rides analysis
- Hour × Day heatmap
- KPI metrics (Total Rides, Completion Rate, Problematic Rides)

---

## 🧠 Insights

- Peak demand at **8:00 AM**
- Monday is the most active day
- ~38% of rides are problematic (driver cancellations + no driver found)
- Low‑cost vehicle types dominate (Auto, Go Mini, Bike)
- Strong weekday morning peaks across all days

---

## 🛠 Tech Stack

- **Power BI** (visuals, DAX, modeling)
- **SQL** (data exploration)
- **Power Query** (cleaning)
- Dataset: `ncr_ride_bookings.csv`

---

1.Which ride status occurs most frequently
SELECT 
    `Booking Status` AS ride_status,
    COUNT(*) AS total_rides
FROM ncr_ride_bookings
GROUP BY ride_status
ORDER BY total_rides DESC;

2.Which vehicle type is used most often?
SELECT 
    `Vehicle Type` AS vehicle_type,
    COUNT(*) AS total_rides
FROM ncr_ride_bookings
GROUP BY vehicle_type
ORDER BY total_rides DESC;

During which hours of the day do people book rides most frequently
SELECT 
    HOUR(Time) AS hour_of_day,
    COUNT(*) AS total_rides
FROM ncr_ride_bookings
GROUP BY hour_of_day
ORDER BY total_rides DESC;
4.Which days of the week have the highest number of rides?
SELECT 
    DAYNAME(Date) AS day_of_week,
    COUNT(*) AS total_rides
FROM ncr_ride_bookings
GROUP BY day_of_week
ORDER BY total_rides DESC;

5.On which day of the week do the most problematic rides occur?
SELECT 
    DAYNAME(Date) AS day_of_week,
    COUNT(*) AS problematic_rides
FROM ncr_ride_bookings
WHERE `Booking Status` != 'Completed'
GROUP BY day_of_week
ORDER BY problematic_rides DESC;

6.Heatmap: Which hours and days have the highest ride activity
SELECT
    DAYNAME(Date) AS day_of_week,
    HOUR(Time) AS hour_of_day,
    COUNT(*) AS total_rides
FROM ncr_ride_bookings
GROUP BY day_of_week, hour_of_day
ORDER BY day_of_week, hour_of_day DESC;
7.Which hours have the highest number of problematic rides (No Driver Found + Incomplete)?
SELECT
    HOUR(Time) AS hour_of_day,
    `Booking Status` AS ride_status,
    COUNT(*) AS problematic_rides
FROM ncr_ride_bookings
WHERE `Booking Status` != 'Completed'
GROUP BY hour_of_day, ride_status
ORDER BY problematic_rides DESC;




👤 Author
Vladyslav Bilokin  
Data Analyst (Power BI • SQL • Excel)
Navan, Ireland
