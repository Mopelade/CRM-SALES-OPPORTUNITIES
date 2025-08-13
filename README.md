# CRM Sales Opportunity Analysis

## 🎯 Project Objective
This project aims to uncover insights from CRM sales data to answer the following key business questions:

1. **Sales Team Performance** – How does each team’s performance compare against others?  
2. **Sales Agent Gaps** – Are there agents consistently lagging in win rate, deal size, or closed revenue?  
3. **Quarter-over-Quarter Trends** – What patterns or shifts can be observed in performance over time?  
4. **Product Win Rate Leaders** – Which products achieve the highest win rates?  
5. **High-Value Products** – Which products generate the largest deal values?  
6. **Pipeline Bottlenecks** – Identify deals stuck too long in the *Engaging* or *Prospecting* stages.  
7. **Opportunity Aging** – Track average deal age per agent and per team to spot delays.  
8. **Top Customer Accounts** – Focus on the highest-revenue or highest-volume customers, analyzing:
   - Number of deals over time  
   - Products purchased  

---

## 📂 Data Source
- Dataset obtained from **Maven Analytics**
- Uploaded CSV files into a **Lakehouse** environment.
- Created a **Dataflow** for cleaning, transforming, and structuring the data for analysis.

---

## 🛠 Data Preparation Steps

### 1. Date Table Creation
To analyze time-based trends, a **custom Date Table** was created in Power Query.

**Step 1: Identify Date Range**
- Earliest engagement date:  
  ```powerquery
  List.Min(List.RemoveNulls(Source[engage_date]))
- Latest close date:
    ```powerquery
  List.Min(List.RemoveNulls(Source[engage_date]))
**Step 2: Generate Date List
  ```powerquery
List.Dates(
    StartDate, 
    Duration.Days(EndDate - StartDate) + 1, 
    #duration(1, 0, 0, 0)
)


Step 3: Convert List to Table
  ```powerquery
Table.FromList(DateList, Splitter.SplitByNothing(), {"Date"})

Step 4: Add Date Attributes
 ```powerquery
**YEAR
 Table.AddColumn(#"Changed column type with locale", "Year", each Date.Year([Date]), type nullable number)

**MONTH NAME:
Table.AddColumn(#"Inserted year", "Month name", each Date.MonthName([Date]), type nullable text)

**QUARTER-YEAR:
Table.AddColumn(#"Removed columns 2", "Quarter-Year", each Text.From(Date.Year([Date])) & "-" & "Qrt" & " " & Text.From(Date.QuarterOfYear([Date])), type text)

**DAY NAME:
Table.AddColumn(#"Inserted week of month", "Day name", each Date.DayOfWeekName([Date]), type nullable text)

