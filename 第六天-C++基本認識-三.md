# 第六天: C++ 基本認識 (三)

昨天講到了字元(char)，裡面就是存 ASCII 的編號符號，那除了 char 的字元以外，還有其他的字元型態，今天就從這部分繼續囉~

---

## 字元

知道了字元(char)其實是來處理 ASCII 的編號符號後，其實會發現那邊處裡的符號有限(可顯示字元只有 95 個，裡面就包括大小英文跟數字符號而已)，像是中文或一些外國的文字，ASCII 裡面都沒有涵蓋到。

所以如果是中文這種有是象形文字的語文，那會有非常多字要去配對，也就是需要一個極其龐大的字典，[Unicode](https://zh.wikipedia.org/wiki/Unicode)就是電腦世界來解決顯示所有文字的字典，裡面目前最新版本為 2022.9 月公布的 15.0.0，已經收錄超過 14 萬個字元。

而上面提到的[Unicode](https://zh.wikipedia.org/wiki/Unicode)只是一個表，在電腦中其實是用[UTF-8](https://zh.wikipedia.org/wiki/UTF-8)的編碼模式，這個編碼就是將 Unicode 的碼點給編出來。

這邊就來看看 C++ char 怎麼去處理 Unicode: wchar_t(使用 2 個位元組(byte)，也就是多的一個 byte 會去對應 Unicode 裡面的碼點，其他延伸的字元類型也是如此: 多位元組字元)

```
wchar_t ch = L'林'; // 這種寫法是擴充字元字面常量（wide character literal）
```

這邊就先簡單介紹 wchar_t 是以 Unicode 處理，前置符號是 L。

另外還有 char8_t 是以 UTF-8，前置符號是 u8;char16_t 是以 UTF-16，前置符號是 u;char32_t 是以 UTF-32，前置符號是 U，這幾個部分礙於篇幅，之後有機會再仔細深入的看囉><

--- 

### 字元小知識

char 還有兩個變形: unsigned char 跟 signed char:

因為 char 是來對應 ASCII 的表(0~127)，只有使用 7 bits，多出來的 1 bit 就變成可以表示正負號的 signed(-128~127)或拿來當正整數往下(0~255)的 unsigned。

所以其實這兩種類別主要是拿來當*int*來用的。

---

## 整數

C++ 的整數類別有以下幾種: short, int, long, long long, 還有上面提到的 unsigned char 跟 signed char
前面加上 _unsigned_ 可以讓其變成正整數

| 類型名稱           | 位元組(byte) | 範圍                                       |
| ------------------ | ------------ | ------------------------------------------ |
| signed char        | 1            | -128 ~ 127                                 |
| short              | 2            | -32768 ~ 32767                             |
| int                | 4            | -2147483648 ~ 247483647                    |
| long               | 4            | -2147483648 ~ 247483647                    |
| long long          | 8            | -9223372036854775808 ~ 9223372036854775807 |
| unsigned char      | 1            | 0 ~ 255                                    |
| unsigned short     | 2            | 0 ~ 65535                                  |
| unsigned int       | 4            | 0 ~ 4294967295                             |
| unsigned long long | 8            | 0 ~ 18446744073709551615                   |

基本上整數的範圍都是以 2 的 8、16、32、64 倍數在成長，`然後根據你要存取的資料大小去選擇資料類別也是很重要，可以在無形中省下很多資源，就像隨手關燈一樣，是個好習慣!`

另外，這邊有補充一下 int 跟 long 為什麼會一樣-[Why int look like same as long in C++](https://stackoverflow.com/questions/271076/what-is-the-difference-between-an-int-and-a-long-in-c)

---

今天的進度就先到這邊囉，明天就接著浮點數跟運算子的部分囉~

## 參考資料

[C++與 Unicode](https://www.ithome.com.tw/voice/135711)
[MSDC-C++ 資料類型範圍](https://learn.microsoft.com/zh-tw/cpp/cpp/data-type-ranges?view=msvc-170)
