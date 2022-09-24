# 第十天: C++ 物件 (一)

今天要來認識物件，一個讓程式變得靈活的東西~

## C++ 類別

物件(object)是類別(class)的實體(instance);類別(class)是物件(object)的模板(template)

上面這兩句話，如果用現實生活作比喻的話就是 鯛魚燒這個食物是一個`物件`，而製作鯛魚燒的模具就是那個`類別`，那倒進去的奶油可以想像成是建立物件的`建構子`(constructor，這個後面一點會提到)

那剛剛講到的是類別的外部，那在類別的內部就是這個類別會有哪些*成員*(member)，這些成員就是這個類別會擁有的資料(基本資料型別)或是函數

而這些成員也有存取限制，有三種權限: `public`, `private` 和 `protected`

- public: 能被物件以及使用物件的地方使用
- private: 只能在物件內被使用
- protected: 只能在物件內被使用，也可以被繼承(inheritance)該物件的物件使用

`如果沒有定義存取限制，預設都是 *private*`

下面來看一下怎麼去宣告一個類別，有兩種: 第一種是直接宣告物件變數；第二種是在其他的地方去宣告一個物件變數:

```
class Fish {
public:
	int body_len;
	void swim() {
		cout << "i can swim";
	}

private:
	double fishbone;
} big_fish; // first declaration

int main()
{
	Fish shark; // second declaration
	shark.body_len = 20;

    big_fish.body_len = 99;

	cout << "shark body len is: " << shark.body_len << endl;
    cout << "big_fish body len is: " << big_fish.body_len << endl;
	shark.swim();

}
```

## C++ 建構子/解構子

認識完了類別及物件怎麼宣告了後，現在來看看建構子與解構子(constructor and destructor):

下面直接延續上面的範例:

```
class Fish {
public:
	int body_len;
	void swim() {
		cout << "i can swim" << endl;
	}

    // Constructor: 在這邊定義物件成員的初始狀態
	Fish(){
		body_len = 1;
		fishbone = 80.2;
	}

    // Destructor: 在物件消失時，會執行裡面的內容
	~Fish() {
		cout << "bye~" << endl;
	}

private:
	double fishbone;
} big_fish;

int main()
{
	Fish shark;
	/*shark.body_len = 20;

	big_fish.body_len = 99;*/

	cout << "shark body len is: " << shark.body_len << endl;
	cout << "big_fish body len is: " << big_fish.body_len << endl;
	shark.swim();

    // 在main函數結束時，會呼叫兩次Fish的destructor函數
}
```

下面再多一個新的東西: 多載(overloading)

多載可以讓我們透過同樣名字的函數，定義這個函數需要的不同參數類型或返回的資料類型，讓我們擁有更靈活的函數運用。

一樣再以上面的例子來看:

```
class Fish {
public:
	int body_len;

	Fish(){
		body_len = 1;
	}

    // overloading: 不一定只有上面建構子預設的數值，也可以透過多載讓使用者自定義預設數值
	Fish(int body) {
		body_len = body;
	}
} ;

int main()
{
	Fish shark;
	Fish overloading_fish(50);

	cout << "shark body len is: " << shark.body_len << endl;
	cout << "overloading_fish body len is: " << overloading_fish.body_len << endl;
}
```

最後再來講一個物件裡面很重要的部分，`this` 指標，這個指標存的就是物件本身的記憶體位址，透過 this，就可以從物件中的成員函數取得成員變數或其他成員函數:

```
class Fish {
public:
	int body_len;

	Fish(){
		body_len = 1;
	}

	void swim()
	{
		cout << "body: " << this->body_len << endl; // 透過this指針取得物件內部其他成員
		cout << "body: " << body_len << endl;  // 另一種寫法，但在編譯器中也還是上面的形式取值
	}

	Fish* myself()
	{
		return this;
	}

	Fish& my_address()
	{
		return *this;
	}
} ;

int main()
{
	Fish shark;

	shark.swim();
	cout << "address of shark is: " << shark.myself() << endl; // this 就是指標，所以會返回記憶體位址
	Fish dd = shark.my_address();  // 這邊是返回的是shark的物件的值，然後賦值到dd上面
	Fish* new_dd = shark.myself(); // 還記得之前講的指標嗎，指標也可以是類別指標

    // dd就是新的fish物件跟shark已經是不同的物件
	dd.body_len = 99;
	shark.swim();
	dd.swim();

    // 下面的new_dd這個類別指標實際是指向shark，所以new_dd改動的值，也會連同影響到shark
	new_dd->body_len = 77;
	new_dd->swim();
	shark.swim();
}
```

---

今天看完了 C++ 物件的類別/實體、存取器、建構子/解構子以及多載，算是物件的起頭而已，明天會是物件的核心部分，代表物件的三大特徵: 封裝、繼承、多型。

## 參考資料

[C++ 類別](http://kaiching.org/pydoing/cpp/cpp-class.html)
[C++ 物件導向](http://disp.ee.ntu.edu.tw/class/C++%E7%89%A9%E4%BB%B6%E5%B0%8E%E5%90%91%E5%8F%8A%E5%A2%9E%E9%80%B2%E6%95%88%E7%8E%87%E7%A8%8B%E5%BC%8F%E6%8A%80%E5%B7%A7)
