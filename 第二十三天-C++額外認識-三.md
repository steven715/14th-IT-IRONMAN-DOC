# 第二十三天: C++ 額外認識-三

今天來介紹 C++ 的其他部分，`垃圾回收`跟`多執行緒`~

## 垃圾回收

首先來了解一下什麼是垃圾回收

垃圾回收是 `一種自動的記憶體管理機制`，而在 C++ 裡面其實是沒有這種機制的，原因是 C++ 的作者出於 C++是一個底層的語言，所以記憶體管理應該是由程式員自己管理

所以實際上 C++在垃圾回收上，可以用某些特定的手法來實現垃圾回收這件事(就是將用不到的物件或變數清除掉)，下面就是一個簡單的透過智能指標來實現垃圾回收的範例

```
class Ptr {  // 實作智慧型指標的類別
	int* ptr;
public:
	explicit Ptr(int* p = NULL) { ptr = p; }  // 將指標儲存起來
	~Ptr() { delete(ptr); }  // 回收記憶體
	int& operator *() { return *ptr; }  // 多載化 * 運算子
};
int main() {
	Ptr ptr(new int());
	*ptr = 4;
	cout << *ptr;
	// 智慧型指標會自動回收記憶體
	return 0;
}
```

## C++ 多執行緒

在 C++ 的多執行緒，用的是`thread`這個 C++ 11 出來的 API

下面就用一個簡單的例子來看看囉

```
#include <thread>

using namespace std;

void SomeFunc() {
	cout << "Some Func" << endl;
}

int main()
{
	// 建立一個執行緒去執行一個函式
	thread v1(SomeFunc);
	// 執行緒配函式代參數
	thread v2(SomeFuncWithArgu, 1);

	// 等待執行緒結束
	v1.join();
	v2.join();
}
```

---

今天剛好是連假開始，而這周身體實在太疲憊了><(藉口 哈哈哈) 所以今天的內容就稍稍少了一點，就在剩餘的天數再補上囉~

## 參考資料

[垃圾回收 - 維基](<https://zh.wikipedia.org/zh-hant/%E5%9E%83%E5%9C%BE%E5%9B%9E%E6%94%B6_(%E8%A8%88%E7%AE%97%E6%A9%9F%E7%A7%91%E5%AD%B8)>)
[C++ 為什麼不加入垃圾回收機制](https://zi.media/@twpetsearcharlinksnet/post/amyAw7)
[C++ std::thread 建立多執行緒用法與範例](https://shengyu7697.github.io/std-thread/)
