# JavaScript 日期資料

JavaScript 以 _Date_ 物件處理日期方面的資料（年、月、日、時、分、秒、毫秒）。我們也可將日期視為是一種以格林威治標準時間 1970年元月一日零時零分零秒為基準點的毫秒差，例如 3000，即是1970年元月一日零時零分三秒。

建立 Date 物件時，有以下四種寫法（本文稍後會詳述）:

* new _Date_\(\)，例如 var dateData = _Date_\(\);
* new _Date_\(毫秒數\) ，例如 var dateData = _Date_\(1489190400000\);
* new _Date_\("日期文字"\)，例如 var dateData = _Date_\("2017-03-11T13:45:00Z"\);
* new _Date_\(年月日等七個數字\)，例如 var dateData = _Date_\(2017, 2 11, 13, 45, 0, 0\);

## 當下這一刻

下列程式建立 Date 物件時，沒有傳入任何參數，預設為「目前時間」。

所謂「目前時間」，詳細地說，是以瀏覽器的本地日期時間，配合瀏覽器所在作業系統設定的時區，換算成國際標準時間（以毫秒為單位的時間戳記），建立 _Date _物件。

不過，_Date _物件的資料在輸出成字串時，預設的作法會依照瀏覽器所在的時區，換算成本地時間。如果需要輸出國際標準時間的字串，應該改呼叫 _toUTCString\(\)_ 方法。程式示範如下：

```
var dateNow = new Date();
console.log(dateNow.getTime()); // 時間戳記(單位: 毫秒)
console.log(dateNow.toString()); // 輸出本地時間
console.log(dateNow.toUTCString()); // 輸出國際標準時間
```

## 將文字轉成日期

依照 ISO 8601 標準，日期格式為 yyyy-mm-dd，依此格式傳入日期文字可建立 _Date_ 物件:

```
var dateData = new Date("2017-03-11");
console.log(dateData.toString());
// ⇒ Sat Mar 11 2017 08:00:00 GMT+0800 (台北標準時間)
console.log(dateData.toUTCString());
// ⇒ Sat, 11 Mar 2017 00:00:00 GMT
```

上述程式既沒有指定時間也沒有指定時區，預設為 00:00:00、格林威治國際標準時間。等同於下列寫法:

```
var dateData = new Date("2017-03-11T00:00:00Z");
console.log(dateData.toString());
// ⇒ Sat Mar 11 2017 08:00:00 GMT+0800 (台北標準時間)
console.log(dateData.toUTCString());
// ⇒ Sat, 11 Mar 2017 00:00:00 GMT
```

對於上述的輸出結果感到困惑嗎? 請想想看，國際標準時3月11日零時，相當於台北上午八點鐘。

如果要指定時區，以台灣為例，請用下列任一格式:

* 2017-03-11T00:00:00+08:00
* 2017-03-11 00:00:00 \(Taipei\)
* 2017-03-11 00:00:00 \(CST\)

以下列程式為例，建立 _Date_ 物件時，有特別註記台灣時間。請特別留意最後一行程式，台灣 3/11 00:00，倫敦時間為前一日的下午四點。

```
var dateData = new Date("2017-03-11T00:00:00+08:00");
console.log(dateData.toString());
// ⇒ Sat Mar 11 2017 00:00:00 GMT+0800 (台北標準時間)
console.log(dateData.toUTCString());
// ⇒ Fri, 10 Mar 2017 16:00:00 GMT
```

## 以七個日期數字建立 _Date _物件

建立 _Date_ 物件時，也可依序傳入年、月、日、時、分、秒、毫秒，建立特定日期時間的 Date物件。但請留意第二個參數「月份」，月份在 JavaScript 是從零起跳的，也就是說，一月為0，二月為1，三月為2。

```
var dateData = new Date(2017, 2, 11, 0, 0, 0, 0);
console.log(dateData.toString());
// ⇒ Sat Mar 11 2017 00:00:00 GMT+0800 (台北標準時間)
console.log(dateData.toUTCString());
// ⇒ Sat Mar 11 2017 00:00:00 GMT+0800 (台北標準時間)
```

## JavaScript 究竟如何儲存日期時間

時間戳記是個數字。JavaScript 的時間戳記是相對於 1970年元月一日零時零分零秒為基準點的毫秒差，例如 3000，即是1970年元月一日零時零分三秒。

不論我們指定哪一時區的時間資料，JavaScript 都會換算成國際標準時間，然後記下該時間的時間戳記。

以下列的程式來說，_getTime\(\)_ 抓出來的時間戳記值為零，因為筆者人在台灣，所以 _toString\(\)_ 顯示的是上午八點鐘。

```
var dateData = new Date("1970-01-01");
console.log(dateData.toString());
// ⇒ Thu Jan 01 1970 08:00:00 GMT+0800 (台北標準時間)
console.log(dateData.toUTCString());
// ⇒ Thu, 01 Jan 1970 00:00:00 GMT
console.log(dateData.getTime());
// ⇒ 0
```

請再看下列這一則例子：這回我們在建立 _Date_ 物件時，有指定時區。雖然傳入的是上午八點鐘的資料，但是後來抓到的時間戳記值仍然是零（而非 1000 \* 60 \* 60 \* 8），很明顯地，JavaScript  _Date_ 物件記住的是國際標準時間。

```
var dateData = new Date("1970-01-01T08:00:00+08:00");
console.log(dateData.toString());
// ⇒ Thu Jan 01 1970 08:00:00 GMT+0800 (台北標準時間)
console.log(dateData.toUTCString());
// ⇒ Thu, 01 Jan 1970 00:00:00 GMT
console.log(dateData.getTime());
// ⇒ 0
```

最後一則例子:

```
var dateData = new Date(0);
console.log(dateData.toString());
// ⇒ Thu Jan 01 1970 08:00:00 GMT+0800 (台北標準時間)
console.log(dateData.toUTCString());
// ⇒ Thu, 01 Jan 1970 00:00:00 GMT
console.log(dateData.getTime());
// ⇒ 0
```

上述程式，傳入 _Date _建構程式的值為 0。這個零值的日期資料，在 _toString\(\)_ 時，傳回的是上午八點鐘，_getTime\(\)_ 的值為零。

## 存取日期的各項屬性

建立 _Date _物件之後，可透過 _Date _物件的 getXXX\(\) 系列方法讀取年、月、日、時、分、秒、星期幾等資料（如下列程式），也可以透過 setXXX\(\) 系列方法設定各個分項屬性。

使用這些方法時，請留意:

* 月份的數字從零起算，一月為0，二月為1。
* _getDay\(\)_ 傳回的是星期，星期天為0, 星期六為6
* _getDate\(\)_ 傳回的才是日期

```
var dateData = new Date("2017-03-11T13:45:00+08:00");
console.log(dateData.toString());
console.log(dateData.getMonth());  // 月份，三月為２
console.log(dateData.getDate());  // 日期，從一起算，3/1就是一，3/2傳回2
console.log(dateData.getDay());  // 星期，星期天為０
```

> ##### Exercise
>
> 請連往 w3schools.com 關於日期各項方法的說明頁並試用其方法，  
> 網址: [https://www.w3schools.com/js/js\_date\_methods.asp](https://www.w3schools.com/js/js_date_methods.asp)
>
> Exercise
>
> 如何將日期輸出成 yyyy-mm-dd 格式? 也就是將 2017/3/11 輸出成 2017-03-11

##### 



