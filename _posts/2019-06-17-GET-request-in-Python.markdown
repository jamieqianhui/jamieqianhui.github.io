---
layout: post
title:  "Create GET Request in Python"
date:   2019-06-17 09:55:36 +0800
categories: API 
---
Creating your **REST API GET Request** can be hassle-free and easy with Python! The entire process can be completed by following a 9-step guide. I constructed a GET request from URA's web API to fetch rental contract data in `.json` format and converted the dataset in `.csv` format for the ease of data load into the database. You can find the .py file stored in my [github repository][gitrepo] as well.

**Below is a 9-step guide (80-line code) on how I constructed the GET request in python to fetch data from URA's web API.**

{: class="table-of-content"}
* TOC
{:toc}

## 1. Register an account with URA to obtain your access key
Find out more here:
```python
https://www.ura.gov.sg/maps/api/#introduction
```

## 2.  Import the required libraries
```python
import json
import requests
import pandas as pd
```
These `import` statements load Python code that allow us to work with the data output in JSON format and the HTTP protocol. <br>

## 3. Set up the HTTP GET request to retrieve a daily token
A valid token needs to be generated to gain access to the data via URA's web API

```python
api_accesskey = 'Key in your access key'
api_url_base= 'https://www.ura.gov.sg/uraDataService/insertNewToken.action'

headers = {'Content-Type': 'application/json',
           'AccessKey': api_accesskey}

def get_token():

    response = requests.get(api_url_base, headers=headers)

    if response.status_code == 200:
        return json.loads(response.content.decode('utf-8'))
    else:
        return None
    
token_info = get_token()

if token_info is not None:
    print("Here's your token: "+'\n'+token_info['Result'])    
else:
    print('[!] Request Failed')
```


## 4. Determine the value of previous month based on Today's date to indicate the 'refPeriod' Parameter
The complete dataset of the previous month will only be published by the 15th day of this month. The API requires user to specify the parameter `reference period 'refPeriod'`. We will need to determine what is the previous month in qqYY format of the current period (e.g. 2Q19) based on today's date. If the current period is April (2Q19), then previous month would be March (1Q19) and we need to specify the `refperiod` for March as **1Q19**

```python
today = pd.to_datetime('today')
previous_month = today - pd.DateOffset(months=1)
period = previous_month.to_period('D').strftime('%Yq%q')
refperiod = period[-4:]
print(refperiod)
```

## 5. Send GET Request to retrieve data based on refPeriod
To retrieve a list of median rentals of private non-landed residential properties, send GET Request to URA API:
```python
api_url_base2= 'https://www.ura.gov.sg/uraDataService/invokeUraDS?service=PMI_Resi_Rental&'

headers2 = {'Content-Type': 'application/json',
           'AccessKey': api_accesskey,
           'Token': token_info['Result']}

params = {'refPeriod' : refperiod}

def get_data():

    response = requests.get(api_url_base2, params=params, headers=headers2)

    if response.status_code == 200:
        return json.loads(response.content.decode('utf-8'))
    else:
        return None
    
data_info = get_data()

if data_info is not None:
    print("Success! json dataset to convert to csv is embedded in data_info['Result']")   
else:
    print('[!] Request Failed')
```

## 6. Flatten nested data in json file
The data retrieved from URA's web API is in a nested json format. We will need to flatten the nested data using json_normalize.

```python
from pandas.io.json import json_normalize
data = data_info['Result']
flattendata = json_normalize(data,'rental',['project','street','y','x'],errors='ignore')
```

## 7.  Determine previous month value in 'mmYY' format then store as string 
We will need to convert previous month (mmYY format) to datetime format. Then extract mmYY value of previous month and store as leaseDate in string format.

```python
previousMMYY = previous_month.to_period('D').strftime('%m%Y')
leaseDate = previousMMYY[0:2]+previousMMYY[-2:]
print(leaseDate)
```
## 8. Get data for the latest month only from a quarterly-period dataset

```python
LatestMonthData = flattendata.loc[flattendata['leaseDate'] == leaseDate]
print(LatestMonthData)
```
## 9. Convert json data to .csv file, removing the index number

```python
LatestMonthData.to_csv('flatten_data_' + leaseDate +'.csv', index=False)
```

And it's completed! In 80-lines of python code! <br>
You can learn more about the basics of API from [here.][RESTful API]



[gitrepo]: https://github.com/jamieqianhui/URA_API_GETrequest
[RESTful API]: https://restful.io/an-introduction-to-api-s-cee90581ca1b
