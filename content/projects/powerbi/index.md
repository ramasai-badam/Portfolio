---
title: 'Unmasking L.A - PowerBI Dashboard'
cover:
    image: bicover.png
date: 2024-06-03
draft: false
---

<!-- <iframe src="https://app.powerbi.com/view?r=eyJrIjoiZWQyZmZkNmUtNGIxYy00MTk4LTg5MzQtMzVlZmQ4ZDY4ZWI3IiwidCI6IjA0NmZlY2JlLWI0Y2MtNDM3Zi05ODM2LTY0OTdjOTk1OWI5NSIsImMiOjJ9"></iframe> -->

Expand the dashboard for a detailed view

{{< powerbi "https://app.powerbi.com/view?r=eyJrIjoiZGJiMzBiMGItNWM2ZS00YWQ5LTllOWItNDk0ZmQ4YjRmN2EwIiwidCI6IjA0NmZlY2JlLWI0Y2MtNDM3Zi05ODM2LTY0OTdjOTk1OWI5NSIsImMiOjJ9" >}}

    data source : https://data.lacity.org/Public-Safety/Crime-Data-from-2020-to-Present/2nrs-mtv8/about_data
--------------------------------------------------------------------------------
## What steps did I take to integrate the data source? 

### Optimized Data Fetch with SoQL:

I created a Dataflow to act as a middleman between the LAPD's web API (SODA API) and my dashboard. But instead of grabbing everything, I used **SoQL filters** within the API call to snag only the columns I actually need for my analysis. This keeps the data transfer lean and minimizes the load on LAPD's servers.

### Data Wrangling in Power Query Editor:

I used Power Query Editor to clean and shape the data.

1. **Fixing Values**: The data was mostly clean and needed less imputation. But there were some values like -1, -2 for age which doesn't make sense. So, replaced them with 0s. 
2. **Creating New Columns**: I defined custom columns to categorize the data points. For example, I **binned** age into groups and time into Morning, Afternoon, Night, etc. making it easier to visualize and understand.

### Datalake as the Staging Area:

Initially, I tried using the Dataflow directly as the data source for my dashboard, but that didn't work out. So, I opted to store the transformed data from the Dataflow in a datalake. This datalake acts like a central storage unit for the prepared data, making it easily accessible for my dashboard.

### Connecting to Live Data in the Datalake:

I established a connection between my Power BI dashboard and the specific table containing the prepared data within the datalake. This connection uses a SQL endpoint with a data query. This way, I avoid importing the entire dataset into Power BI. Instead, my dashboard retrieves data directly from the datalake, ensuring it reflects the latest information available.

### Scheduled Refresh - Working with What I Have:

Power BI's built-in scheduling for dataflow refresh offers daily and weekly options. Ideally, I'd like the refresh to happen every two months to match LAPD's updates, but the closest option is weekly. To achieve the desired bi-monthly refresh cycle, I'm exploring Power Automate. Power Automate provides more flexibility, allowing me to trigger a dataflow refresh every two weeks. This keeps my dashboard data up-to-date without overwhelming LAPD's servers.

------------------------------------------------------------------------------------------

## Unsafe places in L.A

<iframe width="100%" height="500" name="iframe" src="https://hugoportfolio.s3.amazonaws.com/mapppu.html"></iframe>

## Safe places in L.A

<iframe width="100%" height="500" name="iframe" src="https://hugoportfolio.s3.amazonaws.com/safeplaces.html"></iframe>
