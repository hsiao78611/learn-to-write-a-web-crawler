# Computational Thinking 計算思維

開始之前，先來看段影片吧：

```
<iframe width="560" height="315" src="//https://www.youtube.com/watch?v=ApvNdzyvGFA" frameborder="0" allowfullscreen></iframe>
```

[https://www.youtube.com/watch?v=ApvNdzyvGFA](https://www.youtube.com/watch?v=ApvNdzyvGFA)

[https://computationalthinkingcourse.withgoogle.com/unit?lesson=8&unit=1](https://computationalthinkingcourse.withgoogle.com/unit?lesson=8&unit=1)

> Computational Thinking \(CT\) is a problem solving process that includes a number of characteristics and dispositions. CT is essential to the development of computer applications, but **it can also be used to support problem solving across all disciplines**, including the humanities, math, and science. Students who learn CT across the curriculum can begin to see a relationship between academic subjects, as well as between life inside and outside of the classroom.

#### The elements of CT, including:

* Decomposition: Breaking down data, processes, or problems into smaller, manageable parts
* Pattern Recognition: Observing patterns, trends, and regularities in data
* Abstraction: Identifying the general principles that generate these patterns
* Algorithm Design: Developing the step by step instructions for solving this and similar problems

Decomposition 原則上就和字面上的解釋差不多，將大的問題拆成數個小問題，並且透過解決這些小問題，進而解答一開始的大問題。接著在拆解問題的過程中，我們會發現常常重複進行著「拆成數個小問題」的動作，而這樣的規律就是所謂的 Pattern（模式）。接著透過觀察模式的運作，我們可以再將這運作過程抽象化（Abstract）成一個數學公式、或者其他可以表示這 Pattern 是如何形成的方法。最後，將上述的數學公式或方法，轉換成依步驟進行的程序，就會形成所謂的演算法（Algorithm）。

# Divide and Conquer（分而治之）

這個觀念正好與運算思維中的 Decomposition 相呼應。

**Wikipedia:**

> 把一個複雜的問題分成兩個或更多的相同或相似的子問題，直到最後子問題可以簡單的直接求解，原問題的解即子問題的解的合併。

[https://www.khanacademy.org/computing/computer-science/algorithms/merge-sort/a/divide-and-conquer-algorithms](https://www.khanacademy.org/computing/computer-science/algorithms/merge-sort/a/divide-and-conquer-algorithms)

> You should think of a divide-and-conquer algorithm as having three parts:
>
> * Divide the problem into a number of subproblems that are smaller instances of the same problem.
> * Conquer the subproblems by solving them recursively. If they are small enough, solve the subproblems as base cases.
> * Combine the solutions to the subproblems into the solution for the original problem.

其中 recursively 是實現 divide-and-conquer 常常會用到的方法。

# Recursion（遞迴）＆Iterative（迭代）

其中在抽象化的過程中，我們要考慮實現 Pattern 時，重複的步驟是要以「遞迴」還是「迭代」的方式去進行。

**Wikipedia:**

> * 遞迴：在數學與電腦科學中，是指在函式的定義中使用函式自身的方法。 
> * 迭代：是重複反饋過程的活動，其目的通常是為了接近併到達所需的目標或結果。每一次對過程的重複被稱為一次「迭代」，而每一次迭代得到的結果會被用來作為下一次迭代的初始值。

其中遞迴最典型的例子就是「費氏數列」：  
[https://openhome.cc/Gossip/AlgorithmGossip/FibonacciNumber.htm](https://openhome.cc/Gossip/AlgorithmGossip/FibonacciNumber.htm)

而一般我們所知的 for、while 迴圈，則都屬於屬於迭代。  
[https://zh.wikipedia.org/wiki/迭代](https://zh.wikipedia.org/wiki/迭代)

網路上還有很多關於遞迴的討論，一般來說，以遞迴的方式實現的程式碼會比較精簡，可讀性也比較高。但像費氏數列那樣子的計算方式，常常會發生重複計算的情況，因此當數字很大的時候，運算速度就會變得非常慢（因為花很多時間在堆疊和呼叫上）。

這裡並不是說遞迴就是不好，而是要提醒大家在寫程式的時候要稍微注意一下程式執行的效率。

### 其他參考資料

#### 演算法也有不神祕的一面（下集）

[https://school.soft-arch.net/blog/154515/on-algorithm-myth](https://school.soft-arch.net/blog/154515/on-algorithm-myth)

#### 遞迴的美麗與哀愁 遞迴本質上是將複雜問題單純化

[https://www.ithome.com.tw/node/81087](https://www.ithome.com.tw/node/81087)

# pseudocode 虛擬碼

既然提到計算思維了，就不得不提一下 pseudocode。因為一開始寫程式常常腦中已經有想法、有概念，但突然要寫出來就腦袋一片空白。這是因為我們都習慣用自己熟悉的語言去思考，例如要實現 1+1==2，腦中想的是一加一等於二，但對電腦來說可能是 Equals\(Plus\(1,1\)\)，也就是 Plus 這函數有兩個參數分別為一，而這又是 Equals 這函數的參數。...嗯，總之，在我們動手寫程式前，建議可以先寫 pseudocode，不論形式為何（中英夾雜、畫圖、畫箭頭），先在紙上以運算思維的方式想清楚了每一個步驟要做什麼，最後你的 algorithm 長得怎麼樣，再來開始將這些步驟寫成程式。

[https://zh.wikipedia.org/wiki/伪代码](https://zh.wikipedia.org/wiki/伪代码)

> 我們可以將整個演算法執行過程的結構用接近自然語言的形式（這裡可以使用任何一種作者熟悉的文字，例如中文、英文，重點是將程式的意思表達出來）描述出來。使用虛擬碼，可以幫助我們更好的表述演算法，不用拘泥於具體的實現。

[https://www.ithome.com.tw/node/78450](https://www.ithome.com.tw/node/78450)

> 程式語言的語法形式，多半會限制程式設計者對演算法與資料結構重要觀念的思考，因而不少文件或書籍亦用虛擬碼（pseudocode）作高層次描述。

[http://nthucad.cs.nthu.edu.tw/~yyliu/personal/nou/05ct/pseudo\_code.html](http://nthucad.cs.nthu.edu.tw/~yyliu/personal/nou/05ct/pseudo_code.html)

> 範例：從1加到10演算法的虛擬程式碼，如下所示：  
> counter = 1  
> total = 0  
> while counter &lt;= 10  
> {  
>   total = total + counter  
>   add 1 to counter  
> }  
> output total

模組

#### 模組化老哏細談

[https://www.ithome.com.tw/voice/88488](https://www.ithome.com.tw/voice/88488)

DataFrame

Exercise 2

