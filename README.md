# Crypto-API

In this project I used import request to pull data from Coinmarket cap through their API, the data was pulled and then exported into a CSV. The data that was pulled was then visualized using Python visual library.

## Objectives
- To learn more about API and how it can be used get data from a website
- To learn how to import request to extract data
- To further advance my knowledge of visualization libraries in Python.
- To learn how to use define function in pulling out data from a website 

## Special codes in this project

```
  Python

from requests import Request, Session
from requests.exceptions import ConnectionError, Timeout, TooManyRedirects
import json
```

```
Python

def api_runner():

    global df
    
    url = 'https://pro-api.coinmarketcap.com./v1/cryptocurrency/listings/latest'
    parameters = {
      'start':'1',
      'limit':'20',
      'convert':'USD'
    }
    headers = {
      'Accepts': 'application/json',
      'X-CMC_PRO_API_KEY': '33c41d2e-a6ed-467c-8b37-a1c599d3492c',
    }

    session = Session()
    session.headers.update(headers)

    try:
      response = session.get(url, params=parameters)
      data = json.loads(response.text)
      print(data)
    except (ConnectionError, Timeout, TooManyRedirects) as e:
      print(e)
       
    
 

    df2 = pd.json_normalize(data['data'])
    df2['timestamp'] = pd.to_datetime('now')
    df = df.append(df2)
    
    if not os.path.isfile(r'C:\Users\akinl\Documents\Data Course\api.csv'):
        df.to_csv(r'C:\Users\akinl\Documents\Data Course\api.csv', header = 'column_names')
    else: 
         df.to_csv(r'C:\Users\akinl\Documents\Data Course\api.csv', mode = 'a', header = False)
```

