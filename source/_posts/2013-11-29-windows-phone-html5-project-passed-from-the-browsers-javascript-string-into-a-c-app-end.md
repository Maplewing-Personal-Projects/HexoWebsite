layout: post
title: '#Windows Phone：在HTML5專案中，如何從Javascript傳送字串到C#的APP端'
date: 2013-11-29 02:30
comments: true
categories: [Windows Phone, APP, HTML5]
tags: [Windows Phone, APP, HTML5]
---
在開發Windows Phone APP的HTML5專案中，究竟該如何從Javascript傳給APP的C#程式碼中呢？現在就讓我來介紹一下吧！

# 使Javascript能與APP的C#程式碼溝通
首先先對嵌入至HTML5專案中的瀏覽器加上當觸發ScriptNotify事件時處理的函式，Javascript可藉此觸發ScriptNotify事件將字串傳給APP使用。在此範例裡，設定當Javascript傳字串過來時，就使用`MessageBox.Show`將字串顯示出來。
```cs MainPage.cs
private void Browser_Loaded(object sender, RoutedEventArgs e)
{
  Browser.IsScriptEnabled = true;
  Browser.ScriptNotify += HTML_Script_Launched;
  // 在此加入您的 URL
  Browser.Navigate(new Uri(MainUri, UriKind.Relative));
}

private void HTML_Script_Launched(object sender, NotifyEventArgs e)
{
  MessageBox.Show(e.Value); 
}
```
*註：亦可直接從xaml中增加。`<phone:WebBrowser x:Name="Browser" ScriptNotify="HTML_Script_Launched" />`*

接著只要在Javascript端，呼叫`window.external.notify`函式並傳值即可。

```html index.html
  <!DOCTYPE html>
<html>
  <head>
    <meta http-equiv="Content-Type" content="text/html; charset=UTF-8" />
    <link rel="stylesheet" type="text/css" href="/html/css/phone.css" />
    <title>Windows Phone</title>
    <script>
      window.external.notify("Hello World!");
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

這樣就可以了！底下是結果：
![csjs03.png](/image/NfBodyjSjmv1DMhZNuFp_csjs03.png)

# 參考資料
1. Getting Started With Windows Phone 8 HTML5 Apps：[http://blogs.msdn.com/b/matthiasshapiro/archive/2013/02/15/getting-started-with-windows-phone-8-html5-apps.aspx](http://blogs.msdn.com/b/matthiasshapiro/archive/2013/02/15/getting-started-with-windows-phone-8-html5-apps.aspx)