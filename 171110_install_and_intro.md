# 安裝環境

一開始會需要安裝 Python2, Python3, Jupyter \(互動式的筆記本系統\)

會安裝兩種版本的 Python 是因為我爬蟲是用 Python2 寫的，主要是怕有些套件還不支援 Python3。

但 Python3 越來越多人使用，大部分套件都有支援了，所以或許你們可以用 Python3 寫看看。

Jupyter 則是一個可以透過瀏覽器進行程式的開發與維護的工具。

因為可以在其中穿插文字的單元，所以無論是練習寫 Python 或是進行資料分析都很方便。

Homebrew 是一個 Mac 使用的套件管理工具，可以在自訂的目錄下安裝 Python2、Python3 及各種套件。Windows 因為沒有內建 Python，所以不用擔心動到電腦裡原來的 Python 環境，所以好像沒有人在用套件管理工具，聽過的大概就是 Anaconda。

#### 參考網址：

##### Python玩數據 \(1\)：安裝Python, IPython, Numpy, Pandas

[http://www.ycc.idv.tw/YCNote/post/18](http://www.ycc.idv.tw/YCNote/post/18)

##### MAC OSX 正確地同時安裝 PYTHON 2.7 和 PYTHON3

[https://stringpiggy.hpd.io/mac-osx-python3-dual-install/](https://stringpiggy.hpd.io/mac-osx-python3-dual-install/)

##### \[Python\] Mac OS / Windows 安裝 Jupyter

[https://oranwind.org/bid-data-mac-os-an-zhuang-jupyter/](https://oranwind.org/bid-data-mac-os-an-zhuang-jupyter/)

---

# 什麼是網路爬蟲?

[http://www.largitdata.com/course/1/](http://www.largitdata.com/course/1/)

這網站每個影片（至少我看的前面幾個）都只有 3~4 分鐘，講得蠻簡單易懂的。

爬蟲其實就是把網頁上的內容抓下來而已。

看到「如何使用Python 套件: BeautifulSoup4 剖析網頁內容?」就能寫出一個爬蟲了。

之後就是設計一個完整的程序去進行：1, 抓資料；2. 填入自己安排好的 dataframe；3. 儲存/輸出。

只是在這過程中可能會遇到一些障礙，比如說網頁內容是由 javascript 產生的、該網站有防止爬蟲的機制或規則，以及如何在多執行緒下同時進行資料爬取的動作...等等。

