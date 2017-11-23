# 2017-11-10

> 19號前請學弟們交個小作業：首先在自己電腦上安裝好環境，  
> 然後在 Jupyter 上，用 requests 和 Beatifulsoup 抓 kickstarter 上任一個專案中的  
> 標題, 募資目標金額, 已達金額, 人數, 募資期限\(funding period\)。  
> 先不用作字串處理，只要找到該欄位的值，再 print 出來就好。



首先，抱歉，我沒注意到他影片中用的是 select，這叫 CSS 選擇器。  
顧名思義，這是利用 CSS 去尋找在那樣式下的所有 html 內容。  
但前提是對該網頁的 CSS 要很熟悉，知道哪些 class 和 id 下就有你要的資料。

其實尋找頁面指定內容的方法還能利用 Xpath（類似指定一個絕對路徑）,  
或一樣在 BeautifulSoup 下的 find 和 find\_all。  
而這次練習若是用 find 和 find\_all 就可以很快抓到想要的值了。

不過用 select 還是可以抓得到啦！  
可參考：[https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html\#id37](https://www.crummy.com/software/BeautifulSoup/bs4/doc/index.zh.html#id37)

```py
import requests
from bs4 import BeautifulSoup
```

```py
res = requests.get('https://www.kickstarter.com/projects/' + \
                   '1602345155/deiland-rpg-adventure-and-sandbox-game-in-a-little?ref=home_recommended')
soup = BeautifulSoup(res.text, "lxml")
```

---

# 標題

```python
soup.select('head > title')[0].text
```

> 'Deiland - RPG, adventure and sandbox game in a little planet by Chibig —Kickstarter'



或想用其他方法。

首先找到 title:

```html
<title>
Deiland - RPG, adventure and sandbox game in a little planet by Chibig — 
Kickstarter
</title>
```

Google: python beautifulsoup how to get title  
[https://stackoverflow.com/questions/28875799/extract-title-tag-with-beautifulsoup](https://stackoverflow.com/questions/28875799/extract-title-tag-with-beautifulsoup)

可以知道還有 find 這個方法~  
但是他還包含著 html 標籤

```python
soup.find('title')
```

&lt;title&gt;Deiland - RPG, adventure and sandbox game in a little planet by Chibig —Kickstarter&lt;/title&gt;



Google: python remove html tag  
[https://stackoverflow.com/questions/9662346/python-code-to-remove-html-tags-from-a-string](https://stackoverflow.com/questions/9662346/python-code-to-remove-html-tags-from-a-string)

知道 BeautifulSoup 裏有 text 方法可以去除 html 的標籤

```python
soup.find('title').text
```

> 'Deiland - RPG, adventure and sandbox game in a little planet by Chibig —Kickstarter'



output 出來帶有單引號「'」，表示回傳（return）的值是一個字串（string\)；  
而由於 jupyter 可以將程式碼隱藏，只顯示其他圖文內容，因此需要用 print 這方法讓結果出現在前端。

```python
print(soup.find('title').text) # 執行後沒有出現 Out[] 的 cell
```

> Deiland - RPG, adventure and sandbox game in a little planet by Chibig —Kickstarter



##### 題外話，若要在一個 cell 內顯示多筆結果，可能的方法就只有：

* 更改 jupyter 的設定
* 使用 print
* 用不同 cell

```python
import time
print('print 1')
'output 1'
time.sleep(5)
print('print 2')
'output 2'
```

> print 1
>
> print 2
>
> 'output 2'



---

# 募資目標金額

```html
<span class="money">$10,000</span>
```

```python
soup.select('.money')
```

> \[&lt;span class="money usd project\_currency\_code"&gt;&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$10,000&lt;/span&gt;,
>
>  &lt;span class="money usd project\_currency\_code"&gt;&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$10,000&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$15&lt;/span&gt;,
>
>  &lt;span class="money"&gt;US$ 25&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$30&lt;/span&gt;,
>
>  &lt;span class="money"&gt;US$ 40&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$60&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$100&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$650&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$12&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$20&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$180&lt;/span&gt;,
>
>  &lt;span class="money"&gt;$250&lt;/span&gt;\]



```html
<span class="block navy-600 type-12 type-14-md lh3-lg">
pledged of <span class="money">$10,000</span> <span class="mobile-hide">goal</span>
</span>
```

#### span 同時具有多個 class...

Google: beautifulsoup select multiple class  
[https://stackoverflow.com/questions/40305678/beautifulsoup-multiple-class-selector](https://stackoverflow.com/questions/40305678/beautifulsoup-multiple-class-selector)

```python
soup.select('.block.navy-600.type-12.type-14-md.lh3-lg')[0].text
```

> '\npledged of $10,000 goal\n'



但是換行的符號（\n）還在，想要去掉它，於是...

Google: python beautifulsoup remove new line tab  
[https://stackoverflow.com/questions/9662346/python-code-to-remove-html-tags-from-a-string](https://stackoverflow.com/questions/9662346/python-code-to-remove-html-tags-from-a-string)  
發現有個 strip\(\) 方法~

```python
soup.select('.block.navy-600.type-12.type-14-md.lh3-lg')[0].text.strip()
```

> 'pledged of $10,000 goal'



---

# 已達金額

```python
soup.select('.block.green-700.js-pledged.medium.type-16.type-24-md')[0].text.strip()
```

> 'US$ 16,634'



---

# 人數

```python
soup.select('div.ml5.ml0-lg.mb2-lg')[0].text.strip()
```

> '761\n\nbackers'



中間卡著 \n\n 沒辦法藉由 strip\(\) 處理...  
其實我只想讓各位抓數字就好了，因為通常也只會需要數字。  
但既然遇到就來把它替換掉。

```python
soup.select('div.ml5.ml0-lg.mb2-lg')[0].text.strip().replace('\n\n', ' ')
```

> '761 backers'



---

# 募資期限

```python
soup.select('p > time')[0].text.strip()
```

> 'Thu, Dec 7 2017 5:59 pm EST'



6:59 AM \(6:59\) AWST = 5:59 PM \(17:59\) Previous Day EST

網頁可能透過 JavaScript，將時間轉換成瀏覽器所在位置的時區。  
所以我們看到的都是 AWST



---

# 補充

有些人會出現以下的警告，這表示你沒有明確指定一個 html 解析器，而這會使得你的程式碼在不同環境下，會使用不同的解析器。  
解析器的種類與優缺請參考：[https://www.crummy.com/software/BeautifulSoup/bs4/doc/\#installing-a-parser](https://www.crummy.com/software/BeautifulSoup/bs4/doc/#installing-a-parser)  
在這份文件中是推薦使用 lxml ，即 BeautifulSoup\(YOUR\_MARKUP, "lxml"\)，因為它速度比較快。

```python
import requests
from bs4 import BeautifulSoup
res = requests.get("https://www.kickstarter.com/projects/...")
Soup = BeautifulSoup(res.text)
```

```
/usr/local/lib/python3.6/site-packages/bs4/__init__.py:181: UserWarning: No parser was explicitly specified, so I'm using the best available HTML parser for this system ("lxml"). This usually isn't a problem, but if you run this code on another system, or in a different virtual environment, it may use a different parser and behave differently.

The code that caused this warning is on line 193 of the file /usr/local/Cellar/python3/3.6.1/Frameworks/Python.framework/Versions/3.6/lib/python3.6/runpy.py. To get rid of this warning, change code that looks like this:

 BeautifulSoup(YOUR_MARKUP})

to this:

 BeautifulSoup(YOUR_MARKUP, "lxml")

  markup_type=markup_type))
```



