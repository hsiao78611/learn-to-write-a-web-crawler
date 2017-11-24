# 前言

我不是老師，這也不是一堂課，所以不會有人打分數。  
但還是希望在這一學期結束前，~~我能準時畢業~~，大家能學會寫出自己的爬蟲！  
不過我重點是放在「做出爬蟲」，所以 Python 就請各位自學了...

個人認為 Codecademy + 良葛格的學習筆記 + Google & StackOverflow 就很足夠。  
由於當初在為論文爬資料時，並沒有想到 Jack 會要我教大家怎麼寫爬蟲，  
所以我寫爬蟲的過程、爬文後的筆記、清楚的程式註解，通通都沒有~

只能請大家自行到我 [GitHub](https://github.com/hsiao78611/Data4Paper) 上參考我是怎麼寫的。（或[這位大大寫的教學](https://github.com/leVirve/CrawlerTutorial)，我覺得超棒的。）  
在我的檔案當中：

* crawl\_ 開頭的，都是各個爬蟲的主程式，大概只負責紀錄、輸入、輸出。
* packages 下：
  * utils 放的大多比較像是工具的東西，很多是從其他人那複製及修改的。
  * explore 爬 KS 上全部成功專案的連結。  
    （df 表示 DataFrame，input 是 BS 解析過的 html；output 是一個 DataFrame 形態的表格）
  * creator 爬募資人的 about、created、backed。  
    （comments 沒有用到，錯誤應該很多）
  * individuals 爬個別專案的 project（主頁）、rewards、faqs、updates、comments。  
    （其中有兩個 crawler，upd 開頭的抓的是個別 update 的內容，因為比較單純就沒有另外開個 df 開頭的檔案）

我是有做出可以透過 Tor 去偽裝成其他 IP，但有時候會比較慢，或中斷。  
結果 Kickstarter 好像也沒在管，之後抓我都關掉沒用了...

另外，為了能夠同時抓上萬筆專案的資料，尤其是資助者留言的部分，  
所以我也有利用 multiprocessing，實現最多同時 8 組 crawler 在跑，  
但我也是東湊西湊出來的就是了... 畢竟有時間壓力嘛~

