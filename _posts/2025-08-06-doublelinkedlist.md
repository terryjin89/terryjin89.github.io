---
layout: single
title:  "DataStructure - DoubleLinkedList"
category: algorithm
tag: [Datastructure, DoubleLinkedList]
---

## Define - A DoublLinkedList is a linear data structure in which each node contains a data field and two pointers: one pointing to the previous node and one to the next node in the sequence.
#### 더블 링크드 리스트는 데이터와 두개의 포인터로 구성된 노드가 선형으로 연결된 데이터 구조이다.
#### Data structure
![DoubleLinkedList](/images/language/250806_dll.webp "DoubleLinkedListImage")
#### Node structure
![Node-DoubleLinkedList](/images/language/250806_dll_node.webp "Node_DoubleLinkedListImage")


### 1. Implementing a DoubleLinkedList with Python


```python
# DoubleLinkedList implementation in Python

# This module implements a simple DoubleLikedList with basic operations.
class Node:
    # Declare a Node consisting of data and two pointer prevent, next node
    def __init__(self, data) -> None: # type: ignore
        self.data = data # type: ignore
        self.prev = None
        self.next = None

# This class implements a DoubleLinkedList with basic operations
class DoubleLinkedList:

    # Declare the head of the DoubleLinkedList
    def __init__(self) -> None:
        self.head = None # Initialize the head of the DoubleLinkedList
        self._size = 0 # type: ignore
    
    # Method to add a new node at the end of the DoubleLinkedList
    def append(self, data) -> None: # type: ignore
        new_node = Node(data) # type: ignore # Create a new node with given data
        if not self.head: #If the DoubleLinkedList is empty
            self.head = new_node
        else:
            current = self.head # Start from the head
            while current.next:
                current = current.next
            current.next = new_node # type: ignore
            new_node.prev = current # type: ignore
        self._size += 1 # type: ignore

    # Method to delete a node with the specified data from the DoubleLinkedList
    def delete(self, data) -> None: # type: ignore
        current = self.head
        while current: # Traverse through the list
            if current.data == data: # type: ignore # If the current node's data matches
                if current.prev: # middle or last node
                    current.prev.next = current.next
                else: # first node
                    self.head = current.next
                if current.next: 
                    current.next.prev = current.prev
                self._size -= 1 # type: ignore
                return
            current = current.next # Move to the next node
    
    # Method to find with the specified data in the DoubleLinkedList
    def find(self, data): # type: ignore
        current = self.head
        while current: # Traverse through the list
            if current.data==data: # type: ignore # If the current node's data matches
                return current # Return the current node
            current = current.next
        return None # If not found, return None
    
    # Method to get the size of the DoubleLindedList
    def size(self) -> int:
        return self._size  # type: ignore
    
    # Method to print the DoubleLinkedList
    def print_list(self):
        current = self.head
        tail = None # type: ignore

        print("Forward : ", end="")
        while current: # type: ignore
            print(current.data, end=" -> ") # type: ignore
            tail = current # type: ignore
            current = current.next
        print("Null")

        print("Backward : ", end="")
        while tail:
            print(tail.data, end=" <- ") # type: ignore
            tail = tail.prev
        print("head")

# Example usage
if __name__ == "__main__":
    dll = DoubleLinkedList() # Create a new LinkedList instance
    dll.append(1) # type: ignore # Append data 1
    dll.append(2) # type: ignore # Append data 2
    dll.append(3) # type: ignore # Append data 3
    dll.append(4) # type: ignore # Append data 4
    dll.append(5) # type: ignore # Append data 5

    dll.print_list() # Print the linked list
    print(dll.find(3)) # type: ignore # Find a node with data 3
    dll.delete(3) # type: ignore # Delete the node with data 3
    dll.print_list() # Print the linked list after deletion 

    found_node = dll.find(3) # type: ignore # Find a node with data 3
    if found_node:
        print(f"Found node with data: {found_node.data}") # type: ignore
    else:
        print("Node not found")
```

### 2. Implementing a DoubleLinkedList with JavaScript


```javascript
// DoubleLinkedList implementation in JavaScript

// This module implements a simple DoubleLinkedList with basic operations
class Node{

    // Declare a Node consisting of data and two pointer prevent, next node
    constructor(data) {
        this.data = data;
        this.prev = null;
        this.next = null;
    }
}

// This class implements a DoubleLinkedList with basic operations
class DoubleLinkedList{

    // Declare the head of the DoubleLinkedList
    constructor() {
        this.head = null;
        this._size = 0;
    }

    // Method to add a new node at the end of the DoubleLinkedList
    append(data) {
        const new_node = new Node(data)
        if(this.head === null) { this.head = new_node }
        else {
            let current = this.head
            while(current.next != null) {
                current = current.next;
            }
            current.next = new_node;
            new_node.prev = current;
        }
        this._size++;
    }

    // Method to delete a note with the specified data from in DoubleLinkedList
    delete(data) {
        if(!this.head) return; // head is empty
        
        let current = this.head;

        while(current) { // Traverse through the list
            if(current.data === data) { // If the current node's data matches
                if(current === this.head) { // Data match first node
                    this.head = current.next;
                    if(this.head) { this.head.prev = null; }
                } else {// Data match other node
                    if(current.next) { current.next.prev = current.prev; }
                    current.prev.next = current.next;
                }
                this._size--;
            }
            current = current.next;
        }
    }

    // Method to find with the specified data in the DoubleLinkedList.
    find(data) {
        if(!this.head) return;

        let current = this.head;

        while(current) {
            if(current.data === data) {return current; }
            else { current=current.next; }
        }

        return null;
    }

    //Method to get the size of the DoubleLinkedList
    size() { return this._size; }

    //Method to print the DoubleLinkedList
    print() {
        if(!this.head) return console.log("Empty!");
        
        let current = this.head;
        let tail = null;
        let list_str = "";
        
        list_str = "Forward : head";
        while(current) {
            list_str += (current.data + " -> ");
            tail = current;
            current = current.next;
        }
        list_str += "null"
        console.log(list_str);
        list_str = "";

        list_str = "Backword : ";
        while(tail) {
            list_str += (tail.data + " <- ");
            tail = tail.prev;
        }
        list_str += "head "
        console.log(list_str);
    }
}

// Example usage
const doublelist = new DoubleLinkedList();
doublelist.append(10);
doublelist.append(20);
doublelist.append(30);
doublelist.append(40);
doublelist.append(50);
doublelist.print(); // Output: 10 -> 20 -> 30 -> 40 -> 50 -> null
doublelist.delete(30);
doublelist.print(); // Output: 10 -> 20 -> 40 -> 50 -> null
console.log(doublelist.find(20)); // Output: Node { data: 20, next: null }
console.log(doublelist.size()); // Output: 4
```

### 3. Implementing a DoubleLinkedList with JAVA


```java
// DoubleLinkedList implemention in JAVA

// This module implements a simple DoubleLinkedList with basic operations
public class DoubleLinkedList<T> {
        
    // Declare a node consisting of data and a pointer to the next node
    private static class Node<T> {
        private T data;
        private Node<T> prev;
        private Node<T> next;

        //Constructor to initialize the node
        public Node(T data) {
            this.data = data;
            this.prev = null;
            this.next = null;
        }
    
    }
    private Node<T> head;// Head of the list
    private Node<T> tail;// Tail of the list
    private int _size;   // Size of the list

    //Constructor to initialize the node
    public DoubleLinkedList() {
        this.head = null;
        this.tail = null;
        this._size = 0;
    }

    //Method to insert a new node at the end of the list
    public void insert(T data) {
        Node<T> new_node = new Node<>(data); 

        // If head is empty, input the new node to head
        if(this.head == null) { 
            this.head = new_node;
            this.tail = new_node; 
        }
        else {
            this.tail.next = new_node;//In next of the last node, enter a new node
            new_node.prev = this.tail;//In prev of new node, enter the tail node
            this.tail = new_node;// Move the pointer tail node to new node
        }
        this._size++;
    }

    //Method to delete a node with a specific value
    public void delete(T data) {
        // If head is emply
        if( this.head == null) { System.out.println("List is empty!"); return; }
        else {
            int f_size = this._size;

            // first node
            if(this.head.data.equals(data)) {//first node
                if(this.head == this.tail) {// list is 1 node
                    this.head = null;
                    this.tail = null;
                } else {
                    this.head = this.head.next;
                    this.head.prev = null;
                }
            this._size--;
            } else {
                Node<T> current = this.head;

                while(current != null) {
                    Node<T> nextNode = current.next;
                    if(current.data.equals(data)) {
                        if(this.tail == current) {//last node
                            this.tail = current.prev;
                            this.tail.next = null;
                        } else{//middle node
                            current.prev.next = current.next;
                            current.next.prev = current.prev;
                        }
                        this._size--;
                    }
                    current = nextNode;
                }
            }
            if(f_size == _size) {System.out.println("Data not found!");}
        }
    }

    //Method to find 
    public boolean find(T data) {
        Node<T> current = this.head;
        while(current != null) {
            if(current.data.equals(data)) {
                return true;
            }
            current = current.next;
        }
        return false;
    }

    public int size() { return this._size; }

    public void print() {
        Node<T> current = this.head;
        
        System.out.print("Forward : head -> ");
        while(current != null) {
            System.out.print(current.data + " -> ");
            current = current.next;
        }
        System.out.println("null");

        current = this.tail;

        System.out.print("Backword : null -> ");
        while(current != null) {
            System.out.print(current.data + " -> ");
            current = current.prev;
        }
        System.out.println("head");
    }

        public static void main(String[] args) {
        DoubleLinkedList dll = new DoubleLinkedList();
        dll.insert(1);
        dll.insert(3);
        dll.insert(5);
        dll.insert(7);
        dll.insert(9);
        dll.print();// Output: 1 -> 3 -> 5 -> 7 -> 9 -> null
        System.out.println(dll.size());// Output: 4
        dll.delete(5);
        dll.print();// Output: 1 -> 3 -> 7 -> 9 -> null
    }
}
```

### 4. Implementing a DoubleLinkedList with C++


```cpp
#include <iostream>
using namespace std;
//DoubleLinkedList implemention in C++

//This modul implements a simple DoubleLinkedList with basic operations
template <typename T> // Templates allow to write data type-independent code
class DoubleLinkedList {
    private:
        // Declare a node consisting of data a pointer to the next node
        class Node{
            public:
                T data;
                Node* prev;
                Node* next;

                // Constructor to initialize the node
                Node(T data) {
                    this->data = data;
                    this->prev = nullptr;
                    this->next = nullptr;
                }
        };
        Node* head;
        Node* tail;
        int _size;
    
    public:
        
        DoubleLinkedList() {
            head = nullptr;
            tail = nullptr;
            _size = 0;
        }
        
        //Method to insert a new node at the end of the list
        void insert(T data) {
            Node* new_node = new Node(data);

            if(this->head == nullptr) {// Head is empty
                this->head = new_node;
                this->tail = new_node;
            } else {// Head is not empty
                this->tail->next = new_node;// In next of the last node, enter a new node
                new_node->prev = this->tail;// In prev oft new node, enter a tail node
                this->tail = new_node;// Move the pointer tail node to new node
            }
            this->_size++;
        }

        //Method to delete a node whih a specific data

        bool remove(T data) {
            Node* temp = nullptr;

            // Case 1: List is empty
            if(this->head == nullptr) { cout << "head is empty\n"; return false; }

            // Case 2: Only one node in the list
            if(this->head == this->tail) {
                if(this->head->data == data) {
                    delete this->head;
                    this->head = nullptr;
                    this->tail = nullptr;
                    this->_size--;
                    return true;
                } else { cout << "No matching data\n"; return false; }
            }

            // Case 3: Match haed node
            if(this->head->data == data) {
                temp = this->head;
                this->head = this->head->next;
                this->head->prev = nullptr;
                delete temp;
                this->_size--;
                return true;
            }
            
            // Case 4: Match tail node
            if(this->tail->data == data) {
                temp = this->tail;
                this->tail = this->tail->prev;
                this->tail->next = nullptr;
                delete temp;
                this->_size--;
                return true;
            }

            // Case 5: Search in middle node
            Node * current = this->head->next;
            while(current != nullptr) {
                if(current->data == data) {
                    temp = current;
                    current->prev->next = current->next;
                    current->next->prev = current->prev;
                    delete temp;
                    this->_size--;
                    return true;
                }
                current = current->next;
            }

            cout << "No matching data\n";
            return false;
        }

        // Method to find a node with aspecific data
        bool find(T data) {
            // If list is empty
            if(this->head == nullptr) { cout << "List is empty.\n"; return false; }

            Node* current = this->head;
            while(current != nullptr) {
                if(current->data == data) {
                    return true;
                }
                current = current->next;
            }
            return false;
        }

        // Method to size of the list
        int list_size() {return this->_size; }

        // Method to print list's data
        void print() {
            Node* current = this->head;
            cout << "Forward : head -> ";
            while(current != nullptr) {
                cout << current->data << " -> ";
                current = current->next;
            }
            cout << "null\n";

            cout << "Backward : null -> ";
            current = this->tail;
            while(current != nullptr) {
                cout << current->data << " -> ";
                current = current->prev;
            }
            cout << "head\n";
        }
};

int main() {
    DoubleLinkedList<int> dll;
    dll.insert(1);
    dll.insert(2);
    dll.insert(3);
    dll.insert(4);
    dll.insert(5);
    dll.print(); // 1->2->3->->null
    cout << dll.list_size() << endl; // 3
    cout << (dll.find(2) ? "found" : "not found") << endl; // found
    dll.remove(2);
    dll.print(); // 1->3->null
    cout << dll.list_size() << endl; // 2
    return 0;
}
```