---
layout: single
title:  "DataStructure - LinkedList"
category: algorithm
tag: [Datastructure, LinkedList]
---

## Define - LinkedList is a linear data structure where each node contains data and a pointer to the next node in the sequence.
#### 링크드 리스트는 데이터와 포인터로 구성된 노드가 선형으로 연결된 데이터 구조이다.
![LinkedList](/images/language/250805_linkedlist.png "LinkedListImage")

### 1. Implementing a LinkedList with Python


```python
# Linked List Implementation in Python

# This module implements a simple singly linked list with basic operations.
class Node:
    # Declare a Node consisting of data and a pointer to the next node
    def __init__(self, data): # type: ignore
        self.data = data # The data stored in the node
        self.next = None # Pointer to the next node

# A LinkedList class to manage the linked list operations
class LinkedList:

    # Declare the head of the LinkedList
    def __init__(self):
        self.head = None # Initialize the head of the linked list
        self.size = 0    # type: ignore # Initialize the size of the linked list
    
    # Method to add a new node at the end of the linked list
    def append(self, data): # type: ignore
        new_node = Node(data) # type: ignore # Careate a new node with the given data
        if not self.head: # If the linked list is empty
            self.head = new_node # Set the new node as the head
        else:
            current = self.head # Start from the head
            while current.next: # Traverse to the last node
                current = current.next # Move to the next node
            current.next = new_node # type: ignore # Link the new node at the end
        self.size += 1 # type: ignore # Increment the size of the linked list

    # Delete a node with the specified data from the LinkedList
    def delete(self, data): # type: ignore
        current = self.head
        previous = None # Keep track of the previous node
        while current: # Traverse through the list
            if current.data == data: # type: ignore # If the current node's data matches
                if previous: # If it's not the head node
                    previous.next = current.next # Bypass the current node
                else: # If it is the head node
                    self.head = current.next # Move the head to the next node
                self.size -= 1 # type: ignore # Decrement the size of the linked list
                return # Exit after deletion
            previous = current # Move to the next node
            current = current.next # Move to the next node

    # Find a node with the specified data in the LinkedList
    def find(self, data): # type: ignore
        current = self.head
        while current: # Traverse through the list
            if current.data == data: # type: ignore # If the current node's data matches
                return current # Return the current node
            current = current.next # Move to the next node
        return None # If not found, return None
    
    # Get the size of the LinkedList
    def size(self):
        return self.size
    
    # Method to print the LinkedList
    def print_list(self):
        current = self.head
        while current: # Traverse through the list and print each node's data
            print(current.data, end=" -> ") # type: ignore
            current = current.next
        print("None") # Indicate the end of the list

# Example usage
if __name__ == "__main__":
    linklist = LinkedList() # Create a new LinkedList instance
    linklist.append(1) # type: ignore # Append data 1
    linklist.append(2) # type: ignore # Append data 2
    linklist.append(3) # type: ignore # Append data 3
    linklist.append(4) # type: ignore # Append data 4
    linklist.append(5) # type: ignore # Append data 5

    linklist.print_list() # Print the linked list
    print(linklist.find(3)) # type: ignore # Find a node with data 3
    linklist.delete(3) # type: ignore # Delete the node with data 3
    linklist.print_list() # Print the linked list after deletion 

    found_node = linklist.find(3) # type: ignore # Find a node with data 3
    if found_node:
        print(f"Found node with data: {found_node.data}") # type: ignore
    else:
        print("Node not found")
```

### 2. Implementing a LinkedList with JavaScript


```javascript
//Linked List implementation in JavaScript

// This class implements a simple single node of a LinkedList
class Node {
    //Declare a Node with data and a pointer to the next node
    constructor(data) {
        this.data = data;
        this.next = null;
    }
}

// This class implements a LinkedList with basic operations
class LinkedList {

    // Declare a LinkedList with a head node
    constructor() {
        this.head = null;
        this.size = 0;
    }

    // Method to add a new node at the end of the LinkedList
    append(data) {
        const newNode = new Node(data); // Create a new node with the given data
        if(!this.head) { this.head = newNode; } // If the list is empty, set the head to the new node
        else {
            let current = this.head; // Start from the head node
            while(current.next) {    // Traverse to the end of the list
                current = current.next;
            }
            current.next = newNode; // Set the next of the last node to the new node
        }
        this.size++;
    }

    // Method to delete a node by value
    delete(data) {
        if(!this.head) return;
        else {
            if(this.head.data === data) {
                this.head = this.head.next;
                this.size--;
                return;
            } else {
                let current = this.head;
                while(current.next && current.next.data !== data) {
                    current = current.next;
                }
                if(current.next) { current.next = current.next.next;}
                this.size--;
            }
        }
    }

    // Method to find a node by value
    find(data) {
        let current = this.head;
        while(current) { // Traverse through the list
            if(current.data === data) return current; // Return the node if found
            current = current.next; // Move to the next node
        }
        return null; // Return null if not found
    }

    // Method to get the size of the LinkedList
    getSize() { return this.size; }

    // Method to print the LinkedList
    print() {
        let current = this.head;
        let output = '';
        while(current) { // Traverse through the list
            output += current.data + ' -> '; // Append data to output string
            current = current.next; // Move to the next node
        }
        output += 'null'; // End of the list
        console.log(output); // Print the LinkedList
    }
}

// Example usage
const list = new LinkedList();
list.append(10);
list.append(20);
list.append(30);
list.append(40);
list.append(50);
list.print(); // Output: 10 -> 20 -> 30 -> 40 -> 50 -> null
list.delete(30);
list.print(); // Output: 10 -> 20 -> 40 -> 50 -> null
console.log(list.find(20)); // Output: Node { data: 20, next: null }
console.log(list.getSize()); // Output: 4
```

### 3. Implementing a LinkedList with JAVA


```java
//Linked List Implementation in Java

// LinkedList class to manage the linked list operations
public class LinkedList {

    //This module defines a simple linked list structure with basic operations.
    private static class Node {
        private final int data;
        private Node next;

    // Declare a Node consisting of data and a pointer to the next node
    public Node(int data) {
        this.data = data;
        this.next = null; // Initialize next as null
    }
}
    private Node head; // Head of the list
    private int size; // Size of the list

    // Constructor to initialize the linked list
    public LinkedList() {
        this.head = null; // Start with an empty list
        this.size = 0; // Size is zero initially
    }

    // Method to insert a new node at the end of the list
    public void insert(int data) {
        Node newNode = new Node(data);
        if (this.head == null) { this.head = newNode; }
        else { Node current = this.head;
            while (current.next != null) { current = current.next; }
            current.next = newNode;
        }
        this.size++; // Increment the size of the list
    }

    // Delete a node with a specific value
    public void delete(int data) {
        if (this.head.data == data) { // If the head node is to be deleted
            this.head = this.head.next; // Move head to the next node
            this.size--; // Decrement size
        } else{
            Node current = this.head;
            while (current.next != null && current.next.data != data) {
                current = current.next; // Traverse the list
            }
            if (current.next != null) { // If the node to delete was found
                current.next = current.next.next; // Bypass the node
                this.size--; // Decrement size
            }
        }
    }

    //Find a node with a specific value
    public boolean find(int data) {
        Node current = this.head;
        while(current != null) {// Traverse the list
            if(current.data == data) { return true; }
            current = current.next; // Move to the next node
        }
        return false; // Return false if not found
    }

    // Get the size of the LinkedList
    public int size() { return this.size; }

    //Method to print the LinkedList
    public void print() {
        String lstr = "";
        Node current = this.head;

        while(current != null) {
            lstr += String.valueOf(current.data);
            lstr += " -> ";
            current = current.next;
        }
        lstr += "Null";
        System.out.println(lstr);
    }

    //Example usage
    public static void main(String[] args) {
        LinkedList ll = new LinkedList();
        ll.insert(1);
        ll.insert(3);
        ll.insert(5);
        ll.insert(7);
        ll.insert(9);
        ll.print();// Output: 1 -> 3 -> 5 -> 7 -> 9 -> null
        System.out.println(ll.size());// Output: 4
        ll.delete(5);
        ll.print();// Output: 1 -> 3 -> 7 -> 9 -> null
    }
}
```

### 4. Implementing a LinkedList with C++


```cpp
#include <iostream>
using namespace std;

//Linked List Implemention in C++

class LinkedList {
    private:
        // This module defines a simple linked list sturcture with basic operations.
        class Node{
            public:
                int data;
                Node* next;

                //Declare a Node consisting of data and pointer to the next node
                Node(int data) : data(data), next(nullptr) {}
        };

        Node* head;
        int size;

    public:
        LinkedList() : head(nullptr), size(0) {}

        // Method to insert a new node at the end of the list
        void insert(int data) {
            Node* newNode = new Node(data); // Create a new node with the given data
            if(this->head == nullptr) { this->head = newNode; } // if head is null, set the new node as the head
            else {
                Node* current = head;// Start from the head
                while(current->next != nullptr) {  current = current->next; } // Traverse to the last node
                current->next = newNode; // Link the new node at th and
            }
            this->size++;
        }

        // Method to delete a node with a specific value
        void remove(int data) {
            if(this->head == nullptr) return;// Make sure head is empty
            if(this->head->data == data) {   // Make sure first Node equal to data
                Node* temp = head;
                this->head = this->head->next;
                delete temp;
                this->size--;
            }
            else {
                Node* current = this->head;// From the second node, make sure you have the same data.
                while(current->next != nullptr && current->next->data != data) { current = current->next; }
                if(current->next != nullptr) {
                    Node* temp = current->next;
                    current->next = current->next->next;
                    delete temp;
                    this->size--;
                }
            
            }
        }

        // Method to find a node with a specific value
        bool find(int data) {
            Node* current = this->head;
            while(current != nullptr) {
                if(current->data == data) { return true; }
                current = current->next;
            }
            return false;
        }

        // Method to size of the LinkedList
        int list_size() {return this->size; }

        // Method to print the LinkedList
        void print() {
            Node* current = this->head;
            while(current != nullptr) {
                cout << current->data << "->";
                current = current->next;
            }
            cout << "null" << endl;
        }
};

int main() {
    LinkedList ll;
    ll.insert(1);
    ll.insert(2);
    ll.insert(3);
    ll.insert(4);
    ll.insert(5);
    ll.print(); // 1->2->3->->null
    cout << ll.list_size() << endl; // 3
    cout << (ll.find(2) ? "found" : "not found") << endl; // found
    ll.remove(2);
    ll.print(); // 1->3->null
    cout << ll.list_size() << endl; // 2
    return 0;
}
```