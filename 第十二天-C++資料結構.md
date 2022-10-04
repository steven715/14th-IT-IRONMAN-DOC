# 第十二天: C++ 資料結構 (一)

今天來到了 C++的資料結構，想當初資料結構在大學也是上的很辛苦呢 QQ

## C++ Array

第一個先來看看陣列(Array)，陣列就是`固定數量、同一種資料類別的集合`

下面就來看一下陣列的宣告:`資料型態 陣列名稱[陣列長度];`

```
int main()
{
    // 陣列的宣告-無初始值
    // 陣列的宣告-有初始值 => int fish_bone[3] = {5, 10, 15};
	int fish_bone[3];

    // 陣列裡面的賦值
	fish_bone[0] = 5;
	fish_bone[1] = 10;
	fish_bone[2] = 15;

    // 可以透過整數i及while迴圈，印出陣列所有內容
	int i = 0;
	while (i < 3) {
		cout << "fish bone " << i << " : " << fish_bone[i] << endl;
        // 補充: 陣列會幫我們使用連續的記憶體位址去存陣列的值
        cout << "fish bone " << i << " address  : " << &fish_bone[i] << endl;
		i++;
	}

}
```

---

## C++ Linked List

剛剛講了陣列是固定數量的集合，那如果我的數量不是固定的呢? >>> 鏈結串列(Linked List) 就可以派上用場

下面就來看看實際的程式碼吧

```
// template C++ 模板 類似於 C#的泛型(genaric)，可以讓使用者在執行時獲宣告時才定義資料類別，也可以讓多載的多重資料類別只要寫一次實作就好
template <typename T>
class Node
{
    // 鏈結串列裡面的節點，會記錄前後節點
public:
	T value;
	Node* next;
	Node* previous;

	Node(T value)
	{
		this->value = value;
	}
};

template <typename T>
class LinkedList
{
private:
	int size_;
	Node<T>* head_ = NULL;
	Node<T>* tail_ = NULL;
	Node<T>* itr_ = NULL;
public:
	LinkedList()
	{
		this->size_ = 0;
	}

    // 這邊新增是透過tail節點，tail節點的next指標加上新節點，tail節點的previous指標指向現在的tail節點，然後tail節點賦值成新節點
	void append(T value)
	{
		if (this->head_ == NULL)
		{
			this->head_ = new Node<T>(value);
			this->tail_ = this->head_;
		}
		else
		{
			this->tail_->next = new Node<T>(value);
			this->tail_->previous = this->tail_;
			this->tail_ = this->tail_->next;
		}
		this->size_ += 1;
	}

    // iterator(迭代器)，透過一個指標變數，逐個遍尋整個串列
	Node<T>* iterate()
	{
		if (this->itr_ == NULL)
		{
			this->itr_ = this->head_;
		}
		else
		{
			this->itr_ = this->itr_->next;
		}
		return this->itr_;
	}

    // 回傳當前的迭代到的值
	T ptr()
	{
		return this->itr_->value;
	}

	void resetIterator()
	{
		this->tail_ = NULL;
	}
};

int main()
{
	LinkedList<int> llist;
	llist.append(10);
	llist.append(9);

    // iterate 的使用法
	while (llist.iterate() != NULL)
	{
		cout << "llist: " << llist.ptr() << endl;
	}
}
```

---

## 陣列 vs 鏈結串列

|      | 陣列                                                       | 鏈結串列                                                                                                              |
| ---- | ---------------------------------------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 優點 | 固定資料，查詢速度為快 O(1) ，同資料大小下的記憶體耗量較少 | 新增刪除十分方便，不會受限於資料數量的限制                                                                            |
| 缺點 | 資料數量固定，要做新增刪除，需要消耗 O(N)的時間            | 查詢速度為 O(N)，因為沒有 index，需要串列裡面的點都換過一輪才找的到值，節點加入指標去記憶前後節點，需要額外記憶體資源 |

---

今天先看一下陣列跟鏈結串列這兩個很相似的資料結構，明天再繼續 Stack 跟 Queue~~~

## 參考資料

[Data Structures in C++](https://towardsdatascience.com/data-structures-in-c-part-1-b64613b0138d)
[陣列(Array)與鏈結串列(Linked List)的比較](https://ithelp.ithome.com.tw/articles/10217537)
