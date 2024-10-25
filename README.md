# Car Sales Analysis

<br>

### COMPANY OVERVIEW :

The company is a fictitious car dealership company offering a range of car models. To better monitor and analyze their sales performance, I aimed to develop a detailed Car Sales Dashboard using **Power BI**.

<br>

--- 

### TABLE OF CONTENT








<br>


### PROJECT OVERVIEW :

The goal of this project is to create an interactive and dynamic Car Sales Dashboard that will display key performance indicators **(KPIs)** related to car sales, average price, etc., providing insights into **sales trends** over time and supporting **data-driven decision-making**. With interactive visualizations and intuitive analytics, stakeholders can effortlessly track sales by model, region, and time period, enabling informed decision-making and strategic planning for growth. 

<br>

---

### DATA COLLECTION

The dataset used for this project was sourced from Kaggle and downloaded in Excel format. It spans the years **2022 and 2023** and contains **16 columns** and **23,906 rows**, a quick descripton of the data:

![Screenshot 2024-10-23 131450](https://github.com/user-attachments/assets/1a708642-d547-4d88-a31f-a40c1f2078ee)

**Column descriptions**

**Car_id**: Unique identifier assigned to each car sale.

**Date**: The date on which the car sale was made.

**Customer Name**: The name of the customer who purchased the car.

**Gender**: The gender of the customer.

**Annual Income**: The annual income of the customer (in the local currency).

**Dealer_Name**: The name of the car dealership where the car was sold.

**Company**: The brand or company that manufactured the car.

**Model**: The specific model of the car sold.

**Engine**: The type of engine the car is equipped with.

**Transmission**: The type of transmission in the car (e.g., manual or automatic).

**Color**: The exterior color of the car.

**Price ($)**: The sale price of the car in US dollars.

**Dealer_No**: The identification number assigned to the dealer.

**Body Style**: The body type of the car (e.g., SUV, hatchback).

**Phone**: The phone number of the customer or dealer.

**Dealer_Region**: The geographical region where the dealer is located.

<br>

---

## DATA CLEANING

I initiated by checking the quality of the data, for which I used the **Column distribution** and **quality** feature in power query editor. There were no errors and empty values found. In the engine column I **replaced** the value (DoubleÂ Overhead Camshaft) with (Double Overhead Camshaft).

 <br>

---

 ## ANALYSIS

### Calendar Table

The first thing I did while starting to analyze the data was creating a calendar table. The calendar table helped me in performing accurate and flexible **time-based analysis**. It allowed me to easily perform date-related calculations such as Year-to-Date (YTD), Month-to-Date (MTD), and Year-on-year (YOY), as well as compare data across different time periods.

<br>

First I created a table named **Calendar table**; 
``` dax
CALENDAR TABLE = CALENDAR(MIN(car_data[Date]), max(car_data[Date]))
```
The formula generated a range of dates based on the earliest and latest dates found in the "car_data" table under the "Date" column in a new table.

Then I extracted the **month, year and week** from the designated column, using the following formulas:

``` dax
--- for year
Year = YEAR('CALENDAR TABLE'[Date].[Date])

--- for month
Month = FORMAT('CALENDAR TABLE'[Date], "MMMM")

--- for week
Week = WEEKNUM('CALENDAR TABLE'[Date].[Date])
```
<br>
<br>

A quick look at the Calendar Table:

![Screenshot 2024-10-24 144239](https://github.com/user-attachments/assets/e38c0af2-dbd4-4699-a590-dd55da97cba0)

<br>
<br>

To establish a relationship between the car_data table and the newly created Calendar_table by connecting them through the common field which is **Date**
In the calendar table, each date appeared only once, denoted by the symbol '1', while in the car_data table, some dates might have appeared multiple times, indicated by the symbol '*'. Which signified a **One-to-Many** relationship between the two tables.

<br>
<br>

Then, to address the key objectives of this project, I created KPI cards and visualization charts. These visuals offer a focused view of sales patterns, regional strengths, and customer preferences.

### KPI CARDS

I used **DAX measures** to create these KPI cards, offering quick insights into key metrics like total sales, average price, and cars sold.

- **Sales Overview :**

   **Year-to-Date (YTD) Total Sales** : It is the cumulative sales from the **start of the year to the current date**, used to track sales performance within the year. YTD 
     Total sales is **$371.2M**.

  ``` dax
        YTD Total Sales = TOTALYTD(SUM(car_data[Price ($)]), 'CALENDAR TABLE'[Date])
   ```
   
   **Month-to-Date (MTD) Total Sales** : The Month-to-Date (MTD) total sales show the sales generated within the **current month**. It allows for tracking monthly 
     performance. MTD Total Sales **$54.28M**

  ``` dax
        MTD Total Sales = TOTALMTD(SUM(car_data[Price ($)]), 'CALENDAR TABLE'[Date])
   ```

   **Previous-year-to-date (PYTD) Total Sales** : refers to the total sales accumulated from the beginning of the previous year up to the same date as the current year of 
     the privious year. It serves as a benchmark to **compare** the current Year-to-Date (YTD) sales performance with the same period in the previous year, helping 
     businesses assess growth, decline, or consistency in sales trends over time.

  ``` dax
        PYTD Total Sales = CALCULATE(SUM(car_data[Price ($)]), SAMEPERIODLASTYEAR('CALENDAR TABLE'[Date]))
   ```

   **Difference between YTD Sales and Previous Year-to-Date (PTYD) Sales** : Difference between the current year's sales and it's previous year's sales. There was an 
     increement of **$70.8M** in sales in the current year compared to the previous year. 
     
  ``` dax
        Sales Difference = [YTD Total Sales] - [PYTD Total Sales]
   ```

   **Year-over-Year (YOY) Growth in Total Sales** : It refers to the **comparison** of total sales during a specific period in one year with the same period in the previous 
     year. This metric helps evaluate growth or decline in sales performance over time. There was a **23.59% growth** in sales in the current year compared to the previous 
     period.

  ``` dax
        YOY Sales Growth = [Sales Difference]/ [PYTD Total Sales]
   ```
<br>

   Similarly, I calculated all these metrics for Average price and number of Cars sold.

<br>

- **Average Price Analysis :**

    First, I calculated the average price.
  
  ``` dax
        Avg Price = SUM(car_data[Price ($)]) / COUNT(car_data[Car_id])
   ```

   **YTD Average Price** : YTD Average Price helps businesses track pricing trends, assess profitability, and compare pricing performance against previous years or periods. 
     The YTD average price is **$28.0K**.

  ``` dax
        YTD Avg Price = TOTALYTD([Avg Price], 'CALENDAR TABLE'[Date])
   ```
  
   **MTD Average Price** : The average price per car sold Month-to-Date, indicates how recent sales prices compare to the overall YTD prices. The MTD average price is  
   **$28.26K**    

  ``` dax
        MTD Avg Price = TOTALMTD([Avg Price], 'CALENDAR TABLE'[Date])
   ```

   **Previous-year-to-date (PYTD) Average price** : refers to the average selling price of products or services from the beginning of the previous year up to the same date 
     as the current year. 

  ``` dax
       PYTD Avg Price = CALCULATE([Avg Price], SAMEPERIODLASTYEAR('CALENDAR TABLE'[Date]))
   ```

   **Difference between YTD Average Price and PTYD Average Price** : There was a small decrease of **$0.22K** in average price in the current year compared to the previous 
     year.

  ``` dax
       Avg Price Diff = [YTD Avg Price] - [PYTD Avg Price]
   ```

   **YOY Growth in Average Price** : There was a **(-0.79%)** change in average price in the current year compared to the previous period.

  ``` dax
       YOY Avg Price Growth = [Avg Price Diff] / [PYTD Avg Price]
   ```

<br>

- **Cars Sold Metrics :**

   **YTD Cars Sold** : The total number of cars sold YTD was **13K**.

  ``` dax
       YTD Cars sold = TOTALYTD(COUNT(car_data[Car_id]), 'CALENDAR TABLE'[Date])
   ```

   **MTD Cars Sold** : This shows the number of cars sold in the current month that is **2K**, giving insights into monthly sales trends. 

  ``` dax
       MTD Cars sold = TOTALMTD(COUNT(car_data[Car_id]), 'CALENDAR TABLE'[Date])
   ```

   **Previous-year-to-date (PYTD) Cars sold** : Calculates the number of cars sold from the beginning of the previous year up to the same date as the current year. 

  ``` dax
       PYTD Cars sold = CALCULATE(COUNT(car_data[Car_id]) , SAMEPERIODLASTYEAR('CALENDAR TABLE'[Date]))
   ```

   **Difference between YTD Cars Sold and PTYD Cars Sold** : **3 thousand** more cars were sold in the current year compared to the previous year.

  ``` dax
       Cars sold Diff = [YTD Cars sold] - [PYTD Cars sold]
   ```

   **YOY Growth in Cars Sold** : a **24.57%** increase, demonstrates strong performance in sales volume.

  ``` dax
       YOY Cars sold Growth = [Cars sold Diff] / [PYTD Cars sold]
   ```





