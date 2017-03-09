# JavaScript 字串常用屬性與函式

## _length_ 字串字數

* _length_ 屬性傳回字串字數
* 每個中文字佔用三個位元組的記憶體，但 _length _傳回單位為字數，也就是說，"中文字"._length_ 長度為三。

```
var data = "中文字";
var dataLength = data.length;  // 傳回 3
```

> ##### _**Exercise**_
>
> w3schools 線上練習網址:  
> [https://www.w3schools.com/js/tryit.asp?filename=tryjs\_string\_length](https://www.w3schools.com/js/tryit.asp?filename=tryjs_string_length\)\)

## _indexOf\(\)_ 搜尋特定文字

* 使用格式: "稻草堆"._indexOf_\("針" \[, 從哪一個位置找起\]\)
* 傳回「針」的起始位置。傳回零，表示在一開始第一個位置就找到了
* 傳回 -1 表示沒找到
* 省略第二個參數時，預設從零找起

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

* "字串內容"._substr_\(開始位置 \[, 長度\]\)
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

* "字串內容"._slice_\(開始位置 \[, 結束位置\]\)
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





