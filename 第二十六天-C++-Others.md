# 第二十六天 C++ Vector, Define, Header file

今天要來看的題目就是之前在二十四天提到的額外項目，但其實是之前第一天在訂主題的時候，忽略到的部分XD

## C++ Vector

C++的`Vector`其實是C++標準程式庫(STL)中的一個類別，是一種可自動擴展容量的陣列，以循序的方式維護變數集合

下面用實際的程式碼介紹一下他的基本應用~

```
#include <iostream>
#include <vector>

using namespace std;

int main()
{
    vector<int> vec_int;

    // Insert element
    vec_int.push_back(100);

    // Insert into the position you want
    // auto 是類似C#跟JS的var，自動變數類型(C++ 11以後的語法)
    // insert會返回vector的iterator
    auto itr = vec_int.insert(vec_int.end(), 3);
    // iterator是指向到陣列的指標，所以下面會回傳iterator的記憶體位址
    cout << "iterator of vector: " << &itr << endl;
    cout << "value of vector: " << *itr << endl;
    vec_int.insert(itr, 99);
    
    // 取得數量
    cout << "Size of vector: " << vec_int.size() << endl;

    // 是否為空，empty實際上是回傳布林
    cout << "Is empty of vector: " << vec_int.empty() << endl;

    // 找最後一個元素
    cout << "Last element: " << *vec_int.rbegin() << endl;

    vec_int.push_back(99999);
    // 刪除最後的元素
    vec_int.pop_back();

    // erase 能刪除特定範圍的元素
    vec_int.push_back(99999);
    auto end_ele = vec_int.end();
    vec_int.erase(end_ele-1);

    vec_int.push_back(7);
    vec_int.push_back(8);
    
    // Use iterator and auto to print the value of vector
    cout << "ALL elements: " << endl;
    for (auto i = vec_int.begin(); i != vec_int.end(); ++i)
    {
        cout << *i << endl;
    }    

    // 清空所有元素
    vec_int.clear();
    cout << "Is empty of vector: " << vec_int.empty() << endl;
}
```

基本上跟之前[第十二天-C++資料結構](https://ithelp.ithome.com.tw/articles/10298002)裡面的陣列相關的實作都很像，但是由C++本身提供的，所以就不需要重造輪子了~

## C++ define

再看`define`之前，要先了解一個名詞`巨集(macro)`，是一種前置處理器指令，就是做文字的替換，在編譯器編譯之前將define定義的變數替換成define的值

下面用程式碼來看一下實際範例

```
#include <iostream>
#define BIG_SIZE 999
#define DEFAULT_NAME "hahaha"
#define Prints(arg) cout << #arg

using namespace std;

int main()
{
	cout << "define value: " << BIG_SIZE << endl;
	cout << "define value 2: " << DEFAULT_NAME << endl;
	Prints("Nice to meet you");
}
```

上面就只簡單介紹數字、字串及函數的用法囉~

## C++ Header file

最後來看看Header file，在程式中我們也是使用巨集的`include`指令來引入我們需要的lib程式庫

在Header file裡面會去定義要Export出去的介面，用下面的範例來看

假設新增了一個`demo.h`的標頭檔:

```
#include <string>

class Demo
{
public:
	std::string ImportantWords();
};
```

類別裡面的函數實際定義會寫在`demo.cpp`:

```
#include "demo.h"

std::string Demo::ImportantWords()
{
    return "This important words from other library";
}
```

而在client端，只需要將標頭檔引入，就可以使用到裡面的實作

```
#include <iostream>
#include "demo.h"

using namespace std;

int main()
{
	Demo demo;
	cout << demo.ImportantWords() << endl;
}
```

---

今天就是連假的最後一天，想不到竟然還再寫文章，真的是有股淡淡的哀傷，但就剩下4天了，耶~

## 參考資料

[Vector - wiki](https://zh.wikipedia.org/zh-tw/Vector_(STL))
[C++ 速查手冊 巨集](http://kaiching.org/pydoing/cpp/cpp-macro.html)
[C++ 速查手冊 引入標頭檔](http://kaiching.org/pydoing/cpp/cpp-include.html)
