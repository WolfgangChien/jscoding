# JavaScript 字串常用屬性與函式

## _length_ 字串字數

* _length_ 屬性傳回字串字數
* 雖然每個中文字實際佔用三個位元組的記憶體，但 _length _傳回單位為字數，也就是說，"中文字"._length_ 長度為三。

```
var data = "中文字";
var dataLength = data.length;  // 傳回 3
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_length](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_length%29\)

## _indexOf\(\)_ 搜尋特定文字

* 使用格式: "稻草堆"._indexOf _\("針" \[, 從哪一個位置找起\]\)
* 傳回「針」的起始位置。傳回零，表示在開始第一個位置就找到了
* 傳回 -1 表示沒找到
* 省略第二個參數時，預設為零，也就是從最左邊開始找起

```
var data = "A secret makes a woman, woman."; // Vermouth (Detective Conan)
var position = data.indexOf("woman"); // 傳回 17
var nextPosition = data.indexOf("woman", position + 1);  // 傳回 24
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_indexof](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_indexof)

## _substr\(\) _擷取字串的部分內容

* "字串內容"._substr _\(開始位置 \[, 長度\]\)
* 省略「長度」時，將一直取至字串結尾

```
var str = "0123456789";
var result = str.substr(2, 5);  // 23456
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_substr](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_substr)
>
> ##### _**Exercise**_
>
> 請想想看，如何以 _substr\(\)_ 取一個字串最右邊三個字?

## _slice\(\)_ 擷取字串的部分內容

* "字串內容"._slice _\(開始位置 \[, 結束位置\]\)
* 「開始位置」與「結束位置」**大於等於零**時，表示從開始位置取至結束位置之前\(不含結束位置的那個字元\)
* 省略「結束位置」時，將一直取至字串結尾

```
var str = "0123456789876543210";
var result = str.slice(2, 5); // 234
```

* 「開始位置」與「結束位置」為**負數**時，表示從 _length _+ 「開始位置」, 取至 _length _+ 「結束位置」
* 不妨想像成: 從右邊算起，只是，位置編號變成從一開始算起（JavaScript 習慣從零開始數起）。

```
var str = "0123456789876543210";
//                   012345678
// 19 - 6 = 13
// 19 - 1 = 18
// 從 13 取至 18 (不含18), 
// 也可以想成: 右邊數來第六個，取到右邊第一個(不含)之前
var result = str.slice(-6, -1); // 54321
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_slice](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_slice)
>
> ##### _**Exercise**_
>
> 請Google一下 _substring\(\)_ 的使用說明，該函式與 _slice\(\)_、_substr\(\)_ 有何異同?

## _toUpperCase\(\)_ _toLowerCase\(\)_ 轉大寫／小寫

* "string"._toUpperCase\(\)_ 轉大寫
* "string"._toLowerCase\(\)_ 轉大寫

```
// code
var data = "Hello!";
alert( data.toUpperCase() );  // HELLO!
alert( data.toLowerCase() );  // hello!
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_tolower](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_tolower)

## _charAt\(\)_ 傳回字串於指定位置的字元

* 相當於"string"\[編號\]，但是 _charAt \(編號\)_ 比較**安全**
* 編號照例從零算起
* "string"\[編號\] 的編號超過範圍時，會得到 undefined
* _charAt \(編號\)_ 的編號超過範圍時，傳回空字串

```
var str = "錢達智";

var result = str.charAt(2);  // 智
var result = str[2];

var result = str.charAt(3);  // "" 空字串
alert(result.length); // 0
var result = str[3];  // undefined
alert(result.length); // 程式發生錯誤
```

> _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_charat](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_charat)

## _charCodeAt\(\)_ 查出字串指定位置的字元內碼

* _charCodeAt \(編號\)_ 傳回字串指定位置的字元內碼
* 編號照例從零算起
* 指定的位置沒有字元時，傳回 NaN

```
var str = "錢達智";
var result = str.charCodeAt(0).toString(16) 
     + "," + str.charCodeAt(1).toString(16)
     + "," + str.charCodeAt(2).toString(16)
// 9322,9054,667a
```

> ##### _**Exercise**_
>
> 請用 _charCodeAt\(\)_ 查出你的中文名字的 Unicode 編號

## _split\(\)_ 將字串拆解成陣列

* 格式: "字串"._split \("分界字元"\)_
* 用分界字元將字串斷成一個字串陣列

```
var str = "錢達智,B123456789,M";
var dataArray = str.split(","); 
// ["錢達智", "B123456789", "M"]
console.log(JSON.stringify(dataArray));
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_split](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_split)
>
> ##### _**Exercise**_
>
> 請想想看，如何取出 c:\doc\faq.txt 的檔名?

## _search\(\)_ 以 Regular Expression 語法搜尋文字

* 與 _indexOf\(\)_ 相比，更有彈性（但也比較慢一些）。
* 下列程式的第一行，結尾處以 i 告知  JavaScript 引擎進行 case-insensitive 不區分大小寫文字比對。
* 找不到時，傳回 -1

```
var format = /ci-15\d/i;
var data = "Flight numbers: CI-123, CI-151, CI-156."; 
var result = data.search(format);
console.log(result);  // 24
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_search\_regexp](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_search_regexp)
>
> ##### _**Note**_
>
> 關於 Regular Expression，請參考 Regular Expression 這章的說明。

## _replace\(\)_ 字串搜尋替換

* "在來源字串"._replace\(找什麼，"換成什麼"\)_ 
* 第一個參數 "找什麼" 若為字串，會以區分大寫小寫的方式，換掉找到的第一個項目
* 第一個參數「找什麼」 若為 Regular Expression，則依格式處理，例如下列區塊的最後一行程式
  * **i**：case-insensitive，不區分大寫小寫
  * **g**：global match，不只換掉一個，全部更換

```
var source = "abcABCabc";
var result = source.replace("ABC", "$"); // abc$abc
var result = source.replace(/abc/, "$"); // $ABCabc
var result = source.replace(/abc/ig, "$"); // $$$
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref\_replace](https://www.w3schools.com/jsref/tryit.asp?filename=tryjsref_replace)
>
> ##### _**Exercise**_
>
> 如何將 "0123456789" 的 8 移到字串最左邊呢?



