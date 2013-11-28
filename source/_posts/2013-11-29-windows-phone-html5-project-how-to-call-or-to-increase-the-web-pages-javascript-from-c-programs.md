layout: post
title: '#Windows Phone：在HTML5專案中，如何從C#執行網頁的Javascript程式'
date: 2013-11-29 02:00
comments: true
categories: [Windows Phone, APP, HTML5]
tags: [Windows Phone, APP, HTML5]
---
在開發Windows Phone APP的HTML5專案中，究竟該如何從C#執行網頁的Javascript程式呢？現在就讓我來介紹一下吧！

# C#呼叫Javascript端的函式
首先在網頁中定義一個changeTitle的function，讓C#端可以利用這個function更改id為page-title的標籤內的第一個p標籤內的值。
```html index.html
<!DOCTYPE html>
<html>
    <head>
        <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
        <link rel="stylesheet" type="text/css" href="/html/css/phone.css" />
        <title>Windows Phone</title>
        <script>
            var changeTitle = function (text) {
                document.querySelectorAll("#page-title p")[0].innerHTML = text;
            }
        </script>
    </head>
    <body>
        <div>
            <p>我的應用程式</p>
        </div>
        <div id="page-title">
            <p>頁面標題</p>
        </div>
    </body>
</html>
```

為了示範，在這裡更改按下［上一頁］的按鈕的行為為呼叫Javascript端的changeTitle的function，並且傳入"Hello World!"這個字串，底下是程式碼：
```cs MainPage.cs
private void BackApplicationBar_Click(object sender, EventArgs e)
{
  Browser.InvokeScript("changeTitle", new string[] { "Hello World!" });
  //Browser.GoBack();
}
```
*註：如果不需傳參數，直接使用`Browser.InvokeScript("changeTitle")`即可。*

尚未按上一頁按鈕之前：
![csjs01.png](/image/iZpv6fRkTJ2yILO62rKB_csjs01.png)

按下上一頁按鈕之後：
![csjs02.png](/image/hViKSRYzSrc1WLeWZZAN_csjs02.png)

# C#直接執行Javascript端的程式碼
依照上面的道理，其實可以利用`eval()`函式來執行Javascript端的程式碼。所以上述範例其實可以改成：
```cs MainPage.cs
Browser.InvokeScript("eval", 
	new string[] { "document.querySelectorAll("#page-title p")[0].innerHTML = "Hello World!";" });
```

# 參考資料
1. Getting Started With Windows Phone 8 HTML5 Apps：[http://blogs.msdn.com/b/matthiasshapiro/archive/2013/02/15/getting-started-with-windows-phone-8-html5-apps.aspx](http://blogs.msdn.com/b/matthiasshapiro/archive/2013/02/15/getting-started-with-windows-phone-8-html5-apps.aspx)
