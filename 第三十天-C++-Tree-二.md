# 第三十天 C++ Tree 二

耶~ 終於來到鐵人賽最後一天了~ 那就直接來看昨天最後的`BST 二元搜尋樹`吧~

## C++ Binary Search Tree (BST)

那馬上的就來看看二元搜尋樹的規則吧

- 左子樹所有節點之值均小於根節點之值
- 右子樹所有節點之值均大於根節點之值
- 左右子樹都是二元搜尋樹
- 沒有健值相等的節點

下面就來看看二元樹插入跟查詢的程式碼囉~

```
#include <iostream>
#include <string>
#include <vector>

using namespace std;

// 樹的基本架構
struct TreeNode
{
    int value;
    struct TreeNode* left{};
    struct TreeNode* right{};
};

void insertNode(TreeNode *&root, const int k)
{
    // 若還沒有樹的話，建立新的二元樹
    if (root == nullptr)
    {
        root = new TreeNode;
        root->value = k;
        root->left = nullptr;
        root->right = nullptr;
    }
    else
    {
        // 如果已經有樹了，可以判斷樹的規則，值若小於根就往左，反之亦然
        if (k < root->value)
        {
            insertNode(root->left, k);
        }
        else
        {
            insertNode(root->right, k);
        }
    }
}

TreeNode* findNode(TreeNode* root, const int k)
{
    // 沒找到或空樹就回空
    if (root ==nullptr)
    {
        return nullptr;
    }

    // 如果有找到
    if (k == root->value)
    {
        return root;
    }

    // 往子節點找，若值小於根，則往左找，反之亦然
    if (k < root->value)
    {
        return findNode(root->left, k);
    }
    else
    {
        return findNode(root->right, k);
    }
}

void printTree(TreeNode* node)
{
    if (node != nullptr)
    {
        printTree(node->left);
        cout << node->value << "; ";
        printTree(node->right);
    }
}

int main() {
    std::vector<int> v1{ 11, 23, 3, 5, 9, 15, 2, 20 };

    TreeNode* root = nullptr;

    for (const auto& item : v1) {
        insertNode(root, item);
    }
    printTree(root);
    cout << endl;

    std::vector<int> v2{ 1, 22, 4, 16 };
    for (const auto& item : v2) {
        insertNode(root, item);
    }
    printTree(root);
    cout << endl;

    return 0;
}
```

## 欠債清單

- More things in C++ concurrency, parallelism
- [C++併發處理實戰 第二版](https://www.books.com.tw/products/0010911626)

## 完賽心得

這次是第一次參加鐵人賽，過程真的是焦慮又煩躁，畢竟還是要上班的 QQ，但都撐下去了，反倒是最後幾天有點鬆懈><  
而這一次參賽的目的也主要是想強迫自己加強寫文章、寫筆記的習慣，避免自己常常看完書或文章就帶過了  
至於寫 C++的動機，其實是受上班的影響，發現現在的語言(C#, JAVA, Python)等，都在背後幫我們做很多的事情，但其實很多時候都是底層邏輯都是一樣的，所以想透過 C++去更了解底層的實作  
期待明年的自己持續參賽，並寫出更優質的文章!

## 參考資料

[Binary Search Tree](http://alrightchiu.github.io/SecondRound/binary-search-tree-introjian-jie.html)
[C++ 中的二叉搜尋樹插入](https://www.delftstack.com/zh-tw/howto/cpp/binary-tree-insert-in-cpp/)
