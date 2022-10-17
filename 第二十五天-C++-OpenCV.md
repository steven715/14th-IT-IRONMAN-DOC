# 第二十五天 C++ OpenCV 體驗

來到了第二十五天，今天要來體驗 C++有名的 Open Source Library - `OpenCV`

## OpenCV Introduction

那首先來介紹一下什麼是 OpenCV? OpenCV 就是 Open Source Computer Vision，專門在做電腦視覺的 Library

那有了初步認識後，就直接先從下載[OpenCV](https://opencv.org/releases/)開始吧

## OpenCV Environment Set up

0. 這邊先來看一下 OpenCV 的目錄，紅線標示出來的是等等設定 C++ 專案會用到的目錄

[opencv_tree]

1. 建立一個 C++ 的空專案，然後對 _專案_ 右鍵 -> _屬性_ -> _C/C++_，`其他 Include 目錄` 裡面設定 OpenCV 的 Include 目錄

[opencv_include]

2. 接者是，專案屬性中的 _連結器_ -> _一般_ -> `其他程式庫目錄`，設定 OpenCV 的 lib 目錄

[opencv_lib]

3. 再接著，一樣 _連結器_ -> _輸入_ -> `其他相依性`，這邊輸入剛剛步驟 2 裡面的一個 lib 名稱: `opencv_world{version}d.lib`

[opencv_input]

至此，我們就能在專案中使用 openCV 的 library 了

## OpenCV Sample

那這邊就用一個顯示圖片的 C++程式 Sample 來做一個 OpenCV 示範

```
#include <iostream>
#include <opencv2/core/core.hpp>
#include <opencv2/highgui/highgui.hpp>

using namespace std;
using namespace cv;

int main() {
	Mat im = imread("C:\\Users\\Asus\\OneDrive\\文件\\Steven\\cat.jpg");
	if (! im.data)
	{
		cout << "Can't read the file" << endl;
		return 0;
	}

	namedWindow("tested", 1);
	imshow("tested", im);

	waitKey(0);
	return 0;
}
```

[opencv_result]

---

今天就簡單介紹了一下 OpenCV，明天就再繼續其他剩餘主題囉~

## 參考資料

[OpenCV - Github](https://github.com/opencv/opencv/tree/4.6.0)
[OpenCV 入門心得](https://forum.gamer.com.tw/C.php?bsn=60292&snA=6494)
[OpenCV 顯示圖片 C++程式](https://www.youtube.com/watch?v=3zzLx57xr3k)
