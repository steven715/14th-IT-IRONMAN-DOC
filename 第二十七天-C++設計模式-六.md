# 第二十七天 C++ 設計模式 - 六

二十七天又回來到設計模式，哈~ 今天來補充一些之前在[第二十天 C++ 設計模式 五]()最後提到要講的模式

## 單例模式

單例模式(Singleton)是一種創建型設計模式，用來確保我們的類別一次只會有一個實例(instance)

那什麼時候會需要這個東西呢? 有一個例子是`時鐘`，如果程式中有很多時鐘，每個如果都給不同時間，會導致溝通出嚴重的問題，像這類需要統一規範的類別就可以使用`單例模式`

下面就來看看程式囉~

```
#include <iostream>
#include <ctime>
#include <string>

using namespace std;


// Meyers Singleton (單例模式的一種實作)
class ClockSingleton
{
public:

	static ClockSingleton& GetInstance()
	{
		static ClockSingleton instance;
		return instance;
	}

	string GetTime()
	{
		// 取得當前系統時間
		time_t t = time(0);   
		
		// tm 是C/C++中的時間結構
		tm now;

		localtime_s(&now, &t);

		return to_string(now.tm_year + 1900) + '-' + to_string(now.tm_mon + 1) + '-' + to_string(now.tm_mday);
	}
private:
	ClockSingleton() {}
};

int main()
{
	ClockSingleton &clock = ClockSingleton::GetInstance();
	cout << clock.GetTime() << endl;
	// 無法用一般方式初始化
	//ClockSingleton* clock = new ClockSingleton();
}
```

## 模板方法模式

模板方法是屬於行為的設計模式，他在基底類別定義了一些演算法的框架，允許子類別在不修改結構的情況下可以重寫演算法的特定步驟

簡單來說就是如果今天有三個類別同時做著很類似的事，可以把這些重複的事情抽出來成一個基底類別成為一個模板，之後三個類別只要根據自己要調整的部分做複寫即可

下面就來個範例程式囉~

```
class AbstractClass {
public:
    void TemplateMethod() const {
        this->BaseOperation1();
        this->RequiredOperations1();
        this->BaseOperation2();
        this->RequiredOperation2();
        this->BaseOperation3();
    }

protected:
    void BaseOperation1() const {
        cout << "AbstractClass says: I am doing the bulk of the work" << endl;
    }
    void BaseOperation2() const {
        cout << "AbstractClass says: But I let subclasses override some operations" << endl;
    }
    void BaseOperation3() const {
        cout << "AbstractClass says: But I am doing the bulk of the work anyway" << endl;
    }

    virtual void RequiredOperations1() const = 0;
    virtual void RequiredOperation2() const = 0;
 
};

class ConcreteClass1 : public AbstractClass {
protected:
    void RequiredOperations1() const override {
        cout << "ConcreteClass1 says: Implemented Operation1" << endl;
    }
    void RequiredOperation2() const override {
        cout << "ConcreteClass1 says: Implemented Operation2" << endl;
    }
};

class ConcreteClass2 : public AbstractClass {
protected:
    void RequiredOperations1() const override {
        cout << "ConcreteClass2 says: Implemented Operation1" << endl;
    }
    void RequiredOperation2() const override {
        cout << "ConcreteClass2 says: Implemented Operation2" << endl;
    }
};

int main() {
    ConcreteClass1* concreteClass1 = new ConcreteClass1;
    concreteClass1->TemplateMethod();
    ConcreteClass2* concreteClass2 = new ConcreteClass2;
    concreteClass2->TemplateMethod();
    return 0;
}
```

---

今天時間不太夠>< 就先簡單介紹了一下單例模式跟模板方法模式，明天再繼續補完狀態模式囉~

## 參考資料

[C++ 設計模式](https://refactoringguru.cn/design-patterns/cpp)
[C++ 日期](https://www.runoob.com/cplusplus/cpp-date-time.html)
[C++ 單例模式](https://shengyu7697.github.io/cpp-singleton-pattern/)
