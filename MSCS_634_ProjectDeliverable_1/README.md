# MSCS 634 Project - Deliverable 1: Data Collection, Cleaning, and Exploration

Name: Sandip Sitaula

Course: MSCS 634 - Advanced Big Data and Data Mining

## Dataset Summary

I used the Online Retail dataset from the UCI Machine Learning Repository (https://archive.ics.uci.edu/dataset/352/online+retail). It has sales from a UK online store that sells gifts and home decor, from December 2010 to December 2011. Many of its customers are small shops that buy in bulk.

The dataset has 541,909 rows and 8 columns: InvoiceNo, StockCode, Description, Quantity, InvoiceDate, UnitPrice, CustomerID and Country. There are 25,900 invoices, 4,070 products, 4,372 customers and 38 countries.

I chose this dataset because it is large, it is real data that needs cleaning, and it can be used for every part of the project. I can use it for regression (predict customer spending), classification (predict if a customer will buy again), clustering (group customers) and association rules (find products bought together).

## Data Cleaning Steps

1. Removed extra spaces in product names and made stock codes upper case.
2. Removed 5,268 duplicate rows.
3. Removed 1,455 rows with no product name. I kept the rows with no CustomerID (25% of the data) and marked them with a new column.
4. Moved 9,251 cancelled orders to their own table and removed 3 accounting rows.
5. Removed 2,346 rows that were not products, like postage, fees and gift vouchers.
6. Removed 1,046 rows with zero or negative quantity or price. These were mostly staff notes like "damaged".
7. Gave each product only one name (212 products had more than one).
8. Removed 22 very large orders that were cancelled soon after they were placed.

After cleaning, I kept 522,516 rows (96.4% of the data). I also made a customer table with 4,333 customers.

## Data Exploration Steps

- Looked at the distribution of quantity, price and line total with histograms.
- Checked outliers with box plots and the IQR rule.
- Looked at sales by month, by day of the week and by hour.
- Looked at sales by country and the top products.
- Looked at basket size (number of products in each order).
- Made customer features (Recency, Frequency, Monetary) and checked how they relate with a scatter plot and a correlation heatmap.

## Key Insights

- Sales go up a lot from September to November because shops buy for Christmas. December 2011 looks low because the data stops on December 9.
- There are no orders on Saturdays, and most orders come during work hours.
- The UK makes 84.7% of revenue. The top 20% of products make 77.7% of revenue, and the top 10% of customers make 60%.
- The rows with no CustomerID look like orders from guest shoppers.
- Quantity, price and spending are very skewed, so I will need log transforms for modeling.
- 34.7% of customers ordered only once.
- Customers who order more often also spend more (correlation 0.81).
- A typical order has 15 different products, which is good for finding products bought together.

## Challenges and How I Solved Them

- 25% of rows had no CustomerID. I could not guess the IDs, and removing the rows would lose a lot of real sales. So I kept them and only used rows with a CustomerID for customer analysis.
- The normal IQR rule marked too many rows as outliers, because big orders are normal for a store that sells to shops. I used the IQR rule on the log of the values instead, and only removed big orders that were cancelled.
- My first check for cancelled orders also caught a customer who cancelled an order and later ordered again. The second order was real, so I changed the check to only count cancellations that happened after the order.
- One wrong order of £38,970 was fixed with a "Manual" credit instead of a normal cancellation, so my check missed it. I found it by looking at the largest orders and removed it by hand.
- Postage, fees and vouchers were mixed in with products. I listed all unusual stock codes and checked each one.
- The Excel file is big and slow to load, so I saved the clean data as smaller CSV files for the next deliverables.


## Reference

Chen, D. (2015). Online Retail [Dataset]. UCI Machine Learning Repository. https://doi.org/10.24432/C5BW33
