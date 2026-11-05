Zomato Order & Restaurant Analysis Using Power BI

Analysis of Zomato orders, sales based on restaurants using SQL and PowerBI


An end-to-end analysis of Zomato restaurant and order data. The data was cleaned and transformed with SQL (pgAdmin), then modelled and visualised in Power BI to find top restaurants, order patterns by city and area, and what affects customer ratings.

 Domain:  Food & Beverage, Business Analytics
 Tools:  PostgreSQL (pgAdmin), Excel, Power BI, DAX

---

  Problem Statement

Raw restaurant and order data does not show what drives sales on its own. This project turns it into a dashboard that answers questions such as:

- Which restaurants earn the most?
- Which cities and areas bring the most orders and revenue?
- Does price range or delivery time affect customer ratings?
- When are sales high or low?

---

  Dataset

| Table | Description |
|---|---|
| `Zomato_Restaurants` | Restaurant details such as city, area, price range and rating |
| `Zomato_Orders` | Order details such as order amount, date, delivery time and customer rating |

Both tables are linked by `restaurant_id`.

---

  Project Workflow

 # Step 1: Load data into PostgreSQL (pgAdmin)
- Created a database and two tables: `Zomato_Restaurants` and `Zomato_Orders`.
- Imported both CSV files.

 # Step 2: Clean and transform with SQL
- Removed duplicate records.
- Handled NULL values.
- Counted restaurants per city.
- Found the top 5 cities by orders.
- Calculated total revenue per restaurant.
- Calculated average order amount per city.
- Found the top 5 restaurants by total sales.
- Joined both tables to get restaurant names with order details.
- Exported the final dataset to Excel.

 # Step 3: Power BI
- Loaded the Excel file and checked data types in Power Query.
- Created a relationship between the two tables using `restaurant_id`.
- Wrote DAX measures (see below).
- Built the visuals and combined them into one dashboard.

---

  DAX Measures

 Total Sales : adds up the order amount.
```DAX
Total Sales = SUM(Zomato_Orders[total_cost])
```

 Total Orders : counts the orders.
```DAX
Total Orders = COUNT(Zomato_Orders[order_id])
```

 Average Order Value : total sales divided by number of orders. `DIVIDE` avoids a divide-by-zero error.
```DAX
Avg Order Value = DIVIDE([Total Sales], [Total Orders])
```

 Total Restaurants : counts each restaurant once.
```DAX
Total Restaurants = DISTINCTCOUNT(Zomato_Restaurants[restaurant_id])
```

 Average Delivery Time 
```DAX
Avg Delivery Time = AVERAGE(Zomato_Orders[delivery_time])
```

 Average Customer Rating 
```DAX
Avg Customer Rating = AVERAGE(Zomato_Orders[customer_rating])
```

 Total Sales per Restaurant : used in the top 10 / bottom 10 tables. It respects the restaurant name in each table row.
```DAX
Total Sales per Restaurant = SUM(Zomato_Orders[total_cost])
```

---

  Dashboard

 # Main dashboard
![Zomato Dashboard](images/dashboard_zomato_orders.PNG)

It includes:
- KPI cards: total sales, average order value, total restaurants, total orders
- Bar chart: restaurants per city
- Pie chart: orders by city
- Column chart: top 5 restaurants by sales
- Line chart: monthly sales trend
- Scatter plots: delivery time and rating by price range, and customer rating vs. average rating
- Tree map: revenue by area
- Slicers: city, area, price range

 # Top 10 and Bottom 10 restaurants
![Top and Bottom Restaurants](images/top_and_bottom_restaurants.PNG)

Tables with conditional formatting that show total sales, total orders and average order value, with filters for city, area and price range.

---

  Key Insights

 Overview 
- Total sales are about 15.57M from 15K orders across 500 restaurants.
- Average order value is about 1.04K.

 Cities 
-  Mumbai  has the most restaurants (115) and the most orders (3.38K), followed closely by  Bangalore  (109 restaurants, 3.3K orders).
- Delhi, Kolkata and Chennai have fewer restaurants (91 to 93) and fewer orders (2.73K to 2.86K).
- The order split is fairly even across the five cities. No single city dominates.

 Areas 
-  Area A  earns the most revenue (3.39M) and  Area E  the least (2.91M). The gap between areas is small.

 Restaurants 
- The top restaurant is  Restaurant_116  with about 51K in sales, followed by Restaurant_262, Restaurant_56, Restaurant_27 and Restaurant_127.
- The top 10 restaurants earned about 475K from 428 orders, with an average order value of about 1,110.
- The bottom 10 earned about 164K from 178 orders, with an average order value of about 923.
- So top restaurants do better on both  more orders and a higher order value .

 Trends over time 
- Monthly sales stay in a band of about 1.26M to 1.37M in 2024. Sales peak around  April  and are lowest around  January and May to June .

 Ratings 
- Average customer ratings stay around 3.0 whatever the restaurant's own average rating, so there is  no clear correlation  between the two.
- Delivery time is almost the same across price ranges (about 52.3 to 52.5 minutes), and ratings differ only slightly (about 2.98 to 3.03). Medium price range has the best rating and High the lowest.

---

  Recommendations

1. Focus marketing on  Mumbai and Bangalore , which lead in both restaurants and orders.
2. Study what top restaurants do (higher order value, steady orders) and share these practices with low performers.
3. Look at the bottom 10 restaurants for ways to raise order value, for example through combos or add-ons.
4. Plan offers for the low months (January, May and June) to keep sales steady.
5. Investigate other causes of low ratings, since price and delivery time make little difference.

PPT:- https://canva.link/9n0o63a2npdbjf8

---

  Repository Structure

 sql/         # SQL queries (pgAdmin)
data/        # Cleaned dataset (Excel)
 images/      # Dashboard screenshots
PowerBI/      .pbix # Power BI file
PPT/          
README.md


---

  Skills Used

SQL (PostgreSQL), Data Cleaning, Data Modelling, DAX, Power BI, Data Visualisation, Business Insights

