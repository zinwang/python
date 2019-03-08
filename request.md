# python  request 用法

對於這段code的解釋:
```
my_params = {'key1': 'value1', 'key2': 'value2'}

# 將查詢參數加入 GET 請求中
r = requests.get('http://httpbin.org/get', params = my_params)
```
<br/>
因為是使用get method,所以資料是直接接在網址後<br/>
我們想達成以下結果:

```
http://httpbin.org/get?key1=value1&key2=value2
#注意那個問號,看見問號就知道是get method,然後問號後面就是要傳送的資料
```

但不能直接就把上面這串網址拿去request,如果直接在瀏覽器網址欄貼上上面這串網址<br/>
當然行的通,可是在python不能這麼做,所以我們要透過requests.get()來幫我們達成:<br/>
<br/>
requests.get()需要兩個參數:<br/>
第一個參數是放網址,也就是問號前的那串網址,必須為字串<br/>
第二個參數是放要傳送的資料,也就是問號後的東西,必須為字典<br/>


而my_params為一個字典儲存者要request出去的資料,<br/>
key1與key2為http://httpbin.org/get 的get參數名稱,<br/>
value1與value2為你想送上去的數值°<br/><br/>

我再舉另外一個實例:<br/>

http://cowsay.morecode.org/

<br/>
這是我vcraw工具第六個選項彩蛋所爬取的網站,<br/>
這個網站有反爬機制,但這裡只是要解說requests使用方法<br/>
所以暫時當他沒有反爬機制

<br/>
這個網站基本上可以輸入文字，然後會產生一有趣的文字藝術<br/>

![](https://github.com/zinwang/python/blob/master/%E8%9E%A2%E5%B9%95%E6%93%B7%E5%8F%96%E7%95%AB%E9%9D%A2%20(209).png)

