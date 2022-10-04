# 第十三天: C++ 資料結構 (二)

昨天介紹完了陣列(Array)跟鏈結串列(Linked List)，今天就接著繼續來看堆疊(Stack)跟佇列(Queue)

## C++ Stacks

堆疊(Stack)是一種 LIFO(Last In First Out，後進先去)的資料結構，概念有點像搭電梯，通常是後面進電梯的人先出來

Stack 要支援兩種基本操作: _push_, _pop_; `Push`: 將元素加入堆疊中, `Pop`: 將最後一個元素移除

下面就來直接看 code 怎麼去實作這樣的概念

```
template <typename T>
class Node
{
public:
	T value;
	Node* next;

	Node(T value)
	{
		this->value = value;
	}
};

template <typename T>
class Stack
{
private:
	int size_;
	Node<T>* top_ = NULL;

public:
	Stack()
	{
		this->size_ = 0;
	}

	void push(T value)
	{
		if (this->top_ == NULL)
		{
			this->top_ = new Node<T>(value);
		}
		else
		{
			Node<T>* tmp = new Node<T>(value);
			tmp->next = this->top_;
			this->top_ = tmp;
		}
		this->size_ += 1;
	}

	Node<T>* pop()
	{
		Node<T>* tmp = this->top_;

		this->top_ = this->top_->next;
		this->size_ -= 1;
		return tmp;
	}


};

int main()
{
	Stack<int> st;

	st.push(1);
	st.push(70);
	cout << "Stack pop value: " << st.pop()->value << endl;

}
```

## C++ Queue

佇列(Queue)相比於堆疊，他是 FIFO(First In First Out，先進先出)，概念上就是日常生活中的排隊，先排的人會先出去

Queue 也是要支援基本兩種操作: _enqueue_, _dequeue_; `enqueue`: 將元素排入 Queue 中, `dequeue`: 將目前最前面的元素從 Queue 中移除

下面也是來看看實作

```
template <typename T>
class Node
{
public:
	T value;
	Node* next;

	Node(T value)
	{
		this->value = value;
	}
};

template <typename T>
class Queue
{
private:
	int size_;
	Node<T>* front_ = NULL;
	Node<T>* back_ = NULL;

public:
	Queue()
	{
		this->size_ = 0;
	}

    void enqueue(T value)
    {
        if (this->front_ == NULL)
        {
            this->front_ = new Node<T>(value);
            this->back_ = this->front_;
        }
        else
        {
            Node<T> *newNode = new  Node<T>(value);
            this->back_->next = newNode;
            this->back_ = newNode;
        }
        this->size_ += 1;
    }

    Node<T>* dequeue()
    {
        Node<T>* tmp = this->front_;

        this->front_ = this->front_->next;
        this->back_->next = NULL;
        this->size_ -= 1;
        return tmp;
    }

};

int main()
{
	Queue<int> que;

    que.enqueue(3);
    que.enqueue(66);

    cout << "1. queue dequeue: " << que.dequeue()->value << endl;
    cout << "2. queue dequeue: " << que.dequeue()->value << endl;

}
```

---

那 C++ 資料結構基本的這四個就先認識到這邊，明天就來開始看看有關測試框架的東西，俗話說的好，測試寫得好，生活沒煩惱~

## 參考資料

[Data Structures in C++ ](https://towardsdatascience.com/data-structures-in-c-part-1-b64613b0138d)
[Queue: Intro(簡介)，並以 Linked list 實作](http://alrightchiu.github.io/SecondRound/queue-introjian-jie-bing-yi-linked-listshi-zuo.html)
