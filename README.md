## Wikipedia Traffic Data: 2008  - 2021
### Project Goal
The goal of this projcet is to construct, analyze, and publish a dataset of monthly traffic on English Wikipedia from January 1 2008 through August 30 2021

[Link to the problem statement](https://docs.google.com/document/d/1groRZyhgOwBxlSyE4vKEhYa-khKet8iWVaVDAgOH_Y4/edit?usp=sharing) 

## Data Source
In order to measure Wikipedia traffic from 2008-2021, we need to collect data from two different API endpoints, the Legacy Pagecounts API and the Pageviews API.
The Legacy Pagecounts API (documentation, endpoint) provides access to desktop and mobile traffic data from December 2007 through July 2016.
[Documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Legacy_Pagecounts) 
[Endpoint](https://wikimedia.org/api/rest_v1/#/Pagecounts_data_(legacy)/get_metrics_legacy_pagecounts_aggregate_project_access_site_granularity_start_end)

The Pageviews API (documentation, endpoint) provides access to desktop, mobile web, and mobile app traffic data from July 2015 through last month
[Documentation](https://wikitech.wikimedia.org/wiki/Analytics/AQS/Pageviews) 
[Endpoint](https://wikimedia.org/api/rest_v1/#/Pageviews_data/get_metrics_pageviews_aggregate_project_access_agent_granularity_start_end)


## Data acquisition:
All the  data we retrieved using REST APIs are stored in json format with the below file names: 

#### Retrieved using Pagecounts API.(DEC 2007 - Jul 2016)
- pagecounts_desktop-site_200712-201607.json  : Counts from the  desktop-site  version. 
- pagecounts_mobile-site_200712-201607.json   : Counts from the mobile-site version. 
#### Retrieved using Pageview API. (Jul 2015 - Sept 2021)
- pageviews_desktop_201507-202109.json        : Counts from the desktop  version.
- pageviews_mobile-app_201507-202109.json     : Counts from the mobile-app version.
- pageviews_mobile-web_201507-202109.json     : Counts from the mobile-web version.

##### Data processing:
The data files which we colledted need to be processed and store as 'en-wikipedia_traffic_200712-202108.csv' file
Combine all data into a single CSV file with the following headers:


Column | Value | Description |
| ------------- |:-------------:| -----|
year | YYYY | Year corresponding to the data.(2008-2021)|
month | MM | Month corresponding to the data.(2008-2021)|
pagecount_all_views | num_views | Total views retrieved from Pagecount API. |
pagecount_desktop_views | num_views | Desktop  views retrieved from Pagecount API. |
pagecount_mobile_views | num_views | Mobile  page views retrieved from Pagecount API. |
pageview_all_views | num_views | Total  views retrieved from Pageview API. |
pageview_desktop_views | num_views |  Desktop  page views retrieved from Pageview API. |
pageview_mobile_views | num_views |  Mobile  (Web + App) page views retrieved from Pageview API. |

The raw data json files are stored in the `raw_data` folder, the final processed data is tored in 'Final_clean-data' folder

## Code
All the code involved in this project is written in a `Jupyter notebook` : `hcds-a1-data-curation.ipynb`.

The notebook has three steps in the project:
- Data Acquisition: Which Covers the portion of acquiring the data from REST APIs and saving the raw data into json files. 
- Data Processing: Which includes processing the dtaa nd combining all the data into asingle csv file
- Analysis: Involves exploring the data,  plotting the time series graphs and saving the plot to .png file

The following packages are needed to run:
- datetime
- json
- matplotlib
- os
- pandas
- requests

The final result is saved as a .png file which also has been published here as : `wiki_traffic_views_2008_2021.png`

## Known Issues
- The values of pagecount_mobile_views for months before October 2014 should be 0, because mobile traffic data is not available before that month.
- The Pageview API filters out automated (bot) traffic, whereas the PageCount API does not.

## License
The code is licensed under [MIT](LICENSE).

