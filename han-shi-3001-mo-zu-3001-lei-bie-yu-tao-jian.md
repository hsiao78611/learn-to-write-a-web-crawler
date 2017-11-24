# 函式、模組、類別與套件

請先參考：[Python 2 Tutorial 第二堂（3）函式、模組、類別與套件](https://openhome.cc/Gossip/CodeData/PythonTutorial/FunctionModuleClassPackage.html)

以下則是替大家簡述一下每個的使用方式：

---

# 函式（Function\)

當發現到兩個程式片段只有幾個變數不同時，就可以試著寫成一個函式，避免程式重複且冗長。

但建議在動手開始寫程式之前，若是先想好程序中有什麼固定的 pattern，你就能直接將它寫成一個函式。

寫法相當簡單，有回傳值（return value）的：

```py
def max(a, b):
    return a if a > b else b
```

沒有有回傳值的：

```py
def print_max(a, b):
    print('the maximum value is {}'.format(a if a > b else b))
    # https://docs.python.org/3/library/stdtypes.html#str.format
```

---

# 模組（Module）

當你發現有許多函式是在其他程式中也用得到的時候，就可以將功能相近的函式集中成一個模組。

而這在 Python 中也相當簡單，只要你新開一個 .py 檔，將這些函式放進去，該檔案就會是一個模組。

（模組中也可以是一個類別，下面會再介紹）

比如說：

```py
# 建立一個 comparison.py 檔（自訂的名稱即該模組的名稱）

def max(a, b):
    return a if a > b else b 

def min(a, b):
    return a if a < b else b
```

在其他檔案中就可以藉由 import、import as 與 from import 去使用你所建立的模組：

```py
# 任一個在同目錄下的 .py 檔

import comparison
print comparison.max(3, 9)

import comparison as cp
print cp.max(3, 9)

from comparison import max
print max(3, 9)
```

---

# 類別（Class）

類別是一個蠻重要的概念，因為當你的程式需要具有可讀性、可維護性及彈性的時候，就需要以物件導向的方式去撰寫。以下我們直接透過範例去了解。

假設今天模組中的功能是銀行存款、提款、餘額查詢的功能（如連結中給的範例）：

```py
# 每個帳號的狀態/屬性 儲存著資料
def account(name, number, balance):
    return {'name': name, 'number': number, 'balance': balance}
# 以下都是方法
def deposit(acct, amount):
    if amount <= 0:
         raise ValueError('amount must be positive')
    acct['balance'] += amount 

def withdraw(acct, amount):
    if amount > acct['balance']:
        raise RuntimeError('balance not enough')
    acct['balance'] -= amount

def to_str(acct):
    return 'Account:' + str(acct)
```

而使用的時候會發現每個人在使用時，即每個「實例」，其資料透過 account 儲存之後，都需要再一次傳遞給每個方法：

```py
import bank
acct = bank.account('Justin', '123-4567', 1000)
bank.deposit(acct, 500)
bank.withdraw(acct, 200)
print bank.to_str(acct)
```

因此，就如同在函式在部分，我們將重複的模式抽象化成一個通用的函式；在模組中，我們將功能相近的函式放在一起。我們也可以將儲存著資料的狀態/屬性，與方法結合在一起。

也就是從每個實例，即每個人使用這些銀行功能，找出彼此之間的共通點「帳戶」，而這帳戶也就是我們所說的「物件」，而這時候物件還是抽象的一個概念，所以我們需要建立一個「類別」去定義物件。

```py
# 類別，命名為 Account
class Account:
    # 每個帳號的狀態/屬性 儲存著資料
    def __init__(self, name, number, balance):
        self.name = name
        self.number = number
        self.balance = balance
    # 方法
    def deposit(self, amount):
        if amount <= 0:
             raise ValueError('amount must be positive')
        self.balance += amount

    def withdraw(self, amount):
        if amount > self.balance:
            raise RuntimeError('balance not enough')
        self.balance -= amount

    def __str__(self):
        return 'Account({0}, {1}, {2})'.format(
            self.name, self.number, self.balance)
```

在使用上，這裡一樣使用 import 一個名為 bank 的模組，但裡面已經不再是四個分散的函式，而是一個類別。

```py
import bank
acct = bank.Account('Justin', '123-4567', 1000)
acct.deposit(500)
acct.withdraw(200)
print acct
```

第二行，等號右邊的「bank.Account\('Justin', '123-4567', 1000\)」，可以稱之為一個（帳戶的）物件實例。然後該實例的位址再 assign 給 acct，透過它就可以對帳戶的狀態/屬性，直接以方法去進行動作。

#### 其他參考資料

* ##### 物件導向

  [http://antrash.pixnet.net/blog/post/65311153](http://antrash.pixnet.net/blog/post/65311153)

* ##### 類別（Java，不過概念一樣）

  [https://caterpillar.gitbooks.io/javase6tutorial/content/c7\_1.html](https://caterpillar.gitbooks.io/javase6tutorial/content/c7_1.html)

---

# 套件（Package）

這個就很簡單，

> 假設現在你有一些 .py 檔案，別人同樣也有一堆 .py 檔案，你們的檔案現在得放在同一專案中，那麼檔案名稱衝突是有可能發生的，最好是為你們的 .py 檔案分別開設目錄。使用 Python 時，你可以在開設的目錄中放個 **\_\_init\_\_.py **檔案，這樣 Python 就會將這個目錄視為一個套件，而目錄名稱就是套件名稱。



