# Sales-Dashboard

### Dashboard Link : [https://app.powerbi.com/groups/me/reports/384d017e-e935-44dc-9e7d-1626c1a36de1/ReportSection](https://app.powerbi.com/links/bOkeQ7x_KH?ctid=a82cd365-7c77-4f9c-a42c-3a8433f14fbe&pbi_source=linkShare&bookmarkGuid=d24cb0b4-9367-4da2-a863-0b191ad89743)

## Problem Statement

This dashboard enables management and stakeholders to monitor trends, track revenue, evaluate promotional performance, identify top-selling products, compare regional performance, and make timely decisions.

Using the dashboard, they can compare promotional and non-promotional sales, identify which promotion types generate the highest revenue, determine which products respond best to discounts, and understand how promotions influence overall profitability. These insights help guide the development of more effective promotional strategies.

Overall, sales were highest during the promotions held in April and May. From a day-of-week perspective, weekend sales outperformed other days. With this insight, future promotions can be planned more strategically, particularly by focusing more on weekends.


### Steps followed 

- Step 1 : Load data into Power BI Desktop, dataset is a csv file.
- Step 2 : Open power query editor & in view tab under Data preview section, check "column distribution", "column quality" & "column profile" options.
- Step 3 : Also since by default, profile will be opened only for 1000 rows so you need to select "column profiling based on entire dataset".
- Step 4: Performing data transformation for all 4 tables uploaded; Dim Customer, Dim Products, Dim Promotion and Fact table.
- Step 5: For Dim Promotion, we added conditional column which is percentage by promotion type for easier calculation purpose.
- Step 6 : For Fact Table, merging was performed on Product ID with Dim Product table, and then we remove unnecessary and duplicate columns. We also performed left outer join with Dim Promotion table on Promotion ID, rename the column and delete duplicate columns.
- Step 7: On Model View, the relationship between the table are created based on their respectively primary key and foreign key.
- Step 8 : Date table created using DAX, to ensure accurate relationship in visualization in report view. 

for creating Date table column following DAX expression was written;
       
    Date Table 3 = 
    ADDCOLUMNS(
        CALENDARAUTO(),
        "Year", YEAR([Date]),
        "Month", FORMAT([Date], "MMM"),
        "MonthNum", MONTH([Date]),
        "Day", FORMAT([Date],"DDD"),
        "DayNum", WEEKDAY([Date],2),
        "YearMonthDay", FORMAT([Date], "YYYY-MM-DD")
    )
Snap of new calculated column ,

![image alt](https://github.com/SyamimiNordin/Porfolio/blob/main/Date%20Table.png?raw=true)

- Step 9 : In the report view, under view tab, theme was selected.
- Step 10; Since, the data contains information on overall financial, product , and promtion, thus 3 different tab view added using bookmark, named "Financial Overview", "Product Overview" , and "Promotion Overview". 
- Step 11 :  On Financial Overview, another bookmark added which are Revenue and Profit, which available on the left side of the dashboard.
- Step 12 : Visual filters (Slicers) were added for Year and Month fields.
- Step 13 : To calculate MoM, QoQ, DAX are used to create new measure column. 
- Step 14 : On the left pane of dahsboard, two visual filter (Slicer) added for year and month. On the top pane of dashboard, 3 visual card added named "Revenue", "Profit", and "Units Sold".

Left Pane:

![image alt](https://github.com/SyamimiNordin/Porfolio/blob/main/Left%20Pane.png?raw=true)

Top Pane :
![image alt](https://github.com/SyamimiNordin/Porfolio/blob/main/Top%20Pane.png?raw=true)


- Step 15 : On Financial Overview tab, bar charts was added to represent Revenue and Profit Yearly, Monthly and Quaterly. Line chart also added to represent MoM(%) and QoQ(%).
- Step 16 : A bar Chart was added to represent Unit sold by monthly, while line graph was added to represent unit sold yearly and quaterly. Bar chart used for Monthly because it more detail and easier to compare between months, and for yearly and quaterly where the interval is more bigger, it more ideal to use line chart where we can show trend over time clearly. 
- Step 17 : Calculated column added under Dim Customer table to group them by Region.

For creating Region column following DAX expression was written;
       
    Region = 
    SWITCH(
        TRUE(),
        'Dim Customers'[State] IN {"Johor", "Melaka", "Negeri Sembilan"    "Selangor", "Kuala Lumpur", "Putrajaya"}, "Central/South",
        'Dim Customers'[State] IN {"Perak", "Penang", "Kedah", "Perlis"}, "North",
        'Dim Customers'[State] IN {"Kelantan", "Terengganu", "Pahang"}, "East Coast",
        'Dim Customers'[State] IN {"Sabah", "Sarawak", "Labuan"}, "East Malaysia",
        "Other"
    )

- Step 18 : Matrix table added to represent total sales, profit and units sold by region. Product table also added where we can see total sales and total profit for each product. 
- Step 19 :  To calculate total sales during promotion, new measure column added using DAX.

For creating new measure column following DAX expression was written;

    Promo Sales = 
    CALCULATE(
        [Sum of Net Sales],
        FILTER('Fact Table', 'Fact Table'[PromoFlag] = "Promo")
    )

- Step 19 : On Promotion Overview tab, line graph added to represent Monthly Sales Promo Trend and Daily Promo Trend. 
- Step 20 : On Promotion Overview tab, a clustered bar chart also added to represent total promo sales by promotion type. 
- Step 21: On Promotion Overview tab, a donut chart added to show Top Product sold during promotion. 
- Step 22 : 3 Visual card added for overview Promo Sales Performance on the bottom side: 

![image alt](https://github.com/SyamimiNordin/Porfolio/blob/main/Sales%20Performance%20Card.png?raw=true)
 
- Step 23 : The report was then published to Power BI Service.
 
![Publish_Message](https://user-images.githubusercontent.com/102996550/174094520-3a845196-97e6-4d44-8760-34a64abc3e77.jpg)

# Snapshot of Dashboard (Power BI Service)

![image alt](https://github.com/SyamimiNordin/Porfolio/blob/main/Dashboard%20Snapshot.png?raw=true)

 # Report Snapshot (Power BI DESKTOP)

![image alt](https://github.com/SyamimiNordin/Porfolio/blob/main/Report%20Snapshot.png?raw=true)

# Insights

A single page report was created on Power BI Desktop & it was then published to Power BI Service.

Following inferences can be drawn from the dashboard;

### [1] Total Revenue Overall = RM122 million

   Revenue for 2020 = RM31 million
   Revenue for 2021 = RM30 million
   Revenue for 2022 = RM29 million
   Revenue for 2023 = RM32 million
           
### [2] Total Profit Overall = RM12 million

   Profit for 2020 = RM31 million

   Profit for 2021 = RM30 million

   Profit for 2022 = RM29 million

   Profit for 2023 = RM32 million

### [3] Total Units Sold Overall = 

   Units Sold for 2020 = RM31 million

   Units Sold for 2021 = RM30 million
   
   Units Sold for 2022 = RM29 million
   
   Units Sold for 2023 = RM32 million


### [4] Top Product Sold

  4.1) Total Sales for Apple iPhone 14 is RM21.4 million
  
  4.2) Total Sales for Apple MacBook Air is RM19.6 million
  
  4.3) Total Sales for Sony Bravia 55" TV is RM19.4 million
  
  4.4) Total Sales for Samsung Galaxy S21 is RM15.3 million
 


 ### [5] Sales based on Region
 
 5.1) 38% sales coming from South Region.
 
 5.2) 25% sales coming from North Region.

 5.3) 18% sales coming from East Coast Region.

 5.4) 13% sales coming from East Malaysia Region.

 5.5) 6% sales coming from Others Region.
 
         thus, majority customers coming from South Region.

### [6] Promotion

6.1) During Summer Sales, RM17 million sales recorded.
6.2) Weekend Flash Sales, RM1.87 million sales recorded.
6.3) Clearance Sales, RM0.45 million sales recorded.

