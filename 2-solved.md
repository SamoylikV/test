```cpp
#include <iostream>
#include <string>

struct Node {
    std::string data;
    Node* next;
};

class Queue {
public:
    Queue() : head(nullptr), tail(nullptr) {}
    
    void push(const std::string& s) {
        Node* newNode = new Node{s, nullptr};
        if (!head) {
            head = tail = newNode;
        } else {
            tail->next = newNode;
            tail = newNode;
        }
    }
    
    std::string pop() {
        if (!head) return "";
        std::string s = head->data;
        Node* temp = head;
        head = head->next;
        delete temp;
        if (!head) tail = nullptr;
        return s;
    }
    
    std::string front() const {
        return head ? head->data : "";
    }

private:
    Node* head;
    Node* tail;
};

int main() {
    Queue orders;
    
    orders.push("Алиса: эспрессо");
    orders.push("Боб: капучино");
    orders.push("Кэрол: латте");

    std::cout << "Первый обслужен: " << orders.pop() << std::endl;
    std::cout << "Следующий: " << orders.pop() << std::endl;
    std::cout << "Остался: " << orders.front() << std::endl;
    
    return 0;
}
```