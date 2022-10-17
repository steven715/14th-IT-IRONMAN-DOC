# 第二十八天 C++ 設計模式 - 七

今天就緊接著把最後一個設計模式 - 狀態模式 給介紹完吧!

## 狀態模式

狀態模式是一種行為設計模式，讓我們在一個物件的內部狀態變化時改變其行為，使其看上去就像改變了自身所屬的類別一樣

有個簡單的例子，像是我們在部落格之類的網站上發表文章，文章發送前的狀態可能是 `草稿`、`審核中`以及`已發佈`等等的狀態，這種模擬就可以用狀態模式實現

下面就用文章的例子來看看，假設三種狀態 `草稿` 可以*編輯*，*確認*後轉 `審核中` *審核過*了後轉 `已發佈`

```
class Document;

class State
{
protected:
    Document* doc_;

public:
    void set_doc(Document* doc)
    {
        this->doc_ = doc;
    }

    virtual void Change() = 0;
    virtual void Check() = 0;
    virtual void Confirm() = 0;
};

class DraftState : public State {
public:
    void Change() override;
    void Check() override;
    void Confirm() override;
};
class ReviewState : public State {
public:
    void Change() override;
    void Check() override;
    void Confirm() override;
};

class Document
{
private:
    State* state_;
public:
    Document()
    {
        this->Transition(new DraftState);
    }

    void Transition(State* state)
    {
        if (this->state_ != nullptr)
        {
            delete this->state_;
        }
        this->state_ = state;
        this->state_->set_doc(this);
    }

    void Review()
    {
        this->state_->Check();
    }

    void Write()
    {
        this->state_->Change();
    }

    void Confirm()
    {
        this->state_->Confirm();
    }
};

class PublishState : public State {
public:
    void Change() override
    {
        cout << "Publish no change " << endl;
    }

    void Check() override
    {
        cout << "Publish no check " << endl;
    }

    void Confirm() override
    {
        cout << "Doc is publish " << endl;
    }
};

void DraftState::Change()
{
    cout << "Draft can change " << endl;
}

void DraftState::Check()
{
    cout << "Draft to check " << endl;
    this->doc_->Transition(new ReviewState);
}

void DraftState::Confirm()
{
    cout << "Draft no confirm " << endl;
}

void ReviewState::Change()
{
    cout << "Review no change " << endl;
}

void ReviewState::Check()
{
    cout << "Review no check " << endl;
}

void ReviewState::Confirm()
{
    cout << "Review to confirm " << endl;
    this->doc_->Transition(new PublishState);
}

int main() {
    Document* doc = new Document;
    doc->Write();
    doc->Review();
    doc->Confirm();

    return 0;
}
```

可以看到狀態模式能定義出各種狀態該做的事情在不同類別中，但代價是更多更複雜的程式碼，如果狀態很少或是很少改變狀態就可以不用考慮狀態模式唷!

---

今天就將設計模式之前欠的部分補齊囉~期待完賽 XD

## 參考資料

[C++ 狀態模式](https://refactoringguru.cn/design-patterns/state)
