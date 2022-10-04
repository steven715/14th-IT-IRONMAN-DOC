# 第十九天: C++ 設計模式(四)

今天要來介紹的是觀察者模式，這個模式其實是個平常常常使用的模式，最簡單的像是網站上面的JavaScript，上面寫的Function被促發是根據HTML裡面的Element對應的Event(Click, Hover..)，這些都是觀察者模式的一種實作(Implement)

## 觀察者模式

首先，先來看一下他的定義~

> 定義物件間一種一對多的依賴關係，使得每當一個物件改變狀態，則所有依賴於它的物件都會得到通知更自動更新

所以基本上觀察者模式應該至少會有兩種腳色: 觀察者(Observer), 被觀察者(Subject)

當`被觀察者(Subject)`狀態改動了，它會通知它的`觀察者(Observer)`，然後觀察者做出相對應的`反應(Update)`

有了這個觀念就直接來看看程式碼囉~

```
class IOberser {
public:
	virtual void Update() = 0;
};

class ISubject {
public:
	virtual void Attach(IOberser *observer) = 0;
	virtual void Detach(IOberser* observer) = 0;
	virtual void Notify() = 0;
};

class Cat : public ISubject {
public:
	void Attach(IOberser* observer) override {
		list_observer_.push_back(observer);
	}

	void Detach(IOberser* observer) override {
		list_observer_.remove(observer);
	}

	void Notify() override {
		std::list<IOberser *>::iterator iterator = list_observer_.begin();

		while (iterator != list_observer_.end())
		{
			(*iterator)->Update();
			++iterator;
		}
	}

	void Pee() {
		cout << "I pee pee" << endl;
		Notify();
	}

private:
	list<IOberser*> list_observer_;
};

class Man : public IOberser {
public:
	void Update() override {
		cout << "Oh no~" << endl;
	}
};

class Women : public IOberser {
public:
	void Update() override {
		cout << "Oh cute~" << endl;
	}
};

int main()
{
	Cat* cat = new Cat;
	IOberser* man = new Man;
	IOberser* women = new Women;
	
	cat->Attach(man);
	cat->Attach(women);
	cat->Pee();
	cat->Detach(man);
	cat->Pee();
}
```

上面的程式碼作法是讓被觀察者(Subject)去存它的觀察者(Observer)們，然後當它(Subject)做了動作，就去通知(Notify)Observer去更新(Update)

而實務上，也有一種做法是Publisher-Subscriber(簡稱Pub-Sub)，Pub相當於Subject，Sub則是Observer，這種作法中間會有個像是`中間人(Broker)`，把Subject存Observer的工作拿來做，解偶觀察者與被觀察者的依賴關係

---

## 中介者模式

`中介者(Mediator)`是用一個中介物件來封裝一系列的物件互動，讓各物件不需要相互引用，使其耦合松散

下面就來看看程式碼吧~

```
class BasePartner;
class Mediator {
public:
	virtual void Notify(BasePartner* sendor, int event_type) = 0;
};

class BasePartner {
protected:
	Mediator* mediator_;
public:
	BasePartner(Mediator *mediator = nullptr) : mediator_(mediator) {}
	void set_mediator(Mediator* mediator) {
		this->mediator_ = mediator;
	}
};

class PartnerA : public BasePartner {
public:
	void Report() {
		cout << "Partner A report" << endl;
		this->mediator_->Notify(this, 1);
	}

	void Recive() {
		cout << "Partner A receive money" << endl;		
	}
};

class PartnerB : public BasePartner {
public:
	void Report() {
		cout << "Partner B report" << endl;
		this->mediator_->Notify(this, 2);
	}

	void Recive() {
		cout << "Partner B receive money" << endl;
	}
};

class Account : public BasePartner {
public:
	void CountMoney() {
		cout << "Account accounting money" << endl;
		this->mediator_->Notify(this, 3);
	}

	void Praised() {
		cout << "Boss praised Account" << endl;
	}
};

class Boss : public Mediator {
private:
	PartnerA* partner_a_;
	PartnerB* partner_b_;
	Account* partner_c_;
public:
	Boss(PartnerA* p1, PartnerB* p2, Account* p3) : partner_a_(p1), partner_b_(p2), partner_c_(p3) {
		this->partner_a_->set_mediator(this);
		this->partner_b_->set_mediator(this);
		this->partner_c_->set_mediator(this);
	}

	void Notify(BasePartner* sendor, int event_type) override {
		if (event_type == 1)
		{
			cout << "Boss handle partner A report" << endl;
			this->partner_c_->CountMoney();
			this->partner_a_->Recive();
		}
		if (event_type == 2)
		{
			cout << "Boss handle partner B report" << endl;
			this->partner_c_->CountMoney();
			this->partner_b_->Recive();
		}
		if (event_type == 3)
		{
			cout << "Boss handle account message" << endl;			
			this->partner_c_->Praised();
		}
	}
}; 


int main()
{
	PartnerA* partner_A = new PartnerA;
	PartnerB* partner_B = new PartnerB;
	Account* partner_C = new Account;
	Boss* mediator = new Boss(partner_A, partner_B, partner_C);

	partner_A->Report();
	cout << "--------" << endl;
	partner_B->Report();
}
```

上面的程式碼，用員工跟老闆還有會計之間做個例子:

假設員工做完工作，就去找會計拿錢，那同時兩個員工找會計的話，會讓會計手忙腳亂，這時就需要一個中介者(假設為老闆)，讓每個人做好自己的工作，做完事就像中介者回報即可，那這樣溝通的工作就交給中介者來處理

---

今天的觀察者跟中介者都屬於行為模式中的溝通類型，那明天就再接著之前的結構型模式的裝飾者囉~

## 參考資料

[設計模式 - 觀察者模式](https://refactoringguru.cn/design-patterns/observer)
[設計模式 - 中介者模式](https://refactoringguru.cn/design-patterns/mediator)
