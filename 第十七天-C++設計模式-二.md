# 第十七天: C++ 設計模式(二)

昨天介紹完了創建型模式的工廠模式，今天就接著來了解結構型模式的配接器模式囉~

## 配接器模式

配接器用最簡單的例子就是不同國家的充電線有些是 110V 有些是 120V，會需要一個轉接頭來讓兩不同規格的東西可以互相連結，這個東西就是一種配接器(Adapter)

而在軟體的世界，會比較像是有些 API 是只接受 JSON 格式的資料，但是外部的 API 只接受 XML 格式的資料，這時候就需要使用一個配接器串起來

> 我們需要一種方式，為一個功能正確但介面不合的物件建立一個新介面 - 出自 _設計模式的解析與活用_

下面就來看看實際的程式碼囉~

```
// Target
// Cat is interface using by client
class Cat {
public:
	Cat(){}

	virtual string Meow() {
		return "Meow";
	}
};

// Adaptee
// DogMixCat 是一個新的物件，但他的介面無法直接跟Cat的介面相匹配
class DogMixCat {
public:
	DogMixCat(){}

	int Wang() {
		return 999;
	}
};

// Adapter 讓Client可以使用Cat本來的介面，去呼叫DogMixCat的類別
class Adapter : public Cat {
private:
	DogMixCat *mix_;
public:
	Adapter() {
		mix_ = new DogMixCat();
	};

	string Meow() override {
		return to_string(mix_->Wang());
	};
};

void ClientCall(Cat* cat) {
	cout << "Client use: " << cat->Meow() << endl;
}

int main()
{
	Cat* cat = new Cat();
	ClientCall(cat);
	Adapter* adapter = new Adapter();
	ClientCall(adapter);
}
```

上面就是一個 Adapter 模式的範例

而 Adapter 模式是有兩種類型的:

- _物件 Adapter 模式_ : Adapter 相依於本來的介面(Cat)，並包含要被轉換的物件(Adaptee - DogMixCat)
- _繼承 Adapter 模式_ : Adapter 會分別繼承本來的介面跟被轉換的物件

下面就來看看繼承 Adapter 囉~

```
// 繼承Adapter，這邊就只展示Adapter
class Adapter : public Cat , public DogMixCat
{
public:

	string Meow() override {
		return to_string(Wang());
	};
};
```

## 總結

最後就看一下配接器提供了我們什麼樣的優缺點吧

優點:

- 單一職掌原則: 介面轉換的工作交由 Adapter 來做，接口程式或被轉接的物件不需要處理這些工作
- 開放封閉原則: Adapter 類別讓本來的介面或物件不需要修改程式，就能相容不同接口的程式

缺點:

- 程式的複雜度上升，會需要額外新增額外的類別去處理轉接的工作

---

今天就先展示完配接器(Adapter)，明天的話就先從行為模式裡面的策略模式介紹囉~

## 參考資料

[C++設計模式-配接器](https://refactoringguru.cn/design-patterns/adapter)
[設計模式的解析與活用（Design Patterns Explained: A New Perspective on Object-Oriented Design, 2nd Edition）](https://www.books.com.tw/products/0010615145)
