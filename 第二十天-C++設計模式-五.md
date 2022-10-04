# 第二十天: C++ 設計模式(五)

今天就直接來看裝飾者模式囉~

## 裝飾者模式

先來看一下裝飾者(Decorator)的定義: `允許使用者通過將物件放入包含行為的特殊封裝物件中來位元物件綁定新的行為`

可以想像成是一個俄羅斯娃娃，會有很多層包裝在外面，但裡面的東西還是本來的物品

下面就來看看程式碼囉~

```
class IArmor {
public:
	virtual string GetDefense() = 0;
};

class Armor : public IArmor {
public:
	string GetDefense() override {
		return "Zero";
	}
};

class Decorator : public IArmor {
protected:
	IArmor* armor_;
public:
	Decorator(IArmor * armor) : armor_(armor) {}

	string GetDefense() override {
		return this->GetDefense();
	}
};

class ChainMail : public Decorator {
public:
	ChainMail(IArmor * armor) : Decorator(armor) {}
	string GetDefense() override {
		return "Plus strong " + armor_->GetDefense();
	}
};

class Commoner : public Decorator {
public:
	Commoner(IArmor* armor) : Decorator(armor) {}
	string GetDefense() override {
		return "Plus little " + armor_->GetDefense();
	}
};

int main()
{
	IArmor* armor = new Armor;
	cout << "Armor: " << armor->GetDefense() << endl;

	IArmor* chain_plus = new ChainMail(armor);
	cout << "Chain mail plus armor : " << chain_plus->GetDefense() << endl;

	IArmor* commoner_chain_plus = new Commoner(chain_plus);
	cout << "Chain mail plus armor : " << commoner_chain_plus->GetDefense() << endl;
}
```

上面的程式碼中可以看到本來的Armor類別的函數是沒被影響的，而且我們可以透過Decorator的具體類別去擴充本來的Armor類別，而不去影響到本來的Armor類別


---

## 命令模式

在設計模式的最後，我們來看看行為模式裡面的命令模式

一樣先從其定義了解: 命令模式可將請求轉換為一個包含與請求相關的所有訊息的獨立物件。

以現實生活的例子，就像是在餐廳裡面，服務生幫客人點餐會使用紙筆作紀錄，然後再交給廚師去做料理，那指筆就是命令模式的物件。

所以會有`觸發者(Invoker)`, `命令(Command)`, `接收者(Receiver)`三種物件分別擁有各自的職責

下面就來看看程式碼吧

```
class Command {
public:
	virtual void Execute() = 0;
};

class ChefReceiver {
public:
	void Action(string dish_name) {
		cout << "I made the " << dish_name << endl;
	}
};

class CurryCommand : public Command {
private:
	ChefReceiver* receiver_;
public:
	CurryCommand(ChefReceiver* chef_receiver) : receiver_(chef_receiver) {}
	void Execute() override {
		receiver_->Action("Curry");
	}
};

class WaiterInvoker {
public:
	void Notify(Command* command) {
		command->Execute();
	}
};

int main()
{
	ChefReceiver* chef = new ChefReceiver;
	Command* command = new CurryCommand(chef);
	WaiterInvoker* waiter = new WaiterInvoker;
	waiter->Notify(command);
}
```

上面就是透過餐廳點餐的例子展示命令模式囉

---

今天把設計模式預定地範圍都介紹完了，還有一些也很常用的模式(Singleton, Template, State等等)就留到預定地範圍都介紹完，最後的幾天再來看完吧~


## 參考資料

[設計模式 - 裝飾者模式](https://refactoringguru.cn/design-patterns/decorator)
[設計模式 - 命令模式](https://refactoringguru.cn/design-patterns/command/cpp/example#lang-features)
