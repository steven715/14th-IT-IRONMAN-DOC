# 第二十一天: C++ 額外認識

今天來看看 C++的額外部分，主要的想法是小弟我在 C# 寫程式的時候，會有`Config file`能存一些可調整變數，`Logging`的 Library 可以使用來 debug，有 Task 之類的關鍵字來做`Multi thread`的動作，C# 還有`垃圾回收機制`，用完的物件 C#會幫忙清掉等等

那在 C++的話，該怎麼去實現呢?

那接下來就以上述功能來看看 C++ 如何來做這些事囉

## C++ Config File

關於 config file，在 C#中也就是將設定的變數存在 XML 或 JSON 中，那在這邊就以最簡單的 txt 文字檔做個小範例

假設 Config file 的名字是 `config.txt`:

```
name=steven
title=engineer
age=28
```

以下是範例程式碼:

```
#include <iostream>
#include <string>
#include <fstream>
#include <map>


class Config {
public:
	Config() {
		ifstream configFile("E:\\CMakeProject1\\config.txt");
		string line_text;

		while (getline(configFile, line_text))
		{
			std::size_t delimiter = line_text.find('=');
			string name = line_text.substr(0, delimiter);
			string value = line_text.substr(delimiter + 1, line_text.size());

			key_value_.insert(pair<string, string>(name, value));
		}

		configFile.close();
	}

	string GetValue(string name) {
		return key_value_[name];
	}
private:
	map<string, string> key_value_;
};

int main()
{
	Config* config = new Config();

	cout << "Config: name = " << config->GetValue("name") << endl;
	cout << "Config: title = " << config->GetValue("title") << endl;
	cout << "Config: age = " << config->GetValue("age") << endl;
}
```

上面透過讀取檔案內容以及檔案內每筆資料的字元解析，成功設置及取出設定在程式外的變數

---

今天就先介紹到這邊囉，明日再繼續努力~

## 參考資料

[C++ files](https://www.w3schools.com/cpp/cpp_files.asp)
[C++ Map](https://www.geeksforgeeks.org/map-associative-containers-the-c-standard-template-library-stl/)
