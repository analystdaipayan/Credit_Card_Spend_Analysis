# 📊 Credit Cards Spend Analysis 📊

## 📍 [About Data](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/tree/main/Datasets) 
- We have the data of the transactions made by credit cards in each city of India specifying the amount spent in each transaction.
- The Credit Cards are of type Silver, Signature, Gold and Paltinum.
- The spends are usually done on expenses that includes Entertainment, Food, Bills, Fuel, Travel and Grocery
- The data ranges from the Year 2013 - Year 2015.

## 🛠️ Tools Used
- Excel
- Microsoft SQL Server

## ❓ Analysis Scenarios
- [Get the Top 5 Cities with the highest spends and also their contribution percentage in the overall spends.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)
- [Get the month which registered the highest spending and the spending distribution across each card type.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)
- [Get the transaction details of each card type when it reached a cummulative total of 1000000 spend.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)
- [Get the city that had the lowest percentage spend for Gold Card type.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)
- [Get every cities Highest and Lowest Expense Type.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)
- [Get the Females contribution for each Expense Type.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)
- [Get the Card and Expense Type Combination that registered the highest Month on Month Growth in JAN-2014.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)
- [Get the city that had the highest total spend to total no of transactions ratio.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)
- [Get the city that took least number of days to reach 500th transaction.](https://github.com/AnalystDaipayan/Credit_Card_Spend_Analysis/blob/main/SQLSolution/SQLAnalysis.md)

## 🎡 Concepts Covered
- Usage of ```Grouping and Aggregation Functions```.
- Usage of ```CTE's and Subqueries```.
- Usage of ```Window Functions``` like ```RANK, DENSE RANK, LEAD``` and ```LAG```.

## 🎯 Analysis Results 
- The top 5 cities along with their spend percentage are : ```Greater Mumbai (14.15%)```, ```Bengaluru (14.05%)```,```Ahmedabad (13.93%)```,```Delhi (13.67%)```, ```Kolkata (2.83%)```.
- ```Gold Card``` made the highest total spend of ```55455064``` in ```Jan-2105```, ```Platinum Card``` made the highest total spend of ```57936507``` in ```Aug-2014```, ```Signature Card``` made the highest total spend of ```58799522``` in ```Dec-2013``` and ```Silver Card``` made ```59723549``` in ```Mar-2015```.
- With the given transaction id's the different card types made their cummulative total of 1000000: ```Transaction-ID 1522 - Gold```,```Transaction-ID 191 - Platinum```,```Transaction-ID 73 - Signature``` and ```Transaction-ID 1522 - Silver```.
- The ```Dhamtari City``` had the ```lowest percentage spend for Gold Card``` Type resulting in ```33.29%```.
- The ```females``` had the ```highest spend percentage``` share for the ```Bills Expense Type``` resulting in ```63.94%```, followed by spend in ```Food``` with ```54.90%``` and ```Travel``` with ```51.13%```.
- The ```Gold and Travel```, ```card and expense combination type``` saw the ```highest Month-on-Month Growth``` in ```January-2014```.
- ```During Weekends``` the ```Sonepur City``` had the ```highest spend to transaction ratio``` resulting to an ```amount of 299905```.
- ```Benagluru``` took the ```least number of days to reach it's 500th Transaction```, within ```81 Days```.

## 🎉 That's it! 🎉

