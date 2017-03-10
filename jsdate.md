# JavaScript 日期資料

JavaScript 以 _Date_ 物件處理日期方面的資料（年、月、日、時、分、秒、毫秒）。我們也可將日期視為是一種以 1970年元月一日零時零分零秒為基準點的毫秒差，例如 3000，即是1970年元月一日零時零分三秒。

建立 Date 物件時，有以下四種寫法:

* new _Date_\(\)，例如 var dateData = _Date_\(\);
* new _Date_\(毫秒\) ，例如 var dateData = _Date_\(1489190400000\);
* new _Date_\("日期文字"\)，例如 var dateData = _Date_\("2017-03-11T13:45:00Z"\);
* new _Date_\(年月日等七個數字\)，例如 var dateData = _Date_\(2017, 2 11, 13, 45, 0, 0\);

## 當下這一刻

下列程式以瀏覽器目前的本地日期時間建立 _Date _物件:

```
var dateNow = new Date();
console.log(dateNow.toString());  // 輸出日期文字
console.log(dateNow.getTime());  // 輸出時間戳記(單位: 毫秒)
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

## 存取日期的各項屬性

建立 _Date _物件之後，可透過 _Date _物件的 getXXX\(\) 系列方法讀取年、月、日、時、分、秒、星期幾等資料（如下列程式），也可以透過 setXXX\(\) 系列方法設定各個分項屬性。

使用這些方法時，請留意:

* 月份的數字從零起算，一月為0，二月為1。
* getDay\(\) 傳回的是星期，星期天為0, 星期六為6
* getDate\(\) 傳回的才是日期

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



