```cpp
#include <iostream>

struct Node {
    char data;
    Node* next;
};

class Stack {
public:
    Stack() : top(nullptr) {}
    
    void push(char c) {
        Node* newNode = new Node{c, top};
        top = newNode;
    }
    
    char pop() {
        if (!top) return '\0';
        char c = top->data;
        Node* temp = top;
        top = top->next;
        delete temp;
        return c;
    }
    
    bool empty() const {
        return top == nullptr;
    }

private:
    Node* top;
};

int main() {
    Stack undoStack;
    Stack redoStack;

    undoStack.push('a');
    undoStack.push('b');
    undoStack.push('c');

    redoStack.push(undoStack.pop());
    redoStack.push(undoStack.pop());

    undoStack.push(redoStack.pop());

    std::cout << "Текущий текст: ";
    while (!undoStack.empty()) {
        std::cout << undoStack.pop();
    }
    return 0;
}
```