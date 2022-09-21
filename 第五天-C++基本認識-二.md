# 第五天: C++ 基本認識 (二)

今天就從上次的資料型態來開始延續。

## C++ 基本資料型態

C++ 的[基本內建型態](https://learn.microsoft.com/zh-tw/cpp/cpp/fundamental-types-cpp?view=msvc-170)有四種: 布林、字元、整數跟浮點數，下面我就照順序來輪流看一遍吧。

---

### 布林

布林型態的資料是用來存 true 或 false，且使用 1 個位元組的記憶體來存資料。

布林的變數宣告:

```
bool i_am_true = true;
bool i_am_flase = false;
```

除了直接給予 true 或 false，也可以表示為*1*或*0*，另外布林型態也支援運算式。

```
bool i_am_true_2 = 1; // true
bool i_am_false_2 = 0; // false
bool i_am_true_3 = 33 > 1; // true
bool i_am_false_3 = 9 > 888; // false
```

`小知識: 布林雖然是1或0，用1 bit就可以存，但實際在記憶體是0000 0001 或0000 0000。`
[小知識來源](https://www.youtube.com/watch?v=e3Osi9cUeRQ&list=PLhGp6N0DI_1TzGLCbiF0oYxbckUR9mXra&index=10)

---

### 字元

字元是用來存單個字符/字母/數字，或是定義在[ASCII](https://zh.wikipedia.org/wiki/ASCII)的符號

ASCII 裡面會有分為控制字元跟可顯示字元。

#### 可顯示字元

可顯示字元主要對應是鍵盤上會有的英文數字跟一些特殊符號(編號範圍是 32-126):

```
char cha = 'a';
char cha_2 = 'A';
char cha_3 = '1';
// 也可以利用以下轉型語法將ASCII的編號輸出成字元
cout << (char)97; // a，其ASCII的編號為97
cout << (char)65; // A，其ASCII的編號為65
// 由上可以發現英文大小寫是相差32號
// 所以如果要做大小寫轉換也可以利用這個特點
```

#### 控制字元(不可顯示字元)

當 C++把這些整數解讀成 _char_ 輸出，就會執行該 _控制字元_ 的功能

這邊用換行當個例子來介紹:

```
// C++ 的換行功能: endl
cout << 'a' << endl;
// 如果用ASCII的換行符號(\n)也有同樣效果
cout << 'a\n';
```

另外有對 endl 跟換行符號(\n)的差別可以參考[C++ endl vs \n](https://stackoverflow.com/questions/213907/stdendl-vs-n)

---

好了，那看完字元跟布林，今天的進度就先到這邊囉，這周末真的太疲憊了~

## 參考資料

[C++ 教學 BLOG](https://www.csie.ntu.edu.tw/~b98902112/cpp_and_algo/cpp02/character.html)
