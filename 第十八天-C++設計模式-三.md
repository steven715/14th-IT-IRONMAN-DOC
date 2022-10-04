# 第十八天: C++ 設計模式(三)

那今天就來介紹行為模式裡面的策略模式吧~

那再介紹策略模式之前，我小小補充一下設計模式的三種分類

- 創建型模式: 提供創建物件的機制，提升已有程式碼的靈活性和可復用性
- 結構型模式: 如何將物件及類別組成較大的結構，並同時保持結構的靈活和效率
- 行為模式: 負責物件之間的效率溝通和職責委派

## 策略模式

策略模式(Strategy Pattern): 能夠定義一系列的演算法，並將每種演算法放入獨立的類別，使演算法的物件可以相互替換

先來看一下程式碼範例，很多時候，如果遇到不同情況的條件，我們會使用`switch`這個條件來判斷要用什麼樣對應行為

```
class Cat {
public:
	void Meow(int cat_type) {
		switch (cat_type)
		{
		case 1 :
			cout << "i am white cat " << endl;
            break;
		case 2:
			cout << "i am black cat " << endl;
            break;
		default:
			break;
		}
	}
};

class People {
public:
	void PlayCat(Cat cat) {
		cat.Meow(owned_cat_type_);
	}

	int owned_cat_type_ = 1;
};

int main()
{
	People* people = new People();
	Cat* cat = new Cat();

	people->PlayCat(*cat);
}
```

那 Strategy Pattern 的思路就是將 switch 裡面的各個演算法抽離成不同的類別

```
class Action {
public:
	virtual void Meow() = 0;
};

class WhiteAction : public Action {
public:
	WhiteAction() {}

	void Meow() override{
		cout << "i am white cat " << endl;
	}
};

class BlackAction : public Action {
public:
	void Meow() override {
		cout << "i am black cat " << endl;
	}
};

class Cat {
public:
	void Meow() {
		action_->Meow();
	}

	// 這邊可以抽換貓貓行為演算法
	void SetAction(Action* action) {
		action_ = action;
	}
private:
	Action *action_;
};

class People {
public:
	void PlayCat(Cat cat, int cat_type) {
		Action* action = GetAction(cat_type);

		cat.SetAction(action);
		cat.Meow();
	}

private:
	Action* GetAction(int cat_type) {
		switch (cat_type)
		{
		case 1:
			return new WhiteAction();
		case 2:
			return new BlackAction();
		default:
			break;
		}
	}
};

int main()
{
	People* people = new People();
	Cat* cat = new Cat();

	// play with white cat
	people->PlayCat(*cat, 1);

	// play with black cat
	people->PlayCat(*cat, 2);
}
```

可以看到策略模式就是將演算法抽離出來，根據使用者所需去靈活選擇，所以通常應用在演算法需要常常調整的地方，像是一些判斷規則，就可以抽離出來成演算法，透過策略模式封裝演算法，也可以更好利用單元測試去測試各個演算法。

---

那今天我們介紹完了策略模式，明天就來看看觀察者模式囉，這個之前在看前端或寫一些網站的時候，也是一個很常使用到的模式~

## 參考資料

[設計模式 - 策略模式](https://refactoringguru.cn/design-patterns/behavioral-patterns)
