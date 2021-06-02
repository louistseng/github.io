# Callback -> Promise -> await

# [筆記 5/29]

> Callback hell 非同步  
> Solution -> Promise 同步 並可一起處理錯誤  
> Promise -> await 單執行緒

**Promise:**

> 有「擱置（pending）、實現（fulfilled）、拒絕（rejected）」三種狀態。
>
> Promise 是一個物件，代表著一個尚未完成，但最終會完成的一個動作 —在一個「非同步處理」的流程中，它只是一個暫存的值（Placeholder），是 Callback 以外的另一種方式來處理非同步事件，且可讀性與可維護性比 Callback 好很多。

**Promise chain:**

> 將多個 Promise 串在一起，以表達一個序列的非同步執行步驟，而這個序列就是 promise chain。

**await:只能在  async function 內使用**

> 通過事件迴圈實現非阻塞的同步等待，會暫停 async 函式執行，等待 Promise 物件的解析，並在 promise 物件的值被 resolve 時回復 async 函式的執行。await 接著回傳這個被 resolve 的值。如果回傳值不是一個 Promise 物件，則會被轉換為 resolved 狀態的 Promise 物件。  
> 如果 Promise 物件被 rejected，則 await 會丟出 rejected 的值。

**macrotask**

> JS 引擎 -> Promise -> setTimeout

**libuv （C 語言寫成）**

> Node 是 libuv 負責處理跟 OS 的溝通像是讀取檔案內容，從網路取得資料，因此他會對 OS 發出 request。  
> 在 libuv 有一個 Queue，負責放 OS 已經做完的 event。V8 執行 Javascript 程式和 OS 做完事情放到 Queue 是同時進行的。  
> 而 libuv 最重要的是 Event Loop 負責「循環」檢查 Queue 裡面的事件，當發現 Queue 有已經完成的 event 會告訴 V8 執行 Callback(當 event 完成時要執行的程式)
