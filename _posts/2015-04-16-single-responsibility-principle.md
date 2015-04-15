---
layout: post
title: Design Pattern, SOLID princinples
---

<div class="message">
  從來沒有那麼的羞愧，覺得自己以前寫code的都是垃圾
</div>

[SOLID](http://en.wikipedia.org/wiki/SOLID_%28object-oriented_design%29)
是一組縮寫，由5個 design principle 組成，分別是 Single responsibility principle, Open/closed principle, 
Liskov substitution principle, Interface segregation principle, Dependency inversion principle.
這種大師寫的聖旨像我這種一般的凡人怎麼有辦法去做解釋，這邊我只能用我讀完後的心得跟大家做個分享及討論，
如果有錯誤的地方麻煩請指正我.

## S. Single responsibility principle

> 單一功能原則規定每一個Class都應該只負責軟體架構裡其中一個功能, 而這責任也應該完全屬於這個Class. 在這Class裡面, 所有功能都應該緊緊的貼齊這Class的責任, 也就是說沒有多餘,不相關的功能在裡面.

這個原則是由[Robert C. Martin](http://en.wikipedia.org/wiki/Robert_Cecil_Martin)在他的書中提出. 
Martin 定義每個 software 裡面的 module 必須有一個, 而且是唯一的一個理由去改變(one reason to change). 
那到底什麼是 reason to change ?

有些人覺得有 bug 就是要 change, 有另一些人覺得是 refactor 的時候要 change, 而這個答案我們可以從責任去想.

假設我們今天要寫一個nike+, 要把GPS的點位存起來成為一個路跑記錄. 那我們會需要一個 GPS Tracker 的 Class.

{% highlight swift %}
class GPSTracker {
    func start()
    func stop()
    func saveAsActivity() -> Activity
} 
{% endhighlight %}

我們定義了這個Class可以開始跟結束, 然後可以把結果寫進 Activity 存起來. 
這樣的設計看似非常美好, 但是今天如果路跑記錄的 format 有改變, 這個 Class 也是就必須做調整,
同時我們又想增強 GPS 的功能, 支援暫停(stop)跟繼續(resume)的功能, 我們也得去調整 Class.

注意到了嗎? 這個 GPSTracker 因為兩個不同的`責任`而需要改變, 這樣就不遵守SRP了.
GPSTracker本來的用意就是記錄GPS的結果, 要如何把這些記錄存成路跑記錄應該要由別人負責, 
他本身不能也不該知道Activity的細節. 這樣就不是一個好的設計, 我們應該要把 saveAsActivity 拿掉, 
讓所有個功能都緊緊的與他該做的事情貼齊.

Martin 在[一篇文章](http://blog.8thlight.com/uncle-bob/2014/05/08/SingleReponsibilityPrinciple.html)也點出了single responsibility principle的精髓

> This principle is about people.

當我們今天寫了一個module, 我們會希望只會有一個人, 或是一群人代表某個商業邏輯, 來發出修改.
我們非常努力的把這個module在複雜的架構下獨立出來, 只對這一個人, 或一個邏輯負責.

假設你今天興高采烈的寫了一個相機修圖app, 但是iphone有硬體上的bug無法使用. 
結果下一代iphone出來修正了bug, 但是不能修照片了, 你應該會覺得apple把你當白痴耍.
(但是媒體會拼命的報導拿掉相機讓iphone成為世界上最薄的手機)

如果你認真想遵守SRP, 會發現現實面上沒有想像中的那麼簡單, 你會需要更好的pattern, 更棒的interface,
那有沒有什麼時候可以偷偷地不遵守呢?

> If the application changes in ways that affect the signature of the connection functions, then the design will smell of Rigidity... In that case the two responsibilities should be separated. If, on the other hand, the application is not changing in ways that cause the two responsibilities to change at different times, then there is no need to separate them. 如果application沒有辦法用某種方式, 使得兩種責任分別在不同的時間發生改變, 也就是說兩種責任一定一起改變, 那我們不分開他們也沒關係.

最後還是列出Martin對SRP的另一種解釋:

> Gather together the things that change for the same reasons. Separate those things that change for different reasons.把因為相同原因而發生改變的事情包起來, 分開那些因為不同原因而改變的事情








