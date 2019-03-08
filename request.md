# python  request 用法

對於這段code的解釋:
```
my_params = {'key1': 'value1', 'key2': 'value2'}

# 將查詢參數加入 GET 請求中
r = requests.get('http://httpbin.org/get', params = my_params)
```
<br/>
因為是使用get method,所以資料是直接接在網址後
而my_params為一個字典儲存者要request出去的資料

