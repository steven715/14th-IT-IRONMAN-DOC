# 第三天: 為 C++準備環境(二)

來到了第三天，今天我就沿著上次決定 C++版本的部分(C++ 20)繼續下去。

既然決定了程式語言及版本，那下一步就是需要來確定開發環境，那就是該語言的編譯器(C++是[靜態語言](https://blog.csdn.net/yuanmengong886/article/details/52572533)，需要透過編譯器才能變成電腦可以執行的檔案)及 IDE，還有一些額外的輔助工具(如果有的話)。

## C++ 編譯器

GCC 就是 C++的編譯器(同時也能編譯 C、Object-C 跟最近很火的 GO，)，全名是 GNU Compiler Collection，GNU 是指[GNU operation system](https://www.gnu.org/gnu/thegnuproject.html)，是個可以跨平台的酷東西。

那回歸到如果要在我的本機上開發這件事，由於我電腦的 OS 都是 Windows，而身為微軟陣營的人，就是要使用微軟陣營最強大的武器-_Visual Studio 2022_，號稱地表最強的 IDE 啦~

補充一下微軟的 C++ 編譯器是[MSVC](https://zh.wikipedia.org/zh-tw/Microsoft_Visual_C%2B%2B)，C++的編譯器其中一種，目前也已經被整合到地表最強 IDE 當中(VS 2022)。

## C++ IDE

那有關於要怎麼安裝*Visual Studio 2022*的部分，最快的懶人包就是到[VS 2022 官網](https://visualstudio.microsoft.com/zh-hant/vs/whatsnew/)，下載 Community 的版本(見下圖)，然後就照著 IDE 的指示，就能順利安裝了，如果還有問題可以請教 GOOGLE 大神。

![Community](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/download_VS2022.PNG)

![GOOGLE GOD](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/google.PNG)

---

## C++的第一個程式

那既然都安裝好了 C++的編譯器及 IDE，適時候來嘗試第一個程式，第一個程式不免俗地當然從*Hello World*開始囉~

那我就從 Visual Studio 2022 介面開始，來準備做出第一個 C++的程式。

1. 打開 Visual Studio 2022，並點擊*建立新的專案*的按鈕
   ![Visual Studio 2022](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/hello_step_1.PNG)

2. 微軟都會為新專案建立基本的範本(template)，之後也可以自己擴充想要的範本

   1. (可選)所以可以從紅字的 1 號，透過介面提供的篩選器，找出 C++的範本
   2. 因為我的第一個程式，其目的只是要快速體驗"Hello World"，確認 C++能被成功執行，所以就選擇紅字 2 號的範本
   3. 然後點擊紅字 3 號，前往下一步

   ![New project template](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/hello_step_2.PNG)

3. 這邊是可以設定專案及解決方案的名稱，因為本次目的是要快速體驗，所以這邊就都照 IDE 的預設，直接按建立就好囉

   ![New project setting](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/hello_step_3.PNG)

4. 建立完，就會看到下圖的畫面，IDE 下面的註解也有提供執行程式的方法，那就直接照著 IDE 的指示，執行程式吧

   ![Code](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/hello_step_4.PNG)

5. 下圖是成功執行程式後的畫面

   ![helloworld](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/hello_step_5.PNG)

---

## C++ 編譯設定

在上一個段落，我已經成功執行完了一個 C++程式，那代表 IDE 也幫我用 C++的編譯器(MSVC)去編譯剛剛由 IDE 的 C++範本出來的 C++程式碼，讓這些程式碼變成可執行的檔案(EXE)。

那現在就來看一下 IDE 有做了哪些事情吧。

1. 點擊*本機 Windows 偵錯工具*右邊的小三角形，下面會出現一排列表，選擇裡面的*ConsoleApplication1 偵錯屬性*來點擊

   ![Debug property](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/debug_property.PNG)

2. 在專案屬性頁的視窗裡面，紅框標示出的分別是編譯器幫我們把程式產出的位置，以及 IDE 使用的 C++版本，那版本的部分當然就是選擇我之前決定的 C++ 20(雖然 C++ 23 好像已經要出來了?)，如果有變更任何選項的話，別忘了要在該視窗的下面，按下套用及確定的按鈕，這樣調整才會生效喔

   ![Project Config](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/project_config.PNG)

3. 專案屬性都設定完後，可以執行建置專案(快捷鍵: Ctrl+Shift+B)，來編譯程式碼，IDE 下方的[輸出]視窗可以看到相關 Log，會看到 IDE 顯示的輸出目錄就是剛剛專案屬性裡面的目錄

   ![Build Log](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/build_log.PNG)

4. 打開輸出的目錄，可以看到裡面有 Hello World 的執行檔，然後複製一份到另外的目錄

   ![File Folder](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/executable_file.PNG)

5. 接著打開命令提示字元(CMD)，分別去執行兩個目錄裡面的執行檔，可以看到執行檔順利執行，這樣就是一個可以成功帶著走的執行檔了

   ![CMD](https://github.com/steven715/14th-IT-IRONMAN-DOC/blob/master/Images/cmd_log.PNG)

好的，以上就是第三天的全部內容，明天再繼續奮鬥~

## 參考資料

[GCC official](https://gcc.gnu.org/)
