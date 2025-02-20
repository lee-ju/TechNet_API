**Most Relevant Terms API to Python**
----
  Returns JSON data on that includes semantically most relevant terms to the queried term with Python

* **URL**

  /topn

* **Method:**

  `POST` 
  
*  **URL Params**

   **Required:**
 
   `userid=[string]` Any string is OK <br />
   `word=[string]`   Term to query

* **Data Params**

  None

* **Success Response:**

  * **Code:** 200 <br />
    **Content:** `{ word : [string], top20 : [(term1_string, rel1_string), ... , (termN_string, relN,string)] }`
    
    `termK_string : string of Kth top relevant term to query term` <br />
    `relN_string : string of relevance of KTh top relevant term to query term`
     
* **Error Response:**

  * **Code:** 200 <br />
    **Content:** `{ error : "xyz does not exist in database" }`

* **Sample Call:**

  ```javascript
$.ajax({
  url: http://52.221.86.148/api/ideation/concepts + '/topn',
  type: "POST",
  contentType: 'application/json',
  dataType: 'json',
  async: true,
  data: JSON.stringify({"userid":userid, "word": word}),
  success: function(response) {
    console.log(response);
  
    if (response['error']!=null){
      return (0)
    }
          topN = response['top20'];
  },
  error: function() {
    return (0)
  }
  });
  ```

* **Python:**

```python
import requests
import json

userid = 'anything'
word = 'QUERY_TERM' # ex. autonomous vehicle

data = {"userid": userid, "word": word}

try:
    response = requests.post(
                            "http://52.221.86.148/api/ideation/concepts/topn",
                            headers={"Content-Type": "application/json"},
                            data=json.dumps(data)
                            )

    # 응답 처리
    if response.status_code == 200:
        result = response.json()
        print(f'Success')

        # 오류 확인
        if "error" in result and result["error"] is not None:
            topN = 0
        else:
            topN = result.get("top20", 0)  # 'top20'이 없으면 기본값 0 설정
    else:
        topN = 0  # 오류 발생 시 0 반환

except requests.exceptions.RequestException as e:
    print(f"Request failed: {e}")
    topN = 0  # 요청 실패 시 0 반환
```
