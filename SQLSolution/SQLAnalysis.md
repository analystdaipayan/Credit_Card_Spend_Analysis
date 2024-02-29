## 🤩 Queries

### 1. Write a query to print top 5 cities with highest spends and their percentage contribution of total credit card spends.

````sql
SELECT TOP 5 city,SUM(amount) AS City_Total_Spend, 
CONCAT((ROUND((100.0*SUM(Amount)/(SELECT SUM(Amount) FROM Credit_Card_Transactions)),2)),'%') AS City_Spend_Percentage
FROM Credit_Card_Transactions
GROUP BY city
ORDER BY 2 DESC;
````

### 2. Write a query to print highest spend month and amount spent in that month for each card type.


````sql
WITH Total_Spend_Details AS
(
SELECT card_type,txn_yr,txn_mth, SUM(amount) AS Total_Spend
FROM(
SELECT *, DATEPART(Year,transaction_date) AS txn_yr, DATEPART(Month,transaction_date) AS txn_mth
FROM Credit_Card_Transactions) AS calendar
GROUP BY card_type,txn_yr,txn_mth),
Rankings AS
(
SELECT *, RANK() OVER (PARTITION BY card_type ORDER BY Total_Spend DESC) AS Ranks
FROM Total_Spend_Details
)
SELECT*FROM Rankings
WHERE Ranks=1;
````

### 3. Write a query to print the transaction details (all the columns from the table) for each card type when it reaches a cumulative of 1000000 total spends. (We should have 4 rows in the o/p one for each card type).

````sql
WITH Running_Spends AS (
SELECT *,SUM(amount) OVER (PARTITION BY card_type ORDER BY transaction_date,transaction_id) 
AS Total_Spend
FROM Credit_Card_Transactions),
Ranks AS 
(
SELECT *, DENSE_RANK() OVER (PARTITION BY card_type ORDER BY Total_Spend) AS Ranking
FROM Running_Spends
WHERE Total_Spend>=1000000
)
SELECT * FROM Ranks
WHERE transaction_id IN (SELECT transaction_id FROM Ranks WHERE Ranking=1);
````

### 4. Write a query to find city which had lowest percentage spend for gold card type.

````sql
WITH card_wise_amount AS
(
SELECT city, card_type, SUM(amount) AS card_amount_spent
FROM Credit_Card_Transactions
GROUP BY city,card_type
),
city_wise_amount AS
(
SELECT city, SUM(card_amount_spent) AS city_amount_spent
FROM card_wise_amount
GROUP BY city
),
combined_details AS
(
SELECT CA.city, CA.card_type , CA.card_amount_spent, CI.city_amount_spent, 
100.0*CA.card_amount_spent/CI.city_amount_spent AS Spent_Percentage
FROM card_wise_amount CA 
INNER JOIN city_wise_amount CI 
ON CA.city = CI.city
WHERE CA.card_type='Gold'
)
SELECT TOP 1* FROM combined_details
ORDER BY 5;
````

### 5. Write a query to print 3 columns:  city, highest_expense_type , lowest_expense_type (example format : Delhi , bills, Fuel)

````sql
WITH amount_details as (
SELECT city,exp_type, SUM(amount) as total_amount from Credit_Card_Transactions
GROUP BY city,exp_type)
SELECT
city , max(case when rn_asc=1 then exp_type end) as Lowest_Expense_Type
, min(case when rn_desc=1 then exp_type end) as Highest_Expense_Type
from
(select *
,rank() over(partition by city order by total_amount desc) rn_desc
,rank() over(partition by city order by total_amount asc) rn_asc
from amount_details) AS Rankings
group by city;
````

### 6. Write a query to find percentage contribution of spends by females for each expense type.

````sql
SELECT exp_type,
100.0*SUM(CASE WHEN gender='F' THEN amount ELSE 0 END)*1.0/SUM(Amount) AS Female_Spent_Percent
FROM Credit_Card_Transactions
GROUP BY exp_type
ORDER BY 1
````

### 7. Which card and expense type combination saw highest month over month growth in Jan-2014.

````sql
WITH Calendar_details AS 
(
SELECT card_type,exp_type, 
DATEPART(YEAR,transaction_date) AS Txn_Year, 
DATEPART(MONTH,transaction_date) AS Txn_Month, SUM(amount) AS Total_Spend
FROM Credit_Card_Transactions
GROUP BY card_type,exp_type, DATEPART(YEAR,transaction_date), DATEPART(MONTH,transaction_date)
),
Growth_details AS
(SELECT *, 100.0*(Total_Spend-Prev_Spend)*1.0/Prev_Spend AS MoM_Growth
FROM
(SELECT *, LAG(Total_Spend,1) OVER (PARTITION BY card_type,exp_type ORDER BY Txn_Year,Txn_Month) AS Prev_Spend
FROM Calendar_details) AS Growth
WHERE Prev_Spend IS NOT NULL and Txn_Month=1 and Txn_Year=2014)
SELECT TOP 1 card_type, exp_type
FROM Growth_details
ORDER BY MoM_Growth DESC
````

### 8. During weekends which city has highest total spend to total no of transcations ratio.

````sql
SELECT TOP 1 city, ROUND((SUM(amount)/COUNT(transaction_id)),2) AS Spend_Txn_Ratio
FROM Credit_Card_Transactions
WHERE DATENAME(WEEKDAY,transaction_date) IN ('Saturday','Sunday')
GROUP BY city
ORDER BY Spend_Txn_Ratio DESC;
````

### 9. Which city took least number of days to reach its 500th transaction after the first transaction in that city

````sql
WITH Rankings AS(
SELECT *, ROW_NUMBER() OVER (PARTITION BY city ORDER BY transaction_date,transaction_id) AS Ranks
FROM Credit_Card_Transactions),
Dates AS (
SELECT city, MAX(transaction_date) AS Last_txn_date,MIN(transaction_date) AS First_txn_date 
FROM Rankings
WHERE Ranks=1 OR Ranks=500
GROUP BY city
HAVING MAX(transaction_date)!=MIN(transaction_date))
SELECT TOP 1 city, DATEDIFF(DAY,First_txn_date,Last_txn_date) AS Days_Difference
FROM Dates
ORDER BY 2;
````
