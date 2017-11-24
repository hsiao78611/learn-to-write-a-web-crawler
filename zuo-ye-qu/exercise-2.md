# 2017-11-25 - 函式、模組、類別與套件

#### 在開始之前

##### \(1\) 請大家安裝個 Python IDE（看你想用哪一個，我是用 PyCharm），並且建立一個 Python 專案，如下：

* **repository\_name（資料夾**，專案名稱不限**）**

  * main.py
  * **crawl\_project（資料夾）**
    * \_\_init\_\_.py
    * crawler.py
    * df\_info.py
    * df\_upd.py

##### \(2\) 接著註冊一個 GitHub 帳號，然後將剛才新增的 Python 專案 push 至 GitHub 中，commit 內容自訂。

之後請大家撰寫的過程中，每到一個段落或更改，都將寫好的內容 push 上去。

（以上請 11/30 前完成）

##### 最後，完成程式的部分且確定抓下來的資料沒問題了，再將以下資料也一併 push 至 GitHub。

* data**（資料夾）**
  * info.csv
  * upd.csv

---

接下來程式的部分：（自行斟酌需要 import 的套件）

#### 首先，請實作一個套件，名為 crawl\_project

其中包含三個模組 **crawler.py**、**df\_info.py**、**df\_upd.py**：

* crawler.py 中是一個類別，名為 Campaign，即每個專案都是一個物件實例。 其中物件包含三個函式：

  * 屬性（\_\_init\_\_）：只有一個 專案的網址。

  * 方法（利用 exercise 1 中的作法）

    * get\_info\(self\)：取得 BeautifulSoup 解析過的 html，並將它與專案網址傳入 df\_info，即 df\_info\(proj\_url, proj\_soup\)，最後取得並回傳該 DataFrame。

    * get\_upd\(self\)：取得 BeautifulSoup 解析過的 html，並將它與專案網址傳入 df\_update，即 df\_upd\(proj\_url, upd\_soup\)，最後取得並回傳該 DataFrame。

* df\_info.py 與 df\_upd.py 中，分別針對 BeautifulSoup 解析過的 html 做搜尋，並存成一個 DataFrame 型態的資料，再回傳。其中 df\_info.py 要包含 專案網址、專案標題、目標金額、已達金額、人數及募資期限；df\_upd.py 要包含 專案網址、每個 update 的標題跟日期。

（[DataFrame](//171026_about_python.md#dataframe) 請自行參考哦！但不限這連結內的做法。）

#### 最後，實作一個主程式 main.py

import 剛才所建立的 crawl\_project。

任意找 10筆專案的連結，並集中存成一個 list。

在一個迴圈中，利用你所建立的類別去抓取那 10筆專案的資料，並且每抓一筆分別就存入 info.csv 及 upd.csv。

---

以下為 建立檔案目錄 及 DataFrame 存入 .csv 檔中的語法：

```py
import os

# create a directory
directory = os.getcwd() + '/' + 'data'
if not os.path.exists(directory):
    os.makedirs(directory)

def save(df, file_name):
    # if file does not exist
    if not os.path.isfile(directory + '/' + file_name): 
        df.to_csv(directory + '/' + file_name, index=False, encoding='utf-8-sig')

    # else it exists so append without writing the header
    else:  
        df.to_csv(directory + '/' + file_name, mode='a', index=False, header=False, encoding='utf-8-sig')
```



