# 第十四天: C++ 測試框架

在軟體開發中測試一直都是一件十分重要的事，尤其是近年的測試驅動開發(Test-Driven Development)熱度十分火紅，相關好書[Kent Beck的測試驅動開發](https://www.books.com.tw/products/0010883019)

## C++ 測試框架

那這邊的測試框架會介紹兩個: GTest, CppUnit 

會介紹這兩個主要是因為Visual Studio 2022裡面測試框架只有這兩個，哈~

### GTest

*GTest* 全名為 `GoogleTest`，看名字就知道是Google推出的，為了C++而做的測試框架，此外這專案也是開源的，[GTest Github](https://github.com/google/googletest)。

這邊就來簡單的做一個GTest的測試專案玩玩吧

### 新增GTest 專案

1. 那一樣就接著一開始的Hello World專案，從方案的地方按右鍵，然後選擇圖二*紅字1*的加入按鈕，再按*紅字2*的新增專案

圖一[project_tree]
圖二[add_new_project]

2. 新增專案的視窗，使用篩選器輸入`測試`，語言選`C++`，就可以看到 *原生單元測試專案* 跟 *Google Test* ，那這邊就先選擇 *Google Test*。

[test_project]

3. 之後會看到設定新的專案，這邊就先都照著預設走，按右下角的建立就好

[setting]

4. 然後會看到測試專案組態，這邊選擇之前那個測試專案，然後點選*OK*，就會完成新的Google Test專案囉

[config]


### 第一個單元測試

那建立完測試專案之後，當然就是要開始做測試囉~

在測試專案裡面，我們做的測試是[單元測試(Unit Testing)](https://zh.wikipedia.org/zh-tw/%E5%8D%95%E5%85%83%E6%B5%8B%E8%AF%95)，單元測試簡單來說就是以我們所寫的函數(function)為單位來測試

那就準備來試試第一個單元測試囉~

1. 首先對方按按右鍵，然後選擇最下面的屬性

[setting_solution]

2. 將單一起始專案選擇成現在的測試專案

[start_point]

3. 測試專案中*test.cpp*，其實就已經有了測試的程式，我們這邊就可以透過*F5*來執行第一個單元測試了，就會看到下圖的測試結果囉

[test_result]

---

今天先簡單介紹一下GTest以及其用法，明天再補充更多一點的細節以及另外一個CppUnit的用法~

## 參考資料

[C++測試框架介紹](https://ithelp.ithome.com.tw/articles/10106155)
