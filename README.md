# SQL_Interview_Question


### Q.1 Calculate the cancellation rate for each room type over the last 6 months, considering only bookings with a minimum stay of 2 nights.

![image](https://github.com/user-attachments/assets/3587954f-3da4-487d-966c-2e59d3cc979e)

 ```sql
 SELECT
 RoomType,
 COUNT(*) AS TotalBooking,
 ROUND(SUM(IsCancelled)*100.0/ COUNT(*),2) AS CancellationRatePercent
FROM
  bookings
WHERE
  BookingDate >=DATEADD(MONTH,-6,GETDATE())
  AND DATEDIFF(DAY, CheckInDate,CheckOutDate)>=2
GROUP BY
  RoomType;
   ```
![image](https://github.com/user-attachments/assets/c37c373a-c49c-4500-8e13-2da3ae7b5b1e)

### Q.2 Determine the average conversion rate (confirmed bookings vs. search events) for users grouped by their country and device type.  

![image](https://github.com/user-attachments/assets/0c843707-6f27-4bb7-a1c0-9b016f505a13)

 ```sql
SELECT
  Country,
  DeviceType,
  ROUND(AVG(CAST(ConfirmedBookings AS FLOAT)/ NULLIF(SearchEvents,0))*100,2) AS AvgConversionPercent
FROM
  user_activity
GROUP BY 
  country, DeviceType;
   ```
-- Alternative without AVG() ( if you need total conversion insted of average per user)
 ```sql
SELECT
  Country,
  DeviceType,
  SUM(ConfirmedBookings) AS TotalBookings,
  SUM(SearchEvents) AS TotalSearches,
  ROUND(SUM(ConfirmedBookings)*100/NULLIF(SUM(SearchEvents),0),2) AS ConversationRatePercent
FROM
  user_activity
GROUP BY 
  Country, DeviceType;
 ```
![image](https://github.com/user-attachments/assets/719198d6-9dd8-4aa4-98db-ae374e11a77e)

![image](https://github.com/user-attachments/assets/280fd234-c2bc-4459-bb77-f3c1e9c77f27)




