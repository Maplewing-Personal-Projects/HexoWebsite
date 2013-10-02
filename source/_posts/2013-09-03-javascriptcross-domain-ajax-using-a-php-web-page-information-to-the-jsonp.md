layout: post
title: '#Javascript：Cross Domain AJAX－使用PHP將網頁資訊轉JSONP'
date: 2013-09-03 19:50
comments: true
categories: [javascript, Ajax]
---
其實在使用[上篇](http://knightzone.logdown.com/posts/98927-javascriptcross-domain-ajax-using-yql)使用YQL來進行Cross Domain AJAX之前，我是先使用別人寫好的PHP網頁將要抓取之網站資訊轉成JSONP格式回來。

## ba-simple-proxy.php
此頁別人寫好的PHP連結在此：[ba-simple-proxy.php](http://benalman.com/code/projects/php-simple-proxy/docs/files/ba-simple-proxy-php.html)

簡單來說，這PHP就是當作一個代理網頁，給它網址它就會抓取該網址所指的網頁內容，並用JSONP的格式回傳回來。

使用前先將該頁PHP內的 $enable_jsop = false; 從false改為true，然後上傳到PHP伺服器，接著使用AJAX抓取資料的js部分寫上：
``` js xdomainajax.js
$.getJSON( /* ba-simple-proxy.php所在地 + "?callback=?&url=" + 欲抓資料之網頁所在的網址 */ , function(data){
	/* data.contents即是該網頁內容 */
});
```
這樣就可以進行Cross Domain AJAX了！

## 參考資料
1. Cross Domain AJAX 抓網頁撈過界以及如何整合兩個部落格的標籤：[http://user.frdm.info/ckhung/b/js/xdomain.php](http://user.frdm.info/ckhung/b/js/xdomain.php)
2. Design2U » Cross Domain Ajax 跨網域抓取資料(JSONP)：[http://design2u.me/blog/936/cross-domain-ajax-cross-domain-data-has-been-retrieved-jsonp](http://design2u.me/blog/936/cross-domain-ajax-cross-domain-data-has-been-retrieved-jsonp)
3. SIMPLE PHP PROXY: GET EXTERNAL HTML, JSON AND MORE!：[http://benalman.com/code/projects/php-simple-proxy/docs/files/ba-simple-proxy-php.html](http://benalman.com/code/projects/php-simple-proxy/docs/files/ba-simple-proxy-php.html)

