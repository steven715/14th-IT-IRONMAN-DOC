# 第四天: C++ 基本認識 (一)

今天要來認識 C++這項語言，那要認識一個語言，當然就要從其基礎開始。

那其實語言實際上就是人類把要給電腦做的事情寫出來，然後透過編譯器讓電腦去執行，而電腦的本質就是來處理資料(運算資料、保存資料等等)。

基於這項本質，基礎的部分，我選擇先從變數及基本資料型別開始。

## C++ 變數

變數是一個保存資料的地方(保存在記憶體)，那會有哪些資料型態呢?

這邊先簡單介紹以下幾種:

- int: 存放整數類型的數字，像是 111, -22
- double: 存放有小數點的數字，像是 22.1, -20.1
- char: 存放單一字元，像是'a', 'c'. 會以單逗號來包起來
- string: 存放文字，像是"Hello World". 會以雙逗號包起來
- bool: 存放是或否兩種狀態值: true, false

C++是屬於[強型別](https://learn.microsoft.com/zh-tw/cpp/cpp/cpp-type-system-modern-cpp?view=msvc-170)，所以當我們宣告變數時，需要告訴電腦我們要存放的變數是什麼的資料類別。

語法如下:  
`資料型別 變數名稱 = 值;`  
`type variableName = value;`

Smaple:

```
int my_int = 10;
cout << my_int;
```

## C++ 命名規則

接著來看一下 C++命名規則，一個語言寫出來的程式碼其實是要給人看得，對電腦來說我們寫的東西不過是 0 跟 1，所以這個命名規則就有其必要性，畢竟寫出來的命名之後，之後如果要改也是人去改。

我這邊就照著[Google C++ 開源風格指南](https://tw-google-styleguide.readthedocs.io/en/latest/google-cpp-styleguide/naming.html)，讓我之後的程式碼命名有一致性，這個一致性的重要其實是反應於[程式可讀性](https://zh.wikipedia.org/zh-tw/%E7%A8%8B%E5%BC%8F%E5%8F%AF%E8%AE%80%E6%80%A7)。

那命名就跟著當前進度前進，目前只有變數的命名需要有個規則:

- 通用命名規則: 命名要有描述性；少用縮寫。  
   Good sample:

  ```
  int number_people;  // 看名字就知道是人的數量
  ```

  Bad sample:

  ```
  int x;  // 意義不明，讓人不好理解
  ```

- 變數命名: 變數名一律小寫，單詞之間用底線連接，如:
  ```
  int number_total;
  string customer_name;
  ```

## C++ 基本資料型態

C++的基本內建型態(primitive built-in type)為以下四類:

| 資料型態      | 大小            | 描述                                                                       |
| ------------- | --------------- | -------------------------------------------------------------------------- |
| 布林(boolean) | 1 位元組(byte)  | 存放 true 或 false 值                                                      |
| 字元(char)    | 1 位元組(byte)  | 存放單個字符/字母/數字，或 [ASCII 值](https://zh.wikipedia.org/wiki/ASCII) |
| 整數(int)     | 4 位元組(bytes) | 存放無小數點的數字                                                         |
| 浮點數(float) | 4 位元組(bytes) | 存放有小數點的數字                                                         |

`註: 1個位元組(byte)有8個位元(bit)，每一個位元表示0或1的二進位數字`

---

那今天的進度就先到基本資料型態的部分，這兩天台灣發生很多的地震，希望大家都平安無事，天佑台灣~

## 參考資料

[W3C C++ 課程](https://www.w3schools.com/cpp/cpp_data_types.asp)
[C++ 入門指南 基本內健型態](http://kaiching.org/pydoing/cpp-guide/unit-3-primitive-built-in-type.html)
