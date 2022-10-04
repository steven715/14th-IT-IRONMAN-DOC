# 第十六天: C++ 設計模式(一)

今天來看看[設計模式](<https://zh.wikipedia.org/zh-tw/%E8%AE%BE%E8%AE%A1%E6%A8%A1%E5%BC%8F_(%E8%AE%A1%E7%AE%97%E6%9C%BA)>)~

設計模式是*對軟體設計中普遍存在（反覆出現）的各種問題，所提出的解決方案*

設計模式是物件導向的延伸應用，也是當今很多軟體都會使用的模式，所以要寫好程式，設計模式也是需要了解的

設計模式的書名: `設計模式:可復用物件導向軟體的基礎 (Design Patterns - Elements of Reusable Object-Oriented Software)` - 1994 年出版

設計模式裡面有很多種(1994 年時有 23 種，現在更多)，裡面主要有三種類型: `創建型模式`, `結構型模式`, `行為模式`

---

## 工廠方法

那第一個設計模式就由[工廠方法](https://refactoringguru.cn/design-patterns/factory-method/cpp/example#lang-features)開始吧

工廠方法是`一種創建型的設計模式，解決了在不指定具體類的情況下創建產品物件的問題`

那下面就來實際看一下程式碼囉:

```
class Cat {
public:
	virtual string Meow() = 0;
};


class BigCat : public Cat {
public:
	string Meow() override {
		return "Meow Meow";
	}
};

class SmallCat : public Cat {
public:
	string Meow() override {
		return "Meow";
	}
};

Cat* Cat_Factory(int type) {
	switch (type)
	{
	case 1:
		return new BigCat;
	case 2:
		return new SmallCat;
	default:
		break;
	}
}


int main()
{
    // 下面的寫法，我需要知道具體是哪種貓
	BigCat bigcat;
	cout << bigcat.Meow();
	SmallCat smallcat;
	cout << smallcat.Meow();

    // 透過工廠方法，工廠會返回訂好的貓貓給我
    cout << "Give me a big cat: " << Cat_Factory(1)->Meow() << endl;
	cout << "Give me a small cat: " << Cat_Factory(2)->Meow() << endl;
}
```

上面介紹的是`工廠方法`，透過函數來返回具體類

## 工廠模式

下面就來延伸為`工廠模式`，有一個*工廠類別*來做剛剛的工廠方法的事

```
class Factory {
public:
	virtual Cat* Create() = 0;
};

class BigFactory : public Factory {
public:
	Cat* Create() override {
		return new BigCat();
	}
};

class SmallFactory : public Factory {
public:
	Cat* Create() override {
		return new SmallCat();
	}
};

int main()
{
    Factory* big_cat_factory = new BigFactory();
	cout << "Big cat factory create: " << big_cat_factory->Create()->Meow() << endl;
	Factory* small_cat_factory = new SmallFactory();
	cout << "Small cat factory create: " << small_cat_factory->Create()->Meow() << endl;
}
```

這邊工廠模式分類成不同品種的貓交給不同的具體工廠來生產

## 抽象工廠模式

最後是抽象工廠模式，如果今天是有多種種類的產品，會再將工廠類別抽象一層出來

```
// 假設狗狗是新產品
class Dog {
public:
	virtual string Wang() { return ""; };
};


class BigDog : public Dog {
public:
	string Wang() override {
		return "Wang Wang";
	}
};

class SmallDog : public Dog {
public:
	string Wang() override {
		return "Wang";
	}
};

class Factory {
public:
	virtual Cat* CreateCat() = 0;
	virtual Dog* CreateDog() = 0;
};

class BigFactory : public Factory {
public:
	Cat* CreateCat() override {
		return new BigCat();
	}
	Dog* CreateDog() override {
		return new BigDog();
	}
};

class SmallFactory : public Factory {
public:
	Cat* CreateCat() override {
		return new SmallCat();
	}
	Dog* CreateDog() override {
		return new SmallDog();
	}
};

int main()
{
    Factory* big_factory = new BigFactory();
	cout << "Big factory create cat: " << big_factory->CreateCat()->Meow() << endl;
	cout << "Big factory create dag: " << big_factory->CreateDog()->Wang() << endl;
	Factory* small_factory = new SmallFactory();
	cout << "Small factory create cat: " << small_factory->CreateCat()->Meow() << endl;
	cout << "Small factory create dag: " << small_factory->CreateDog()->Wang() << endl;
}
```

## 總結

|      | 簡單工廠方法                                                                                                                      | 工廠模式                           | 抽象工廠                                                                                                                                                                                     |
| ---- | --------------------------------------------------------------------------------------------------------------------------------- | ---------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 優點 | 簡單快速                                                                                                                          | 遵守*開放封閉原則*                 | 能夠確保多種產品跟工廠的關係，遵守*開放封閉原則*，遵守[單一職責原則(Single responsibility principle)](https://zh.wikipedia.org/zh-tw/%E5%8D%95%E4%B8%80%E5%8A%9F%E8%83%BD%E5%8E%9F%E5%88%99) |
| 缺點 | 違反[開放封閉原則(Open-Close)](https://zh.wikipedia.org/zh-tw/%E5%BC%80%E9%97%AD%E5%8E%9F%E5%88%99)，每次多一個類別，都要修改方法 | 新增一個產品，同時也要新增一個工廠 | 新增一個產品要改動的複雜度會上升很多                                                                                                                                                         |

---

今天介紹完三種工廠，也是創建型模式的其中一種，明天就來介紹結構型模式的配接器模式(十分常用)~

## 參考資料

[C++ 設計模式](https://refactoringguru.cn/design-patterns/cpp)
