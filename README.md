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

The dataset used for this project was sourced from Kaggle and downloaded in Excel format. It spans the years **2022 and 2023** and contains **16 columns** and **23,906 rows**, a quick desripton of the data:

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

### DATA CLEANING

I initiated by checking the quality of the data, for which I used the **Column distribution** and **quality** feature in power query editor. There were no errors and empty values found. In the engine column I **replaced** the value (DoubleÂ Overhead Camshaft) with (Double Overhead Camshaft).

 <br>

---

 ### ANALYSIS

To address the key objectives of this project, I created KPI cards and visualization charts. These visuals offer a focused view of sales patterns, regional strengths, and customer preferences.

[**KPI CARDS**]

I used **DAX measures** to create these KPI cards, offering quick insights into key metrics like total sales, average price, and cars sold.

**1) Sales Overview :**

    Year-to-Date (YTD) Total Sales : 

    Month-to-Date (MTD) Total Sales :

    Year-over-Year (YOY) Growth in Total Sales :

    Difference between YTD Sales and Previous Year-to-Date (PTYD) Sales :


Average Price Analysis:

YTD Average Price
MTD Average Price
YOY Growth in Average Price
Difference between YTD Average Price and PTYD Average Price
Cars Sold Metrics:

YTD Cars Sold
MTD Cars Sold
YOY Growth in Cars Sold
Difference between YTD Cars Sold and PTYD Cars Sold

