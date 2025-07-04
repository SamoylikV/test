```cpp
#include <iostream>
#include <string>

struct Node {
    std::string data;
    Node* next;
};

class Playlist {
public:
    Playlist() : head(nullptr) {}
    
    void push_back(const std::string& song) {
        Node* newNode = new Node{song, nullptr};
        if (!head) {
            head = newNode;
            return;
        }
        Node* cur = head;
        while (cur->next) cur = cur->next;
        cur->next = newNode;
    }
    
    void insert_after(Node* node, const std::string& song) {
        if (!node) return;
        Node* newNode = new Node{song, node->next};
        node->next = newNode;
    }
    
    void erase_after(Node* node) {
        if (!node || !node->next) return;
        Node* temp = node->next;
        node->next = temp->next;
        delete temp;
    }
    
    Node* find(const std::string& song) {
        Node* cur = head;
        while (cur) {
            if (cur->data == song) return cur;
            cur = cur->next;
        }
        return nullptr;
    }
    
    void print() const {
        Node* cur = head;
        while (cur) {
            std::cout << " - " << cur->data << "\n";
            cur = cur->next;
        }
    }

private:
    Node* head;
};

int main() {
    Playlist playlist;
    
    playlist.push_back("Bohemian Rhapsody");
    playlist.push_back("Imagine");
    playlist.push_back("Hotel California");
    
    Node* target = playlist.find("Imagine");
    playlist.insert_after(target, "Stairway to Heaven");
    
    playlist.erase_after(playlist.find("Bohemian Rhapsody"));
    
    std::cout << "Обновленный плейлист:\n";
    playlist.print();
    
    return 0;
}
```