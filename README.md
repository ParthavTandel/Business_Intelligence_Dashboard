# Business_Intelligence_Dashboard
BI Dashboard created in Power BI using Power BI Desktop and Power Query.

<img width="912" alt="Dashboard_SS" src="https://user-images.githubusercontent.com/118220804/223491796-1b0d970c-c0c8-4b06-8ec4-f99560df9a5c.png">

Did star schema data modelling in Power Query. Created custom Dim_Date table.

Created Current YTD and Previous YTD measures for Profit, Revenue and Quantity,

YTD Profit = CALCULATE([Total Profit],DATESYTD(Dim_Date[Date]))

Previous YTD Profit = COALESCE(CALCULATE([YTD Profit], SAMEPERIODLASTYEAR(Dim_Date[Date])), 0)

Top selling Product sales = 
  VAR Ranking = VALUES(Dim_Product[prod_name]) 
  RETURN 
  CALCULATE([Total Revenue], TOPN(1, ALL(Dim_Product[prod_name]), [Total Revenue]), Ranking)
  
Share of Top Selling Product = DIVIDE([Top selling Product sales], CALCULATE([Total Revenue], REMOVEFILTERS(Dim_Product)), 0)

Rolling 4 month avg Sales = 
  CALCULATE(AVERAGEX(VALUES(Dim_Date[Month]), [Total Revenue]), DATESINPERIOD(Dim_Date[Date], MAX(Dim_Date[Date]), -4, MONTH))


