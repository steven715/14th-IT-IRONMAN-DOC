# 第十一天: C++ 物件 (二)

今天要來進入物件的核心部分: 封裝、繼承、多型，那就開始吧~

## C++ 封裝 (Encapsulation)

C++封裝的定義其實主要是針對裡面成員的存取限制，對於一個類別來說他本身內部會有某些`private`成員變數或函數來處理一些邏輯，而這些邏輯本身應該是要跟外部使用這類別的使用者切開的，這樣也可以避免類別被外部使用者給擾亂

外部使用類別的使用者，只需要關心`public`的成員或函數提供哪些需要的資料即可

## C++ 繼承 (Inheritance)

繼承是讓不同的類別之間，可以傳承其擁有的東西，透過繼承，我們可以不同類別中，重複使用的一些函數或資料，抽出來成一個基底類別，然後讓那些本來的類別繼承這個基底類別，這樣就能消除重複的程式碼了

這邊就接著昨天的範例繼續看繼承吧~

繼承基本用法: `class 繼承類別: 存取限制(public, protected, private) 基底類別`  
`存取限制預設也是為 private`

```
class Fish {
public:
	int body_len = 55;

	void swim()
	{
		cout << "body: " << body_len << endl;
	}

protected:
	int mucle = 10;
};

class Shark : public Fish {
public:
	void jump() {
		cout << "mucle: " << mucle << endl; // 透過繼承，就能使用前面有提到的protected限制的資料或函數
	}
};

int main()
{
	Fish a_fish;
	Shark a_shark;

	a_shark.jump();
	a_shark.swim();	// 繼承讓shark可以用fish的函數
}
```

## C++ 多重繼承

C++ 中是支援多重繼承的，讓類別能繼承多種不同的類別

多重繼承用法: `class 繼承類別: 存取限制(public, protected, private) 基底類別_1, 存取限制 基底類別_2`

```
class Fish {
public:
	int body_len = 55;

	void swim()
	{
		cout << "body: " << body_len << endl;
	}

protected:
	int mucle = 10;
};

class People {
public:
	friend class Shark; // friend 關鍵字可以讓private的成員被其他的類別存取
private:
	int secret_weight = 100;
};

class Shark : public Fish, public People { // 多重繼承宣告
public:
	void jump() {
		cout << "mucle: " << mucle << endl;
	}

	void myFriend(People& people) {
		cout << "secret: " << people.secret_weight << endl; // 存取其他類別的private成員
	}
};

int main()
{
	People people;
	Shark a_shark;

	a_shark.jump();
    // a_shark能呼叫他繼承類別裡面的函數
    a_shark.swim();
	a_shark.myFriend(people);
}
```

## C++ 多型 (Polymorphism)

C++ 物件中的第三個核心就是多型，多型在 C++中有分為靜態跟動態

- 靜態多型(編譯階段): 這個是指之前有提到的多載(overloading)，還有一個是泛型模板(template，之後會再提到)
- 動態多型(執行階段): 透過虛擬函數(virtual)及其衍生類別的複寫

老樣子，一樣是把上面的例子拿下來用

```
class Fish {
public:
	int body_len = 55;

	virtual void swim()
	{
		cout << "body: " << body_len << endl;
	}
};

class Shark : public Fish {
public:
	void swim() {
		cout << "body: Shark" << endl;
	}
};

class WuGuo : public Fish {
public:
	void swim() {
		cout << "body: WuGuo" << endl;
	}
};

int main()
{
	Shark shark;
	WuGuo wuguo;
	Fish* ptr_fish;
	ptr_fish = &shark;
	ptr_fish->swim();
	ptr_fish = &wuguo;
	ptr_fish->swim();
}
```

## C++ 介面

最後來講到一下有關 C++ 的介面，因為小弟我是寫習慣 C#，所以會想找 interface，但實際上 interface 就是剛剛上面提到的 virtual，在 C++ 就會是用個有虛擬函數的類別當成介面囉

---

好啦，那 C++ 物件的基礎部分也就迅速的帶過去囉，明天開始就要來看資料結構了~

## 參考資料

[C++ 繼承](http://www.w3big.com/zh-TW/cplusplus/cpp-inheritance.html#gsc.tab=0)
