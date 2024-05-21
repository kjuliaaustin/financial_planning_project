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

After integrating the Zillow API, I utilized it to access current listings of homes for sale in my city, Port Wentworth, GA. By specifying the location and status parameters in the API request, I retrieved a JSON response containing detailed information about available properties. This data included listing prices, property sizes, and other relevant details essential for my analysis. By normalizing the JSON response into a structured DataFrame using Pandas, I was able to easily explore and analyze the available listings, providing me with valuable insights into the current real estate market in my area.

```python
url = "https://zillow56.p.rapidapi.com/search"
querystring = {"location": "port wentworth, ga", "status":"forSale", "output": "json"}
headers = {
    "X-RapidAPI-Key": "private",
    "X-RapidAPI-Host": "zillow56.p.rapidapi.com"
}
response = requests.get(url, headers=headers, params=querystring)
data = response.json()
if 'results' in data:
	results = data['results']
else:
	results = []

# Normalize the JSON response to flatten it
df = pd.json_normalize(results)
```

This is what the table looked like:
|index|bathrooms|bedrooms|city|country|currency|daysOnZillow|homeStatus|homeStatusForHDP|homeType|imgSrc|isFeatured|isNonOwnerOccupied|isPreforeclosureAuction|isPremierBuilder|isShowcaseListing|isUnmappable|isZillowOwned|latitude|livingArea|longitude|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|0|3\.0|4\.0|Port Wentworth|USA|USD|0|FOR\_SALE|FOR\_SALE|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/bc3ce0c2bf44eabbf2f06ca4a43f7f4f-p\_e\.jpg|false|true|false|false|false|false|false|32\.225937|3141\.0|-81\.20441|
|1|1\.0|3\.0|Port Wentworth|USA|USD|0|FOR\_SALE|FOR\_SALE|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/a0a44a9aa2450c4898e3fbe4388c0571-p\_e\.jpg|false|true|false|false|false|false|false|32\.149986|935\.0|-81\.16613|
|2|2\.0|3\.0|Port Wentworth|USA|USD|1|FOR\_SALE|FOR\_SALE|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/2485b5a7b80a9dcb10525def630ec125-p\_e\.jpg|false|true|false|false|false|false|false|32\.1767|1618\.0|-81\.2025|
|3|2\.0|3\.0|Port Wentworth|USA|USD|1|FOR\_SALE|FOR\_SALE|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/25442c1d33374061d414ff8bd18cb129-p\_e\.jpg|false|true|false|false|false|false|false|32\.1767|1618\.0|-81\.2025|
|4|2\.0|3\.0|Port Wentworth|USA|USD|1|FOR\_SALE|FOR\_SALE|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/2485b5a7b80a9dcb10525def630ec125-p\_e\.jpg|false|true|false|false|false|false|false|32\.1767|1618\.0|-81\.2025|

### Homes Sold in My City

In addition to viewing homes for sale, I used the Zillow API to retrieve data on homes sold in my city, Port Wentworth, GA. By adjusting the API request parameters to specify the status as "sold," I was able to gather comprehensive information on recently sold properties.

|index|bathrooms|bedrooms|city|country|currency|dateSold|daysOnZillow|homeStatus|homeStatusForHDP|homeType|imgSrc|isFeatured|isNonOwnerOccupied|isPreforeclosureAuction|isPremierBuilder|isShowcaseListing|isUnmappable|isZillowOwned|latitude|livingArea|
|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|---|
|0|2\.0|3\.0|Port Wentworth|USA|USD|2024-05-17 07:00:00|4|RECENTLY\_SOLD|RECENTLY\_SOLD|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/f835bb28b38f533bddf9f3c9846f8485-p\_e\.jpg|false|true|false|false|false|false|false|32\.213425|1370\.0|
|1|3\.0|4\.0|Port Wentworth|USA|USD|2024-05-17 07:00:00|4|RECENTLY\_SOLD|RECENTLY\_SOLD|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/a9b4cbc93514a6c3eeb76f01bf3f30e2-p\_e\.jpg|false|true|false|false|false|false|false|32\.22756|1886\.0|
|2|3\.0|4\.0|Port Wentworth|USA|USD|2024-05-17 07:00:00|4|RECENTLY\_SOLD|RECENTLY\_SOLD|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/f18e20e3a346cbaae97e8aafe30b6fcd-p\_e\.jpg|false|true|false|false|false|false|false|32\.210194|2012\.0|
|3|1\.0|3\.0|Port Wentworth|USA|USD|2024-05-14 07:00:00|7|RECENTLY\_SOLD|RECENTLY\_SOLD|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/a632697e303935106a33cce8da3d8085-p\_e\.jpg|false|true|false|false|false|false|false|32\.14489|1220\.0|
|4|3\.0|3\.0|Port Wentworth|USA|USD|2024-05-09 07:00:00|12|RECENTLY\_SOLD|RECENTLY\_SOLD|SINGLE\_FAMILY|https://photos\.zillowstatic\.com/fp/f3784454bf402ab0d703f11d73f11daf-p\_e\.jpg|false|true|false|false|false|false|false|32\.187138|1930\.0|

## Financial Data Collection

To enhance my analysis, I developed a 'HomePurchase' class in Python to model and calculate various financial aspects of purchasing a home. This class is initialized with parameters such as home price, down payment percentage, interest rate, loan term in years, and closing costs percentage. It includes methods to calculate the down payment, loan amount, monthly mortgage payment, total interest paid over the loan term, and closing costs. Additionally, the class has a method to calculate the potential profit from selling the home, factoring in the selling price and agent costs percentage. This structured approach allows for a detailed and customizable evaluation of home purchasing and selling scenarios, enabling more accurate financial planning and decision-making.

```python
class HomePurchase:
    def __init__(self, home_price, down_payment_percent, interest_rate, loan_term_years, closing_costs_percent):
        self.home_price = home_price
        self.down_payment_percent = down_payment_percent
        self.interest_rate = interest_rate
        self.loan_term_years = loan_term_years
        self.closing_costs_percent = closing_costs_percent

    def calculate_down_payment(self):
        return self.home_price * (self.down_payment_percent / 100)

    def calculate_loan_amount(self):
        return self.home_price - self.calculate_down_payment()

    def calculate_monthly_payment(self):
        monthly_interest_rate = self.interest_rate / 100 / 12
        num_payments = self.loan_term_years * 12
        return (self.calculate_loan_amount() * monthly_interest_rate) / (1 - (1 + monthly_interest_rate) ** -num_payments)

    def calculate_total_interest(self):
        return (self.calculate_monthly_payment() * self.loan_term_years * 12) - self.calculate_loan_amount()

    def calculate_closing_costs(self):
        return self.home_price * (self.closing_costs_percent / 100)

    def calculate_profit(self, selling_price, agent_costs_percent):
        return selling_price - (self.home_price + self.calculate_closing_costs() + (selling_price * (selling_costs_percent / 100)))
```

Here is an example:
```python
home_price = 325000
down_payment_percent = 70
interest_rate = 6.5
loan_term_years = 15
closing_costs_percent = 2
selling_price = 325000
agent_costs_percent = 3

purchase = HomePurchase(home_price, down_payment_percent, interest_rate, loan_term_years, closing_costs_percent)

print(f"Down Payment: ${purchase.calculate_down_payment()}")
print(f"Loan Amount: ${purchase.calculate_loan_amount()}")
print(f"Monthly Mortgage Payment: ${purchase.calculate_monthly_payment():.2f}")
print(f"Total Interest Paid: ${purchase.calculate_total_interest():.2f}")
print(f"Closing Costs: ${purchase.calculate_closing_costs()}")
```

This code resulted in this output:
Down Payment: $227500.0
Loan Amount: $97500.0
Monthly Mortgage Payment: $849.33
Total Interest Paid: $55379.34
Closing Costs: $6500.0

I repeated this approach with the creation of a 'HomeSale' class to model and calculate various financial aspects of selling a home, including down payment, closing costs, agent costs, transfer taxes, and both federal and state capital gains taxes, ultimately determining the final profit and total sale amount.

```python
class HomeSale:
    def __init__(self, home_price, down_payment_percent, closing_costs_percent, transfer_tax):
        self.home_price = home_price
        self.down_payment_percent = down_payment_percent
        self.closing_costs_percent = closing_costs_percent
        self.transfer_tax = transfer_tax

    def calculate_down_payment(self):
        return self.home_price * (self.down_payment_percent / 100)

    def calculate_closing_costs(self):
        return self.home_price * (self.closing_costs_percent / 100)

    def calculate_agent_costs(self, agent_costs_percent):
        return self.home_price * (agent_costs_percent / 100)

    def calculate_transfer_tax(self, selling_price):
        return selling_price * (self.transfer_tax / 100)

    def calculate_profit(self, selling_price, agent_costs_percent):
        return selling_price - (self.home_price + self.calculate_closing_costs() + (selling_price * (agent_costs_percent / 100)))

    def calculate_capitalgains_federal(self, selling_price, agent_costs_percent):
        if self.calculate_profit(selling_price, agent_costs_percent) <= 63000:
          return self.calculate_profit(selling_price, agent_costs_percent) * (0/100)
        elif self.calculate_profit(selling_price, agent_costs_percent) > 63000 and self.calculate_profit(selling_price, agent_costs_percent) < 551351:
          return self.calculate_profit(selling_price, agent_costs_percent) * (15/100)
        else:
          return self.calculate_profit(selling_price, agent_costs_percent) * (20/100)

    def calculate_capitalgains_state(self, selling_price, agent_costs_percent):
        if self.calculate_profit(selling_price, agent_costs_percent) <= 750:
          return self.calculate_profit(selling_price, agent_costs_percent) * (1/100)
        elif self.calculate_profit(selling_price, agent_costs_percent) >= 1000 and self.calculate_profit(selling_price, agent_costs_percent) < 3000:
          return self.calculate_profit(selling_price, agent_costs_percent) * (2/100)
        elif self.calculate_profit(selling_price, agent_costs_percent) >= 3000 and self.calculate_profit(selling_price, agent_costs_percent) < 5000:
          return self.calculate_profit(selling_price, agent_costs_percent) * (3/100)
        elif self.calculate_profit(selling_price, agent_costs_percent) >= 5000 and self.calculate_profit(selling_price, agent_costs_percent) < 7000:
          return self.calculate_profit(selling_price, agent_costs_percent) * (4/100)
        elif self.calculate_profit(selling_price, agent_costs_percent) >= 7000 and self.calculate_profit(selling_price, agent_costs_percent) < 10000:
          return self.calculate_profit(selling_price, agent_costs_percent) * (5/100)
        else:
          return self.calculate_profit(selling_price, agent_costs_percent) * (5.75/100)

    def calculate_final_profit(self):
        return self.calculate_profit(selling_price, agent_costs_percent) - self.calculate_capitalgains_federal(selling_price, agent_costs_percent) - self.calculate_capitalgains_state(selling_price, agent_costs_percent) - self.calculate_transfer_tax(selling_price)

    def calculate_total_sale(self, selling_price, agent_costs_percent):
        return self.calculate_final_profit() + (self.home_price * (self.down_payment_percent / 100))
```

Here is an example:
```python
home_price = 193000
down_payment_percent = 100
closing_costs_percent = 2
selling_price = 230000
agent_costs_percent = 5
transfer_tax = .1

sale = HomeSale(home_price, down_payment_percent, closing_costs_percent, transfer_tax)

print(f"Home Price: ${home_price}")
print(f"Down Payment: ${sale.calculate_down_payment()}")
print(f"Selling Price: ${selling_price}")
print(f"Closing Costs: ${sale.calculate_closing_costs()}")
print(f"Agent Costs: ${sale.calculate_agent_costs(agent_costs_percent)}")
print(f"Profit before Tax: ${sale.calculate_profit(selling_price, agent_costs_percent)}")
print(f"Federal Taxes: ${sale.calculate_capitalgains_federal(selling_price, agent_costs_percent)}")
print(f"State Taxes: ${sale.calculate_capitalgains_state(selling_price, agent_costs_percent)}")
print(f"Transfer Tax: ${sale.calculate_transfer_tax(selling_price)}")
print(f"Profit after Tax: ${sale.calculate_final_profit()}")
print(f"Total Sale: ${sale.calculate_total_sale(selling_price, agent_costs_percent)}")
```

And the resulting output:
Home Price: $193000
Down Payment: $193000.0
Selling Price: $230000
Closing Costs: $3860.0
Agent Costs: $9650.0
Profit before Tax: $21640.0
Federal Taxes: $0.0
State Taxes: $1244.3
Transfer Tax: $230.0
Profit after Tax: $20165.7
**Total Sale**: $213165.7
