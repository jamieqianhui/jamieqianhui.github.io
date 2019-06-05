---
layout: post
title:  "Data Wrangling using Pandas"
date:   2019-06-04 13:24:36 +0800
categories: Python Pandas
---
Sharinga few simple tips on data wrangling using Python Pandas data frame!

I have stored the .py file code in my github repository too, you can find it here:
{% highlight html %}
https://github.com/jamieqianhui/URA_API_GETrequest
{% endhighlight %}

Below is a 9-step guide on how I constructed the GET request in python 

#### 1. Import the required python libraries

```python
import json
import requests
```
#### 2. Register an account with URA to obtain your access key 
#### 3. Send GET Request to retrieve daily token

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


#### 4. Determine the previous month of current period based on Today's date to enter 'refPeriod' Parameter

```python
import pandas as pd
today = pd.to_datetime('today')
previous_month = today - pd.DateOffset(months=1)
period = previous_month.to_period('D').strftime('%Yq%q')
refperiod = period[-4:]
print(refperiod)
```

#### 5. Send GET Request to retrieve a list of median rentals of private non-landed residential properties based on refPeriod

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

#### 6. Flatten nested data in json file

```python
from pandas.io.json import json_normalize
data = data_info['Result']
flattendata = json_normalize(data,'rental',['project','street','y','x'],errors='ignore')
```

#### 7. URA Publishes previous month's data; Determine previous month mmYY from period YYqq

```python
previousMMYY = previous_month.to_period('D').strftime('%m%Y')
leaseDate = previousMMYY[0:2]+previousMMYY[-2:]
print(leaseDate)
```
#### 8. Get data for the latest month only from a quarterly-period dataset

```python
LatestMonthData = flattendata.loc[flattendata['leaseDate'] == leaseDate]
print(LatestMonthData)
```
#### 9. Convert json data to .csv file, removing the index number

```python
LatestMonthData.to_csv('flatten_data_' + leaseDate +'.csv', index=False)

```

## And it's completed! In 80-lines of python code!

Check out the [Jekyll docs][jekyll-docs] for more info on how to get the most out of Jekyll. File all bugs/feature requests at [Jekyll’s GitHub repo][jekyll-gh]. If you have questions, you can ask them on [Jekyll Talk][jekyll-talk].

[jekyll-docs]: https://jekyllrb.com/docs/home
[jekyll-gh]:   https://github.com/jekyll/jekyll
[jekyll-talk]: https://talk.jekyllrb.com/
