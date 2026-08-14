# DSA3050-PowerBI-Harina-666983
# Dataset
## Source
Data = https://www.kaggle.com/datasets/krithi96/dirty-data-for-cleaning
Rows: 22,000
Columns = 13
Contains:
-	Mixed data types 
-	Incomplete or missing entries 
-	Duplicates, inconsistencies, and formatting issues 
-	Potential key metrics hidden across columns
The dataset represents booking information for Airbnbs in America. It has columns that describe the customer and their booking information, like check-in and check-out dates, price, and reviews.

## Business problem
This project aims to create a Power BI solution that purifies and standardizes the raw booking data while providing a reliable, interactive dashboard for leadership to oversee revenue performance, booking patterns, and risk of payment/cancellation by city and across time.

## Business questions
1.	Revenue performance — What is the overall and average booking revenue by city and by month/quarter, and how is it changing over the specified period?
2.	Cancellations — What is the rate of cancellations categorized by city and price tier, and is there any correlation between cancellations and review ratings or duration of stay?
3.	Payment risk — What percentage of overall booking value remains in "pending" or "unpaid" status by city, and what is the associated financial risk?
4.	Guest satisfaction — In what ways do average review ratings differ by city and by listing, and is there a relationship between review ratings and the price per night or duration of stay?
5.	Reservation/stay trends — How is the length of stay (nights) distributed among bookings, and how does the duration of stay correlate with total revenue for each booking?
6.	Effect on data quality What percentage of entries have absent, incorrect, or dummy values (empty guest name/email, -1 or N/A review scores, negative nights, non-numeric prices), and which areas or attributes are the most impacted?
7.	Evaluating listings — Identifying which specific listings yield the most revenue and highest review ratings and recognizing any underachieving listings that should be noted.

# Power Query
1. Loaded the data
2. Renamed columns
3. Changed data types (Changed checking_data and checkout_date to date data type, Price_per_night and total_price to decimal)
4. Text trim for Guest Name
5. Replace values (fixed the different listing cities: eg LA, la = Los Angeles)
   <img width="975" height="519" alt="image" src="https://github.com/user-attachments/assets/98aec6c2-74e2-4b7d-ba75-d1881a4e2627" />

6. Removed blanks (removed blanks from Price per Night)
7. Removed duplicates from booking ID
8. Filled blank values in Guest Name with "Unknown Guest"
<img width="975" height="426" alt="image" src="https://github.com/user-attachments/assets/6639e4cf-c850-4b85-877d-455af8822eee" />
9. Replaced incorrect negative review scores with their positive value
10. Custom column for number of nights and total price
<img width="975" height="618" alt="image" src="https://github.com/user-attachments/assets/df683022-7fbd-4a36-beb2-b4d91d086c4e" />
<img width="975" height="618" alt="image" src="https://github.com/user-attachments/assets/6fb4931c-51cd-48d7-820c-c111a6dbaab5" />
11. Deleted column number_of_Nights and Total Price
12. Split column Booking ID by the delimiter "-" to just keep the numeric ID value
<img width="975" height="618" alt="image" src="https://github.com/user-attachments/assets/a6d1b24e-2e8e-4436-835d-f33d759b1ef9" />

# Modeling
<img width="975" height="674" alt="image" src="https://github.com/user-attachments/assets/6c9658e7-336e-4386-808a-5991515ce3ec" />

<img width="624" height="231" alt="image" src="https://github.com/user-attachments/assets/8be1d5b1-2da1-4e88-8195-3148d496caf9" />

FactBookings contains the transactional details of the dataset — one entry for each booking — as well as the metrics that are summarized in analysis: Duration Nights, Price per Night, Total Price Payment, Review Score. 
It is located at the core of the model, as all other tables are designed to either describe or filter these booking transactions, aligning with the FactSales pattern.
Reasons for the creation of each dimension:
DimGuests — isolates attributes that identify guests (Guest Name, Email Address) from the fact table. Guests have the ability to make numerous bookings, which means that keeping their information in a single dimension prevents the need to duplicate the same name/email in several fact rows and facilitates clear guest-level analysis (e.g., identifying repeat bookers).
DimListings — differentiates property characteristics (Listing City) from reservations, as a single listing can be reserved multiple times. This enables city-level filtering/aggregation to occur without repeating city text in each fact row.
DimDate — a specific calendar table created using CALENDAR(), covering the range from the first check-in to the last check-out. It facilitates time-related analysis (reservations by month, quarter, day of the week) that raw date columns cannot efficiently handle and meets the need for an appropriately marked date table.

# DAX
D – Measures
1.	Total Sales
 <img width="824" height="66" alt="image" src="https://github.com/user-attachments/assets/222e5efa-c749-4578-8340-12557d1bf433" />

2.	Average Price Per Night
 <img width="975" height="39" alt="image" src="https://github.com/user-attachments/assets/878b8198-4e18-4bec-bd81-f623b4e2f48b" />

3.	Total Bookings
 <img width="703" height="66" alt="image" src="https://github.com/user-attachments/assets/64af37e0-36a1-47bd-87c8-855651f500f0" />

4.	YTD sales
 <img width="975" height="58" alt="image" src="https://github.com/user-attachments/assets/f0d63ae5-68d5-4278-ad36-c9929f2e30c0" />

5.	Rank of the Cities per total sales
 <img width="975" height="54" alt="image" src="https://github.com/user-attachments/assets/c77e3b01-3873-4b72-9384-70597ff3e1c1" />

6.	Total Bookings in LA
 <img width="975" height="47" alt="image" src="https://github.com/user-attachments/assets/74943427-2be8-4cd7-8dda-4649d9aff72b" />

7.	Previous Years’ bookings
   <img width="975" height="51" alt="image" src="https://github.com/user-attachments/assets/d725c983-0290-45a0-8d6c-5135b1af43b6" />

8.	YoY Growth %
 <img width="666" height="225" alt="image" src="https://github.com/user-attachments/assets/ae519da2-6bed-487d-b4ce-b480d19a7fc6" />

9.	New York Sales % of Total
 <img width="877" height="269" alt="image" src="https://github.com/user-attachments/assets/f23fd079-a861-418b-b500-7fa6112fa2f9" />

10.	Booking Price tier
 <img width="975" height="47" alt="image" src="https://github.com/user-attachments/assets/b288f05b-f210-40c3-a3a4-e2ce27264cf5" />

11.	Yearly goal Status
 <img width="683" height="470" alt="image" src="https://github.com/user-attachments/assets/7ddd85b8-fba6-4f18-a457-79a1dec77ed9" />

12.	Unique listings that are paid for
 <img width="734" height="195" alt="image" src="https://github.com/user-attachments/assets/9b7dc812-56b8-4971-870b-96a40dcaa13c" />

13.	Total Selected Paid Bookings
 <img width="817" height="275" alt="image" src="https://github.com/user-attachments/assets/bffdebc2-be99-47fb-96e0-f0f0ec5f0ab4" />


## DAX Documentation
1.	Total Sales
This measure calculates the total sum of money gathered from the bookings. This is important to have as it shows the business how much money they have earned in total. The main DAX function used is SUM(). The measure on the dashboard is a KPI card.

2.	Average price per night
This measures the average price per night of the booking. It is important to have as it allows the business to have an idea of how much the guests have been paying on average. The DAX function used is AVERAGE(). The measure on the dashboard is a KPI card.

3.	Total bookings
Total bookings is the count of the number of bookings the business has made; it is important to have this information to have an idea of the number of bookings made. The DAX function used is COUNTROWS(). Dashboard visualisation is a KPI card.

4.	Rank of cities per total sales
This is the measure that ranks the cities based on the sales they each have. It is an important measure to have as it shows which city is the most expensive. The DAX function used is RANKX(). Dashboard visualisation is a KPI card.

5.	Yearly goal status
This is the measure that highlights if the business has reached its goal of 5000 paid bookings within the year. It keeps the business knowing if they’re in line with their goals or changes need to be made. DAX functions used are VAR() and CALCULATE(). Dashboard visualisation is KPI card.

6.	YoY growth %
This is a measure that shows the year-over-year trend growth of the sales; it compares current year sales to the previous year’s sales to show if there has been any change. The DAX function used is DIVIDE(). Dashboard visualisation is a KPI card.

# Dashboard and insights

<img width="975" height="546" alt="image" src="https://github.com/user-attachments/assets/337f775a-790c-4922-85da-298c7932016c" />
This dashboard page should display the goal for the year, the total number of sales and bookings, the average price per night, the year-over-year growth %, and the city rank as KPI cards. 
The slicers allow the manager to pick the specific year and city to gain more information on the sales. 
The pie chart shows that the reviews and average price per night have no trend; the price does not seem to increase or decrease with higher reviews.

<img width="975" height="547" alt="image" src="https://github.com/user-attachments/assets/42287b23-df5c-4a7e-a3e3-31c893f94dd5" />
This page of the dashboard shows the analysis of the 3 cities: New York, Los Angeles, and San Francisco. 
It shows the divide of the average total price and price per night between the 3 cities; there seems to be no significant difference. 
It shows how the average night duration varies with whether the booking is cheap or expensive, and how the rank varies with the booking tier. 
The slicer allows you to slide between the years.

<img width="975" height="616" alt="image" src="https://github.com/user-attachments/assets/3c016897-12a7-4c0e-bb5f-1b8db66b1f59" />
Why did Total sales dip or spike in certain periods? 
The decomposition tree shows that the 1st and 4th quarters have the least sales that were paid. 
This could be because the 1st and 4th quarters are during the holiday season or just after, and therefore people have spent a lot of money and so they cannot pay during those months. This is consistent with all 3 cities.
Average price per night is highest for bookings that scored a 2, and generally drops as review scores rise toward 4, 6 — before an oddity at score 1, which sits closer to the low end alongside "Not Reviewed." 
This is the opposite of what is expected; it is expected that as reviews increase, so does the price. 
This could be because with a higher price, guests may have higher expectations to match that price point, so they leave a poor score rather than a great review score. 
The score anomaly should be confirmed; it could be due to a small sample size and so a little unreliable.
The stacked column chart shows that cancelled bookings (True) show a higher average total price than completed bookings (False) at every single review score level, without exception. 
It does support that higher-value bookings are more likely to be cancelled, regardless of review score. 
Cancelled bookings carry a higher-than-average total price than completed bookings across every review score, suggesting higher-value bookings are at greater cancellation risk.
