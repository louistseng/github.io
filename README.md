   
#  Js 單一單執行緒(single Thread)  
# [筆記 5/21]   

**setimeout Callback**   
**webapis -> event loop -> task queue**   

>如果task queue還有任務要執行會在放回 task  
>(會在 webapis 倒數，再被放到 task queue)

**Async callback 非同步回調**  
>不能直接把東西丟回 stack 上,會隨機出現在你的程式碼中.  
>
>event loop 的工作就是查看stack並查看任務佇列,  
>如果stack是空的,他會將第一個東西放在佇列上,並推到stack上執行.  
>
>**設settimeout並不會馬上執行**    
>
>在陣列上forEach的方式不會執行,需要一個函式呼叫一個cb,  
>但他不會非同步執行,而是在當前的stack中執行,  
>可定義一個非同步forEach好讓它可接受一個陣列、一個cb,  
>陣列中的項目上,它將使用這個cb去執行.
>
>假設在陣列中,每個元素進行緩慢的處理,  
>如果沒注意程式碼是如何排進佇列的話,畫面就會變得遲鈍.  

**Async是接收到需求,不用一直等到需求完成再執行其他需求**    

>sync：在「同一個步道」比賽「接力賽跑」,當棒子沒有交給我,我就得等你,不能跑.  
>Async：在「不 ( 非 ) 同步道」比賽「賽跑」,誰都不等誰,只要輪到我跑,我就開始跑.  

* **執行環境 (runtime) ：**    
    * Js: setTimeout \ document \ XMLHRequest \ fetch (瀏覽器)  
    * Node.js: setTimeout \ OS \ http \ fs  

>真正執行渲染時的 thread 跟執行 js 的 thread 是屬於不同個 thread  
>執行 js 程式的 thread 範疇是在 task 以及 microtask 中  
>但進行渲染時會是透過另一個 GUI thread 去進行渲染  

>GUI渲染線程與JS引擎線程互斥，由於JavaScript是可操縱DOM的，如果在修改這些元素屬性同時渲染介面（即JavaScript線程和UI線程同時運行），那麼渲染線程前後獲得的元素數據就可能不一致。當JavaScript引擎執行時GUI線程會被掛起，GUI更新會被保存在一個隊列中等到引擎線程空閒時立即被執行。由於GUI渲染線程與JS執行線程是互斥的關係，當瀏覽器在執行JS程序的時候，GUI渲染線程會被保存在一個隊列中，直到JS程序執行完成，才會接著執行。因此如果JS執行的時間過長，這樣就會造成頁面的渲染不連貫，導致頁面渲染加載阻塞的感覺。     

    [原文網址：](https://kknews.cc/other/rl4o9ov.html)  

**Ajax XHR**     
>AJAX 在 JS 中,是透過 XMLHttpRequest(XHR) 物件作為實作.  
>它能夠在 client 端對 server 端送出 http request  

**XMLHttpRequest 物件實體有兩種方式來提交表單：**  
>僅使用 AJAX : 只使用 AJAX 的方式較為複雜，但也更加靈活、強大。  
>使用 FormData API : 使用 FormData API 是最簡單、快速的方式，但不利於將資料集合進行字串化。
>
>SPA 單頁應用(single-page application)  

   


