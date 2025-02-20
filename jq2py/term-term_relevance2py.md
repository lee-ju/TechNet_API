**Term - Term Relevance API**
----
  Returns JSON data on the quantified relevance of two terms

* **URL**

  /similarity

* **Method:**

  `GET` 
  
*  **URL Params**

   **Required:**
 
   `key1=[string]&key2=[string]`

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{ similarity : [float] }`
 
* **Error Response:**

  * **Code:** 200 <br />
    **Content:** `{ error : "term not found" }`

* **JQ:**

  `http://52.221.86.148/api/ideation/concepts/similarity?key1=autonomous_vehicle&key2=blind_spot_detecting`

* **Python:**
```python
import requests

url = "http://52.221.86.148/api/ideation/concepts/similarity"
params = {
    'key1': 'QUERY_TERM1', # ex. autonomous_vehicle,
    'key2': 'QUERY_TERM2'  # ex. "blind_spot_detecting"
}

try:
    response = requests.get(url, params=params)
    if response.status_code == 200:
        result = response.json()
        print(f'Success')
    else:
        print(f"Error: {response.status_code}, {response.text}")

except requests.exceptions.RequestException as e:
    print(f"Request failed: {e}")
```
