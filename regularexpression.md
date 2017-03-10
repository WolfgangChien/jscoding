# Regular Expression

Regular Expression（正則表達式、正規表示法、正規運算式、規則運算式、常規表示法）是一套語法，這套語法在文字內容的比對與擷取等方面，功能十分強大。本章將說明Regular Expression的常用語法，並且應用於表單（Form）內容驗證及JavaScript程式。

## 基本入門：逐個字元定義格式

該怎麼使用Regular Expression呢?

舉例來說，華航的航班編號是 CI-XXX，其中XXX是數字，例如: CI-123。我們希望操作人員在輸入下列的表單資料時，能按照這個格式輸入。

```
<form method="post" action="echo.php">
  China Airline flight number:
  <input type="text" name="flightNumber" pattern=""> <br>
  <input type="submit" name="btnOK" id="btnOK" value="OK">  
</form>
```

pattern 的屬性值可以這樣子處理:  
1. 「CI-」是固定的，直接註記即可  
2. 第一個 X，在一對中括號裏頭註記0-9，像這樣: CI-\[0-9\]  
3. 第二個與第三個 X，也採用相同的作法，完成後的格式: CI-\[0-9\]\[0-9\]\[0-9\]，如下:

```
<form method="post" action="echo.php">
  China Airline flight number:
  <input type="text" name="flightNumber" pattern="CI-[0-9][0-9][0-9]"> <br>
  <input type="submit" name="btnOK" id="btnOK" value="OK">  
</form>
```

> ##### _**Note**_
>
> 用一對中括號指定一個字元，在中括號裏頭註明可接受哪些字元，例如: \[AX\]O，就表示只有AO或XO符合格式，aO不行（a要大寫），CO也不可以（第一個字元只接受A或X）。

由於 \[0-9\] 數字很常用，於是Regular Expression特別設計一個簡寫的代替語法: **\d** ，上述的華航的航班編號格式，可以改寫成  
 **CI-\d\d\d**。

其他常用的字元語法整理如下表:

| 格式 | 說明 | 相當於... |
| :--- | :--- | :--- |
| **\d** | 數字 | \[0-9\] |
| **\w** | 英文字母、數字、底線 | \[0-9a-zA-Z\_\] |
| **\s** | 空白字元 | \[ \t\r\n\f\] |
| **\D** | 不要數字 | \[^0-9\] |
| **\W** | 不要這些: 英文字母、數字、底線 | \[^0-9a-zA-Z\_\] |

## 數量語法

接下來，我們來試試看身份證字號的格式該怎麼訂:  
1. 第一個字元是大寫字母: \[A-Z\]  
2. 第二碼不是一就是二，格式就變成: \[A-Z\]\[12\]  
3. 接下來有八個數字，寫成 \[A-Z\]\[12\]\[0-9\]\[0-9\]\[0-9\]\[0-9\]\[0-9\]\[0-9\]\[0-9\]\[0-9\]，感覺不僅有點囉嗦，而且很容易數錯。  
4. 改成這樣會好一點（恐怕還是會數錯）: \[A-Z\]\[12\]\d\d\d\d\d\d\d\d  
5. 這樣會不會更好: **\[A-Z\]\[12\]\d{8}**

關於{數字}的語法說明:

* **X{N}**，N是數字，表示X的數量不多不少正好要是N個
* **{N, M}**，表示數量介於N到M之間\(包括 N, M\)，例如 \d{3, 5} 表示三到五個數字。
* **{N, }** 表示 N 個\(含\)以上
* **{, M}** 表示 M 個\(含\)以下

其他有闗於數量的語法:

| 格式 | 說明 | 相當於... |
| :--- | :--- | :--- |
| **?** | 零或一個 | {0,1} |
| **\*** | 零個以上 | {0, } |
| **+** | 至少一個 | {1, } |

## 群組

學會「群組」，你的Regular Expression功力就更上一層。什麼是「群組」？簡單地說：用括號包起來的就算一組。

還是用例子來學比較有方向感。舉例來說，如何指定 e-mail 的格式呢?  
1. e-mail 最好認的特徵就是 @，所以，先暫定成 \w+@\w+。也就是 @ 符號前後一定都要有字。  
2. 有時候，在 @ 左邊可能會出現例如 wolfgnag.ta-chih.chien@gmail.com 含有句號、連字號的情形，但 \w+ 並不接受句號、連字號，怎麼辦呢?  
3. 這樣子如何: **\w+\(\[.-\]\w+\)\*@\w+\(\[.-\]\w+\)+**

（驚！）別急一段一段慢慢來：

* ** \[.-\]\w+** 用括號包起來，所以它們構成一組。這組的格式是說，句號或連字號的後頭一定要有字（像 wolfgang**-**@gmail.com就不許，連字號後面一定要有字）。
* **\( \[.-\]\w+\) **這組又以＊修飾，說明了這組可能完全不出現，也可能重複好幾次（每次重複都一定不能以句號、連字號結尾）。
* \w+\(\[.-\]\w+\)\*@**\w+\(\[.-\]\w+\)+** 在 @ 右邊的情也類似，但是改用＋符號設定至少要出現一次。

## 其他重要符號

| 符號 | 說明 |
| :--- | :--- |
| ｜ | 鍵盤 **shift + \** 打出來的那個濾管符號，作用為:「**或者**」。例如郵遞區號有三碼也有五碼的數字，格式為: \d{5}｜\d{3} |
| ＼ | 倒斜線 = **「轉意符」、「逸脫字元」**。例如，左括號在正則運算式已用來指定群組，但我們現在希望特定位置就是括號時，可利用 \\( 來聲明那裏就是括號，不是群組。 |

## JavaScript 與 Regular Expression

JavaScript 使用下列格式指定 Regular Expression:

```
  /pattern/modifiers
```

例如:

```
var format = /ci-15\d/i;
var data = "Flight numbers: CI-123, CI-151, CI-156."; 
var result = data.search(format);
console.log(result);  // 24
```

上述程式的第一行，結尾處以** i **告知  JavaScript 引擎進行 case-insensitive 不區分大小寫文字比對。

## _test\(\)_ 測試文字內容是否符合格式

* _/RegularExpression/.test\("待驗內容"\)_ 檢查「待驗內容」是否符合RegularExpression格式。
* 符合格式的話，_test\(\)_傳回 true，否則傳回 false

```
var format = /ci-15\d/i;
var data = "Flight numbers: CI-123, CI-151, CI-156."; 
var result = format.test(data);
console.log(result);  // true
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_regexp\_test](https://www.w3schools.com/js/tryit.asp?filename=tryjs_regexp_test)

## _exec\(\)_ 以 Regular Expression 擷取文字

* _/RegularExpression/.exec\("文字內容"\)_  依Regular Expression格式擷取「文字內容」。
* 如果找到符合格式的文字，傳回找到的內容，否則傳回 null 

```
var format = /ci-15\d/i;
var data = "Flight numbers: CI-123, CI-151, CI-156."; 
var result = format.exec(data);
console.log(result);  // CI-151
```

如果要繼續找「下一個」，請留意下列兩個重點:

* /pattern/modifiers，modifiers 要加上 **g**，例如: /ci-15\d/i**g**
* 連續呼叫 _exec\(\)_ 方法。第二回合如果有找到的話就是找出第二個，第三回合找到的就是第三個，以下類推。例如:

```
var format = /CI-15\d/g;
var data = "Flight numbers: CI-123, CI-151, CI-156.";
alert(result.length);
while ( ( result = format.exec(data) ) !== null ) {
    alert(result);
}
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_regexp\_exec](https://www.w3schools.com/js/tryit.asp?filename=tryjs_regexp_exec)



