# Home Sale Analysis and Financial Planning Project
## Scope and Objectives
**Scope**: Analyze home sale trends, determine the worth of current home, and understand the financial aspects of selling and purchasing a home.
**Objectives:**
- Determine the current market value of my home.
- Analyze trends in home sales in Chatham County and Effingham County.
- Understand the costs associated with selling my home and purchasing a new one.
- Evaluate potential investment returns from my home sale and new purchase.

## Real Estate Data Collection
### County Homes Sold (Chatham & Effingham)
For this project, I accessed public records for homes sales in both Chatham County and Effingham County, spanning a period of 2 1/2 years. Using this data, I meticulously compiled and merged the information into separate CSV files for each county. By combining the data from both counties, I aimed to conduct a thorough analysis of home sale trends and market conditions in the region.

Effingham County Homes Sold 2022:
|index|Parcel ID|Address|Sale Date|Sale Price|Qualified Sales|Reason|Acres|Parcel  Class |Year  Built |Square Ft |Price Per  Square Ft |Neighborhood|Delinquent Years|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|0|0351A007A00|115 BRETTS CT|1/31/2022|$340,000\.00|Qualified|FM|0\.51|Residential|2022\.0|2660\.0|$127\.82|0351A: LAND: 00000/BLDG: 00001 PHS II LOTS 1A-19A|NaN|
|1|R2600041|209 SANDY SPRINGS DR|1/10/2022|$0\.00|Unqualified|U|0\.38|Residential|2018\.0|3024\.0|$0\.00|R2600: LAND: 00000 / BLDG: 00110|NaN|
|2|04280001A00|743 LOG LANDING RD|1/26/2022|$0\.00|Unqualified|U|3\.04|Residential|NaN|NaN|$0\.00|04280: LAND: 00000 / BLDG: 00000|NaN|
|3|R2590038|522 WINDSONG DR|1/5/2022|$0\.00|Unqualified|Y|0\.19|Residential|2010\.0|2981\.0|$0\.00|R2590: LAND: 00001/ BLDG: 000090 2 STY HOUSE|NaN|
|4|0428C267|108 SAND PINE CT|1/27/2022|$172,500\.00|Qualified|FM|0\.29|Residential|2008\.0|1171\.0|$147\.31|0428C: LAND: 00000 / BLDG: 000110|NaN|

### My Home Zestimate History

Following the compilation of public records, I integrated the Zillow API to access and analyze the historical Zestimate values for my home. By leveraging the API, I obtained a detailed history of Zestimate values over time, allowing me to track fluctuations and trends in my home's estimated worth. This data provided valuable insights into the market dynamics affecting my property's value, enabling me to make informed decisions regarding its potential sale. Combining the Zestimate history with the broader home sales data from Chatham and Effingham Counties enriched my analysis, providing a comprehensive view of the real estate landscape in the area.

|index|date|timestamp|value|
|---|---|---|---|
|0|2014-05|2014-05-31 07:00:00|119700|
|1|2014-06|2014-06-30 07:00:00|118063|
|2|2014-07|2014-07-31 07:00:00|119845|
|3|2014-08|2014-08-31 07:00:00|114984|
|4|2014-09|2014-09-30 07:00:00|112420|

### Homes for Sale in My City


### Homes Sold in My City


## Financial Data Collection
