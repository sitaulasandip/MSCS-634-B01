## Purpose

In this lab, I explore a real sales dataset, clean it, prepare it, and summarize it with statistics.

## Dataset

I used the Warehouse and Retail Sales dataset from Data.gov: https://catalog.data.gov/dataset/warehouse-and-retail-sales

It is published by Montgomery County, Maryland. The county sells alcohol in its own stores and from a warehouse to bars and restaurants. Each row is one product in one month. The file has 341,037 rows, and sales are measured in cases.


## Key insights

From the charts
- Stores sell mostly liquor and wine. The warehouse sells mostly beer (about 7.3 million cases) to bars and restaurants.
- When a store sells more of a product, it gets more of that product from the warehouse (correlation 0.93).
- Sales are highest in December (holiday season). March 2020 was also high, probably because of COVID-19 stock-up buying.
- Wine is 60% of all products, but liquor sells more cases in stores. More products does not mean more sales.

From the statistics
- Most products sell very little: 40% of rows have zero sales. The mean is much higher than the median, so the median is a better "typical" value.
- Retail sales and retail transfers have a correlation of 0.97 after cleaning.
- Year and month have almost no correlation with sales.

## Decisions and challenges

- Missing values: There were only a few. I dropped rows that are not real products (pallets, refunds, store supplies), filled missing sales with 0, filled the missing item type with the mode, and filled missing suppliers with "UNKNOWN".
- Outliers: The normal IQR rule marked 15.6% of rows as outliers, because 40% of the sales values are 0. That was too many. So I used the IQR rule on the log of sales instead, which marked only 122 rows (sales above 644 cases a month). These were real top sellers, like ice and Tito's vodka.
- Missing months: The dataset does not have every month (for example, March to December 2018 is missing), so the line chart jumps between some months.
- Large data: The scatter plot uses a random sample of 5,000 rows so it is easy to read.

## How to run

```bash
pip install -r requirements.txt
jupyter notebook Lab1_Data_Exploration.ipynb
```
