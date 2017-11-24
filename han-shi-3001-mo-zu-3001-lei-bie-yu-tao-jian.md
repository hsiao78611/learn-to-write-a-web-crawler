# 函式、模組、類別與套件

請先參考：[Python 2 Tutorial 第二堂（3）函式、模組、類別與套件](https://openhome.cc/Gossip/CodeData/PythonTutorial/FunctionModuleClassPackage.html)

以下則是替大家簡述一下每個的使用方式：

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

---

# 套件（Package）



