# 第十五天: C++ 測試框架 (二)

今天延續昨天的 GTest 專案，昨天有先試著跑了一下 GTest 出來的樣子，那今天就來試試看更多的東西吧~

## C++ GTest Unit Test

那這邊就來之前 C++類別的例子來參考:

假設現在有一個魚的類別，程式碼如下:

```
class Fish
{
public:

	Fish(int age)
	{
		this->age_ = age;
	}

	int Get_age()
	{
		return age_;
	}
private:
	int age_;
};
```

上面可以看到魚類別的建構子，現在我們要限制魚的年齡需要大於 0，那我會寫下測試來測試這件事:

```
TEST(FishBehaver, FishAgeGreaterZero) {
	int test_age = 0;
	Fish test_fish = Fish(test_age);
	int target_age = 0;
	EXPECT_TRUE(test_fish.Get_age() > target_age);
}
```

然後執行測試，會發現下圖的結果，一開始就測試失敗了，但這其實才是測試驅動開發重要的第一步: `紅燈`  
先透過一個失敗，我們才能定下要怎麼確定正常

[test_failed]

然後我們就要做測試驅動開發的第二步: `綠燈`  
這邊我們就調整一下前面魚的建構子，讓這個失敗的測試能快速通過

```
// 只調整建構子的部分
Fish(int age)
	{
		this->age_ = age <= 0 ? 1 : age;
	}
```

調整完後再執行一次測試，就能看到我們的測試如下通過了

[test_pass]

而在測試驅動開發的第三步: `重構`  
這邊礙於主題跟篇幅的關係，就不多討論太多

更多的內容可以參考[重構 改善既有程式的設計](https://www.books.com.tw/products/0010825896)

那以上就是簡單的測試驅動開發的概念應用在一個超小型的 C++ Unit Test

測試驅動開發三口訣: `紅燈` -> `綠燈` -> `重構`

---

那 C++ 測試的部分就先到這邊，簡單的快速帶過，哈哈哈哈，最近工作疲勞轟炸，實在有點有心無力...  
但我會在下一個部分 C++設計模式回來的~

## 參考資料

[Kent Beck 的測試驅動開發](https://www.books.com.tw/products/0010883019)
