
# Regular Expression


Regular Expression（正則表達式、正規表示法、正規運算式、規則運算式、常規表示法）是一套語法，這套語法在文字內容比對與擷取等方面，功能十分強大。本章將說明Regular Expression的常用語法，並且應用於表單（Form）內容驗證及JavaScript程式。

## 逐個字元定義格式

該怎麼使用Regular Expression呢? 

舉例來說，華航的航班編號是 CI-XXX，其中XXX是數字，例如: CI-123。我們希望操作人員在輸入下列的表單資料時，能按照這個格式輸入。

```
<form method="post" action="echo.php">
  China Airline flight number:
  <input type="text" name="flightNumber" pattern=""> <br>
  <input type="submit" name="btnOK" id="btnOK" value="OK">  
</form>
```

pattern 屬性可以這樣子處理:
1. 「CI-」是固定的，直接註記即可
2. 第一個 X，在一對中括號裏頭註記0-9，像這樣: CI-\[0-9\]
3. 第二個與第三個 X，也是一樣的作法，結果就變成: CI-\[0-9\]\[0-9\]\[0-9\]，如下:

```
<form method="post" action="echo.php">
  China Airline flight number:
  <input type="text" name="flightNumber" pattern="CI-[0-9][0-9][0-9]"> <br>
  <input type="submit" name="btnOK" id="btnOK" value="OK">  
</form>
```

> ##### _**Note**_
> 
> 用一對中括號指定一個字元，在中括號裏頭註明可接受哪些字元，
> 例如: [AX]O，就表示只有AO或XO符合格式，
> aO不行（a要大寫），CO也不可以（第一個字元只接受A或X）。

由於 [0-9] 數字很常用，也可以用 \d 代替:

| 格式 | 說明 | 相當於 |
| :--- | :--- | :--- |
| \d | 數字 | \[0-9\] |
| \w | 英文字母、數字、底線 | \[0-9a-zA-Z\_\] |
| \s | 空白字元 | \[\t\r\n\f\] |

> ##### _**Note**_
> 
> \d 是小寫 d，\D 表示該字元什麼都好，就是不要數字。


