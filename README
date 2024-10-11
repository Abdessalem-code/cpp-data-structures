## Table of Contents

1. [Arrays and Dynamic Arrays](#1-arrays-and-dynamic-arrays)
2. [Linked Lists](#2-linked-lists)
   - Singly Linked List
   - Doubly Linked List
   - Circular Linked List
3. [Stacks and Queues](#3-stacks-and-queues)
   - Stack
   - Queue
   - Priority Queue
   - Deque
4. [Trees](#4-trees)
   - Binary Tree
   - Binary Search Tree (BST)
   - AVL Tree
   - Red-Black Tree
   - Trie (Prefix Tree)
5. [Heaps](#5-heaps)
   - Binary Heap
   - Fibonacci Heap
6. [Hash Tables](#6-hash-tables)
   - Using `std::unordered_map` and `std::unordered_set`
   - Custom Implementation
7. [Graphs](#7-graphs)
   - Adjacency Matrix
   - Adjacency List
   - Edge List
8. [Sets and Maps](#8-sets-and-maps)
   - Using `std::set` and `std::map`
   - Using `std::unordered_set` and `std::unordered_map`
   - Custom Implementation
9. [Disjoint Sets (Union-Find)](#9-disjoint-sets-union-find)
10. [Other Data Structures](#10-other-data-structures)
    - Bitset
    - Bloom Filter
    - Skip List

---

## 1. Arrays and Dynamic Arrays

### Static Arrays

**Description:** Fixed-size arrays allocated on the stack.

**Implementation:**

```cpp
#include <iostream>

int main() {
    int arr[5] = {1, 2, 3, 4, 5};
    // Access elements
    std::cout << arr[2] << std::endl; // Outputs: 3
    return 0;
}
```

**Characteristics:**
- Fixed size determined at compile time.
- Stored contiguously in memory.
- Fast access to elements (`O(1)`).

### Dynamic Arrays (`std::vector`)

**Description:** Resizable arrays provided by the C++ Standard Library.

**Implementation:**

```cpp
#include <iostream>
#include <vector>

int main() {
    std::vector<int> vec = {1, 2, 3, 4, 5};
    vec.push_back(6); // Add element
    std::cout << vec[2] << std::endl; // Outputs: 3
    return 0;
}
```

**Characteristics:**
- Dynamic resizing.
- Stored contiguously.
- Provides random access (`O(1)`).
- Supports various operations like insertion, deletion, etc.

### Custom Dynamic Array

**Description:** Implementing a dynamic array manually using pointers and dynamic memory allocation.

**Implementation:**

```cpp
#include <iostream>
#include <algorithm> // For std::copy

class DynamicArray {
private:
    int* data;
    size_t capacity;
    size_t size;

    void resize() {
        capacity *= 2;
        int* newData = new int[capacity];
        std::copy(data, data + size, newData);
        delete[] data;
        data = newData;
    }

public:
    DynamicArray() : capacity(2), size(0) {
        data = new int[capacity];
    }

    ~DynamicArray() {
        delete[] data;
    }

    void push_back(int value) {
        if (size == capacity) {
            resize();
        }
        data[size++] = value;
    }

    int operator[](size_t index) const {
        if(index >= size) throw std::out_of_range("Index out of range");
        return data[index];
    }

    size_t getSize() const { return size; }
};

int main() {
    DynamicArray arr;
    arr.push_back(1);
    arr.push_back(2);
    arr.push_back(3);
    std::cout << arr[2] << std::endl; // Outputs: 3
    return 0;
}
```

**Characteristics:**
- Manual control over memory management.
- Requires handling resizing, copying, and destruction.
- Educational but generally less efficient and safe than `std::vector`.

---

## 2. Linked Lists

Linked lists are linear data structures where each element (node) points to the next (and possibly previous) node. They allow for efficient insertions and deletions.

### Singly Linked List

**Description:** Each node points only to the next node.

**Implementation:**

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class SinglyLinkedList {
private:
    Node* head;

public:
    SinglyLinkedList() : head(nullptr) {}

    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (!head) {
            head = newNode;
            return;
        }
        Node* temp = head;
        while(temp->next)
            temp = temp->next;
        temp->next = newNode;
    }

    void display() const {
        Node* temp = head;
        while(temp){
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }

    ~SinglyLinkedList(){
        Node* current = head;
        while(current){
            Node* nextNode = current->next;
            delete current;
            current = nextNode;
        }
    }
};

int main(){
    SinglyLinkedList list;
    list.insertAtEnd(1);
    list.insertAtEnd(2);
    list.insertAtEnd(3);
    list.display(); // Outputs: 1 2 3
    return 0;
}
```

**Characteristics:**
- Efficient insertions and deletions (`O(1)` if position is known).
- No random access (`O(n)` to access elements).
- Uses extra memory for pointers.

### Doubly Linked List

**Description:** Each node points to both the next and previous nodes.

**Implementation:**

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node* prev;
    Node(int val) : data(val), next(nullptr), prev(nullptr) {}
};

class DoublyLinkedList {
private:
    Node* head;
    Node* tail;

public:
    DoublyLinkedList() : head(nullptr), tail(nullptr) {}

    void insertAtEnd(int val) {
        Node* newNode = new Node(val);
        if (!head){
            head = tail = newNode;
            return;
        }
        tail->next = newNode;
        newNode->prev = tail;
        tail = newNode;
    }

    void displayForward() const {
        Node* temp = head;
        while(temp){
            std::cout << temp->data << " ";
            temp = temp->next;
        }
        std::cout << std::endl;
    }

    void displayBackward() const {
        Node* temp = tail;
        while(temp){
            std::cout << temp->data << " ";
            temp = temp->prev;
        }
        std::cout << std::endl;
    }

    ~DoublyLinkedList(){
        Node* current = head;
        while(current){
            Node* nextNode = current->next;
            delete current;
            current = nextNode;
        }
    }
};

int main(){
    DoublyLinkedList list;
    list.insertAtEnd(1);
    list.insertAtEnd(2);
    list.insertAtEnd(3);
    list.displayForward();  // Outputs: 1 2 3
    list.displayBackward(); // Outputs: 3 2 1
    return 0;
}
```

**Characteristics:**
- Efficient insertions and deletions from both ends.
- Bidirectional traversal.
- More memory overhead due to additional pointer.

### Circular Linked List

**Description:** The last node points back to the first node, forming a circle.

**Implementation:**

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class CircularLinkedList {
private:
    Node* head;

public:
    CircularLinkedList() : head(nullptr) {}

    void insert(int val){
        Node* newNode = new Node(val);
        if (!head){
            head = newNode;
            newNode->next = head;
            return;
        }
        Node* temp = head;
        while(temp->next != head)
            temp = temp->next;
        temp->next = newNode;
        newNode->next = head;
    }

    void display() const {
        if (!head) return;
        Node* temp = head;
        do{
            std::cout << temp->data << " ";
            temp = temp->next;
        } while(temp != head);
        std::cout << std::endl;
    }

    ~CircularLinkedList(){
        if (!head) return;
        Node* current = head->next;
        while(current != head){
            Node* nextNode = current->next;
            delete current;
            current = nextNode;
        }
        delete head;
    }
};

int main(){
    CircularLinkedList list;
    list.insert(1);
    list.insert(2);
    list.insert(3);
    list.display(); // Outputs: 1 2 3
    return 0;
}
```

**Characteristics:**
- Efficient traversal without null termination.
- Useful for implementing round-robin algorithms.
- Similar memory characteristics to singly linked lists.

---

## 3. Stacks and Queues

Stacks and queues are abstract data types that follow specific orderings for insertions and deletions.

### Stack

**Description:** Last-In-First-Out (LIFO) structure.

**Implementation Using `std::vector`:**

```cpp
#include <iostream>
#include <vector>

int main(){
    std::vector<int> stack;
    // Push elements
    stack.push_back(1);
    stack.push_back(2);
    stack.push_back(3);
    // Pop elements
    while(!stack.empty()){
        std::cout << stack.back() << " ";
        stack.pop_back();
    }
    // Outputs: 3 2 1
    return 0;
}
```

**Implementation Using `std::stack`:**

```cpp
#include <iostream>
#include <stack>

int main(){
    std::stack<int> stack;
    // Push elements
    stack.push(1);
    stack.push(2);
    stack.push(3);
    // Pop elements
    while(!stack.empty()){
        std::cout << stack.top() << " ";
        stack.pop();
    }
    // Outputs: 3 2 1
    return 0;
}
```

**Custom Implementation Using Linked List:**

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class Stack {
private:
    Node* topNode;

public:
    Stack() : topNode(nullptr) {}

    void push(int val){
        Node* newNode = new Node(val);
        newNode->next = topNode;
        topNode = newNode;
    }

    void pop(){
        if (!topNode) throw std::out_of_range("Stack is empty");
        Node* temp = topNode;
        topNode = topNode->next;
        delete temp;
    }

    int top() const {
        if (!topNode) throw std::out_of_range("Stack is empty");
        return topNode->data;
    }

    bool empty() const { return topNode == nullptr; }

    ~Stack(){
        while(!empty()) pop();
    }
};

int main(){
    Stack stack;
    stack.push(1);
    stack.push(2);
    stack.push(3);
    while(!stack.empty()){
        std::cout << stack.top() << " ";
        stack.pop();
    }
    // Outputs: 3 2 1
    return 0;
}
```

**Characteristics:**
- LIFO ordering.
- Efficient `push` and `pop` operations (`O(1)`).

### Queue

**Description:** First-In-First-Out (FIFO) structure.

**Implementation Using `std::deque`:**

```cpp
#include <iostream>
#include <deque>

int main(){
    std::deque<int> queue;
    // Enqueue elements
    queue.push_back(1);
    queue.push_back(2);
    queue.push_back(3);
    // Dequeue elements
    while(!queue.empty()){
        std::cout << queue.front() << " ";
        queue.pop_front();
    }
    // Outputs: 1 2 3
    return 0;
}
```

**Implementation Using `std::queue`:**

```cpp
#include <iostream>
#include <queue>

int main(){
    std::queue<int> queue;
    // Enqueue elements
    queue.push(1);
    queue.push(2);
    queue.push(3);
    // Dequeue elements
    while(!queue.empty()){
        std::cout << queue.front() << " ";
        queue.pop();
    }
    // Outputs: 1 2 3
    return 0;
}
```

**Custom Implementation Using Linked List:**

```cpp
#include <iostream>

struct Node {
    int data;
    Node* next;
    Node(int val) : data(val), next(nullptr) {}
};

class Queue {
private:
    Node* frontNode;
    Node* rearNode;

public:
    Queue() : frontNode(nullptr), rearNode(nullptr) {}

    void enqueue(int val){
        Node* newNode = new Node(val);
        if (!rearNode){
            frontNode = rearNode = newNode;
            return;
        }
        rearNode->next = newNode;
        rearNode = newNode;
    }

    void dequeue(){
        if (!frontNode) throw std::out_of_range("Queue is empty");
        Node* temp = frontNode;
        frontNode = frontNode->next;
        if (!frontNode) rearNode = nullptr;
        delete temp;
    }

    int front() const {
        if (!frontNode) throw std::out_of_range("Queue is empty");
        return frontNode->data;
    }

    bool empty() const { return frontNode == nullptr; }

    ~Queue(){
        while(!empty()) dequeue();
    }
};

int main(){
    Queue queue;
    queue.enqueue(1);
    queue.enqueue(2);
    queue.enqueue(3);
    while(!queue.empty()){
        std::cout << queue.front() << " ";
        queue.dequeue();
    }
    // Outputs: 1 2 3
    return 0;
}
```

**Characteristics:**
- FIFO ordering.
- Efficient `enqueue` and `dequeue` operations (`O(1)`).

### Priority Queue

**Description:** A special type of queue where elements are ordered based on priority.

**Implementation Using `std::priority_queue`:**

```cpp
#include <iostream>
#include <queue>
#include <vector>

int main(){
    // Max-Heap (default)
    std::priority_queue<int> maxHeap;
    maxHeap.push(3);
    maxHeap.push(1);
    maxHeap.push(4);
    maxHeap.push(2);
    while(!maxHeap.empty()){
        std::cout << maxHeap.top() << " "; // Outputs: 4 3 2 1
        maxHeap.pop();
    }
    std::cout << std::endl;

    // Min-Heap using comparator
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;
    minHeap.push(3);
    minHeap.push(1);
    minHeap.push(4);
    minHeap.push(2);
    while(!minHeap.empty()){
        std::cout << minHeap.top() << " "; // Outputs: 1 2 3 4
        minHeap.pop();
    }
    return 0;
}
```

**Characteristics:**
- By default, `std::priority_queue` is a max-heap.
- Can be customized to function as a min-heap or with custom comparators.
- Efficient `push` and `pop` operations (`O(log n)`).

### Deque

**Description:** Double-ended queue allowing insertions and deletions at both ends.

**Implementation Using `std::deque`:**

```cpp
#include <iostream>
#include <deque>

int main(){
    std::deque<int> dq;
    // Insert at front and back
    dq.push_front(1);
    dq.push_back(2);
    dq.push_front(0);
    // Access elements
    for(auto& val : dq){
        std::cout << val << " "; // Outputs: 0 1 2
    }
    std::cout << std::endl;
    return 0;
}
```

**Characteristics:**
- Supports random access (`O(1)`).
- Efficient insertions and deletions at both ends (`O(1)`).
- Underlying implementation may vary (often a sequence of contiguous blocks).

---

## 4. Trees

Trees are hierarchical data structures consisting of nodes connected by edges. They are widely used in various applications like databases, file systems, and more.

### Binary Tree

**Description:** Each node has at most two children: left and right.

**Implementation:**

```cpp
#include <iostream>

struct TreeNode {
    int data;
    TreeNode* left;
    TreeNode* right;
    TreeNode(int val): data(val), left(nullptr), right(nullptr){}
};

class BinaryTree {
public:
    TreeNode* root;

    BinaryTree() : root(nullptr) {}

    void insert(int val){
        if (!root){
            root = new TreeNode(val);
            return;
        }
        insertHelper(root, val);
    }

    void insertHelper(TreeNode* node, int val){
        // Simple insertion without ordering
        if (!node->left){
            node->left = new TreeNode(val);
        }
        else if (!node->right){
            node->right = new TreeNode(val);
        }
        else{
            // Insert into left subtree for simplicity
            insertHelper(node->left, val);
        }
    }

    void inorder(TreeNode* node) const {
        if (!node) return;
        inorder(node->left);
        std::cout << node->data << " ";
        inorder(node->right);
    }

    void displayInorder() const {
        inorder(root);
        std::cout << std::endl;
    }

    ~BinaryTree(){
        destroy(root);
    }

    void destroy(TreeNode* node){
        if (!node) return;
        destroy(node->left);
        destroy(node->right);
        delete node;
    }
};

int main(){
    BinaryTree tree;
    tree.insert(1);
    tree.insert(2);
    tree.insert(3);
    tree.insert(4);
    tree.displayInorder(); // Outputs: 4 2 1 3
    return 0;
}
```

**Characteristics:**
- Hierarchical structure.
- No inherent ordering of nodes unless specified (e.g., BST).

### Binary Search Tree (BST)

**Description:** Binary tree with ordered nodes: left subtree contains nodes less than the parent, right subtree contains nodes greater.

**Implementation Using Linked Nodes:**

```cpp
#include <iostream>

struct BSTNode {
    int data;
    BSTNode* left;
    BSTNode* right;
    BSTNode(int val): data(val), left(nullptr), right(nullptr){}
};

class BST {
public:
    BSTNode* root;

    BST() : root(nullptr) {}

    void insert(int val){
        root = insertHelper(root, val);
    }

    BSTNode* insertHelper(BSTNode* node, int val){
        if (!node) return new BSTNode(val);
        if (val < node->data)
            node->left = insertHelper(node->left, val);
        else
            node->right = insertHelper(node->right, val);
        return node;
    }

    bool search(int val) const {
        return searchHelper(root, val);
    }

    bool searchHelper(BSTNode* node, int val) const{
        if (!node) return false;
        if (val == node->data) return true;
        if (val < node->data)
            return searchHelper(node->left, val);
        else
            return searchHelper(node->right, val);
    }

    void inorder(BSTNode* node) const {
        if (!node) return;
        inorder(node->left);
        std::cout << node->data << " ";
        inorder(node->right);
    }

    void displayInorder() const {
        inorder(root);
        std::cout << std::endl;
    }

    ~BST(){
        destroy(root);
    }

    void destroy(BSTNode* node){
        if (!node) return;
        destroy(node->left);
        destroy(node->right);
        delete node;
    }
};

int main(){
    BST tree;
    tree.insert(5);
    tree.insert(3);
    tree.insert(7);
    tree.insert(2);
    tree.insert(4);
    tree.insert(6);
    tree.insert(8);
    tree.displayInorder(); // Outputs: 2 3 4 5 6 7 8
    std::cout << std::boolalpha << tree.search(4) << std::endl; // Outputs: true
    std::cout << std::boolalpha << tree.search(10) << std::endl; // Outputs: false
    return 0;
}
```

**Characteristics:**
- Allows efficient searching, insertion, and deletion (`O(log n)` on average).
- In-order traversal yields sorted order.
- Can become unbalanced (`O(n)` operations) without balancing.

### AVL Tree

**Description:** Self-balancing BST where the heights of two child subtrees of any node differ by at most one.

**Implementation:**

Implementing a complete AVL tree is extensive. Below is a simplified version focusing on insertion and balancing.

```cpp
#include <iostream>
#include <algorithm>

struct AVLNode {
    int data;
    AVLNode* left;
    AVLNode* right;
    int height;
    AVLNode(int val): data(val), left(nullptr), right(nullptr), height(1){}
};

class AVLTree {
public:
    AVLNode* root;

    AVLTree() : root(nullptr) {}

    // Get height
    int height(AVLNode* node){
        if (!node) return 0;
        return node->height;
    }

    // Get balance factor
    int getBalance(AVLNode* node){
        if (!node) return 0;
        return height(node->left) - height(node->right);
    }

    // Right rotate
    AVLNode* rightRotate(AVLNode* y){
        AVLNode* x = y->left;
        AVLNode* T2 = x->right;

        // Perform rotation
        x->right = y;
        y->left = T2;

        // Update heights
        y->height = 1 + std::max(height(y->left), height(y->right));
        x->height = 1 + std::max(height(x->left), height(x->right));

        return x;
    }

    // Left rotate
    AVLNode* leftRotate(AVLNode* x){
        AVLNode* y = x->right;
        AVLNode* T2 = y->left;

        // Perform rotation
        y->left = x;
        x->right = T2;

        // Update heights
        x->height = 1 + std::max(height(x->left), height(x->right));
        y->height = 1 + std::max(height(y->left), height(y->right));

        return y;
    }

    // Insert node
    AVLNode* insert(AVLNode* node, int val){
        if (!node) return new AVLNode(val);
        if (val < node->data)
            node->left = insert(node->left, val);
        else if (val > node->data)
            node->right = insert(node->right, val);
        else // Duplicate keys not allowed
            return node;

        // Update height
        node->height = 1 + std::max(height(node->left), height(node->right));

        // Get balance factor
        int balance = getBalance(node);

        // If unbalanced, perform rotations

        // Left Left Case
        if (balance > 1 && val < node->left->data)
            return rightRotate(node);

        // Right Right Case
        if (balance < -1 && val > node->right->data)
            return leftRotate(node);

        // Left Right Case
        if (balance > 1 && val > node->left->data){
            node->left = leftRotate(node->left);
            return rightRotate(node);
        }

        // Right Left Case
        if (balance < -1 && val < node->right->data){
            node->right = rightRotate(node->right);
            return leftRotate(node);
        }

        return node;
    }

    void insert(int val){
        root = insert(root, val);
    }

    void inorder(AVLNode* node) const {
        if (!node) return;
        inorder(node->left);
        std::cout << node->data << " ";
        inorder(node->right);
    }

    void displayInorder() const {
        inorder(root);
        std::cout << std::endl;
    }

    ~AVLTree(){
        destroy(root);
    }

    void destroy(AVLNode* node){
        if (!node) return;
        destroy(node->left);
        destroy(node->right);
        delete node;
    }
};

int main(){
    AVLTree tree;
    tree.insert(10);
    tree.insert(20);
    tree.insert(30);
    tree.insert(40);
    tree.insert(50);
    tree.insert(25);
    tree.displayInorder(); // Outputs: 10 20 25 30 40 50
    return 0;
}
```

**Characteristics:**
- Maintains balance after insertions and deletions.
- Guarantees `O(log n)` time for search, insert, and delete.
- More complex to implement compared to basic BST.

### Red-Black Tree

**Description:** Another type of self-balancing BST with properties ensuring the tree remains approximately balanced.

**Implementation:**

Implementing a full red-black tree is complex and beyond the scope of this guide. However, the C++ Standard Library's `std::map` and `std::set` are typically implemented as red-black trees.

**Using `std::map` (which uses a red-black tree internally):**

```cpp
#include <iostream>
#include <map>

int main(){
    std::map<int, std::string> rbTree;
    rbTree[10] = "Ten";
    rbTree[20] = "Twenty";
    rbTree[30] = "Thirty";
    rbTree[15] = "Fifteen";

    for(auto& pair : rbTree){
        std::cout << pair.first << ": " << pair.second << std::endl;
    }
    /*
    Outputs:
    10: Ten
    15: Fifteen
    20: Twenty
    30: Thirty
    */
    return 0;
}
```

**Characteristics:**
- Guarantees `O(log n)` time for operations.
- Maintains a balanced tree using color properties.
- `std::map` and `std::set` are typical red-black tree implementations in C++.

### Trie (Prefix Tree)

**Description:** Tree-like data structure used for efficient retrieval of keys, often strings.

**Implementation:**

```cpp
#include <iostream>
#include <unordered_map>

struct TrieNode {
    bool isEnd;
    std::unordered_map<char, TrieNode*> children;
    TrieNode() : isEnd(false) {}
};

class Trie {
private:
    TrieNode* root;

public:
    Trie() : root(new TrieNode()) {}

    void insert(const std::string& word){
        TrieNode* node = root;
        for(char ch : word){
            if(!node->children.count(ch)){
                node->children[ch] = new TrieNode();
            }
            node = node->children[ch];
        }
        node->isEnd = true;
    }

    bool search(const std::string& word) const {
        TrieNode* node = root;
        for(char ch : word){
            if(!node->children.count(ch)) return false;
            node = node->children.at(ch);
        }
        return node->isEnd;
    }

    bool startsWith(const std::string& prefix) const {
        TrieNode* node = root;
        for(char ch : prefix){
            if(!node->children.count(ch)) return false;
            node = node->children.at(ch);
        }
        return true;
    }

    ~Trie(){
        destroy(root);
    }

    void destroy(TrieNode* node){
        if (!node) return;
        for(auto& pair : node->children){
            destroy(pair.second);
        }
        delete node;
    }
};

int main(){
    Trie trie;
    trie.insert("apple");
    trie.insert("app");
    std::cout << std::boolalpha;
    std::cout << trie.search("apple") << std::endl;   // Outputs: true
    std::cout << trie.search("app") << std::endl;     // Outputs: true
    std::cout << trie.search("appl") << std::endl;    // Outputs: false
    std::cout << trie.startsWith("appl") << std::endl; // Outputs: true
    return 0;
}
```

**Characteristics:**
- Efficient for prefix-based searches.
- Useful in applications like autocomplete and spell checking.
- Space can be high if not optimized.

---

## 5. Heaps

Heaps are specialized tree-based structures that satisfy the heap property: in a **max-heap**, every parent node is greater than or equal to its children, and in a **min-heap**, every parent node is less than or equal to its children.

### Binary Heap

**Description:** Complete binary tree that satisfies the heap property.

**Implementation Using `std::priority_queue`:**

```cpp
#include <iostream>
#include <queue>
#include <vector>

int main(){
    // Max-Heap
    std::priority_queue<int> maxHeap;
    maxHeap.push(10);
    maxHeap.push(5);
    maxHeap.push(20);
    while(!maxHeap.empty()){
        std::cout << maxHeap.top() << " "; // Outputs: 20 10 5
        maxHeap.pop();
    }
    std::cout << std::endl;

    // Min-Heap
    std::priority_queue<int, std::vector<int>, std::greater<int>> minHeap;
    minHeap.push(10);
    minHeap.push(5);
    minHeap.push(20);
    while(!minHeap.empty()){
        std::cout << minHeap.top() << " "; // Outputs: 5 10 20
        minHeap.pop();
    }
    return 0;
}
```

**Characteristics:**
- Efficient `push` and `pop` operations (`O(log n)`).
- Built on top of a vector or other container.

### Binary Heap Custom Implementation

**Description:** Implementing a binary heap manually using a vector.

**Implementation:**

```cpp
#include <iostream>
#include <vector>
#include <algorithm>

class BinaryHeap {
private:
    std::vector<int> heap;
    bool isMinHeap;

    // Compare function
    bool compare(int a, int b){
        return isMinHeap ? a < b : a > b;
    }

    void heapifyUp(int index){
        if(index && compare(heap[index], heap[parent(index)])){
            std::swap(heap[index], heap[parent(index)]);
            heapifyUp(parent(index));
        }
    }

    void heapifyDown(int index){
        int leftIdx = left(index);
        int rightIdx = right(index);
        int extreme = index;

        if(leftIdx < heap.size() && compare(heap[leftIdx], heap[extreme]))
            extreme = leftIdx;
        if(rightIdx < heap.size() && compare(heap[rightIdx], heap[extreme]))
            extreme = rightIdx;
        if(extreme != index){
            std::swap(heap[index], heap[extreme]);
            heapifyDown(extreme);
        }
    }

    int parent(int index){ return (index - 1) / 2; }
    int left(int index){ return 2 * index + 1; }
    int right(int index){ return 2 * index + 2; }

public:
    BinaryHeap(bool minHeap=true) : isMinHeap(minHeap) {}

    void insert(int val){
        heap.push_back(val);
        heapifyUp(heap.size()-1);
    }

    int getExtreme() const {
        if(heap.empty()) throw std::out_of_range("Heap is empty");
        return heap[0];
    }

    void extractExtreme(){
        if(heap.empty()) throw std::out_of_range("Heap is empty");
        heap[0] = heap.back();
        heap.pop_back();
        heapifyDown(0);
    }

    bool empty() const { return heap.empty(); }

    void display() const {
        for(auto val : heap)
            std::cout << val << " ";
        std::cout << std::endl;
    }
};

int main(){
    BinaryHeap maxHeap(false); // Max-Heap
    maxHeap.insert(10);
    maxHeap.insert(5);
    maxHeap.insert(20);
    maxHeap.display(); // Possible output: 20 5 10
    while(!maxHeap.empty()){
        std::cout << maxHeap.getExtreme() << " "; // Outputs: 20 10 5
        maxHeap.extractExtreme();
    }
    std::cout << std::endl;

    BinaryHeap minHeap(true); // Min-Heap
    minHeap.insert(10);
    minHeap.insert(5);
    minHeap.insert(20);
    minHeap.display(); // Possible output: 5 10 20
    while(!minHeap.empty()){
        std::cout << minHeap.getExtreme() << " "; // Outputs: 5 10 20
        minHeap.extractExtreme();
    }
    return 0;
}
```

**Characteristics:**
- Complete binary tree.
- Efficient for implementing priority queues.
- Custom implementation provides flexibility but requires careful handling.

### Fibonacci Heap

**Description:** A more advanced heap with better amortized running times for some operations.

**Implementation:**

Implementing a Fibonacci heap is complex and generally unnecessary unless specific performance characteristics are required. It's beyond the scope of this guide. Instead, consider using `std::priority_queue` or implementing a binary heap as shown above.

**Characteristics:**
- Supports `insert`, `find-min`, `merge` in `O(1)` amortized time.
- `extract-min` and `delete` operations take `O(log n)` amortized time.
- Useful in algorithms like Dijkstra's with Fibonacci heaps.

---

## 6. Hash Tables

Hash tables are data structures that provide fast insertion, deletion, and lookup of key-value pairs based on hash functions.

### Using `std::unordered_map` and `std::unordered_set`

**Description:** C++ Standard Library implementations of hash tables.

**Implementation of `std::unordered_map`:**

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main(){
    std::unordered_map<std::string, int> hashMap;
    // Insert key-value pairs
    hashMap["apple"] = 3;
    hashMap["banana"] = 5;
    hashMap["orange"] = 2;

    // Access elements
    std::cout << "apple: " << hashMap["apple"] << std::endl; // Outputs: apple: 3

    // Iterate
    for(auto& pair : hashMap){
        std::cout << pair.first << ": " << pair.second << std::endl;
    }

    // Check existence
    if(hashMap.find("banana") != hashMap.end()){
        std::cout << "Banana exists." << std::endl;
    }

    return 0;
}
```

**Implementation of `std::unordered_set`:**

```cpp
#include <iostream>
#include <unordered_set>

int main(){
    std::unordered_set<int> hashSet;
    // Insert elements
    hashSet.insert(1);
    hashSet.insert(2);
    hashSet.insert(3);

    // Check existence
    if(hashSet.find(2) != hashSet.end()){
        std::cout << "2 is in the set." << std::endl;
    }

    // Iterate
    for(auto& val : hashSet){
        std::cout << val << " ";
    }
    std::cout << std::endl;

    return 0;
}
```

**Characteristics:**
- Average-case `O(1)` time complexity for insertions, deletions, and lookups.
- Uses separate chaining or open addressing for collision resolution.
- `std::unordered_map` stores key-value pairs, while `std::unordered_set` stores unique keys.

### Custom Hash Table Implementation

**Description:** Implementing a hash table manually using arrays and linked lists or other collision resolution strategies.

**Implementation Using Separate Chaining:**

```cpp
#include <iostream>
#include <vector>
#include <list>
#include <string>

class HashTable {
private:
    int bucketCount;
    std::vector<std::list<std::pair<std::string, int>>> table;

    int hashFunction(const std::string& key) const {
        std::hash<std::string> hash_fn;
        return hash_fn(key) % bucketCount;
    }

public:
    HashTable(int size=10) : bucketCount(size), table(size) {}

    void insert(const std::string& key, int value){
        int idx = hashFunction(key);
        for(auto& pair : table[idx]){
            if(pair.first == key){
                pair.second = value; // Update existing key
                return;
            }
        }
        table[idx].emplace_back(key, value);
    }

    bool search(const std::string& key, int& value) const {
        int idx = hashFunction(key);
        for(auto& pair : table[idx]){
            if(pair.first == key){
                value = pair.second;
                return true;
            }
        }
        return false;
    }

    void remove(const std::string& key){
        int idx = hashFunction(key);
        table[idx].remove_if([&key](const std::pair<std::string, int>& pair) {
            return pair.first == key;
        });
    }

    void display() const {
        for(int i=0; i<bucketCount; ++i){
            std::cout << "Bucket " << i << ": ";
            for(auto& pair : table[i]){
                std::cout << "(" << pair.first << ", " << pair.second << ") ";
            }
            std::cout << std::endl;
        }
    }
};

int main(){
    HashTable ht(5);
    ht.insert("apple", 3);
    ht.insert("banana", 5);
    ht.insert("orange", 2);
    ht.insert("apple", 4); // Update value
    ht.display();

    int value;
    if(ht.search("banana", value)){
        std::cout << "banana: " << value << std::endl;
    }

    ht.remove("orange");
    ht.display();

    return 0;
}
```

**Characteristics:**
- Customizable bucket size and hash functions.
- Requires handling collision resolution (e.g., separate chaining, open addressing).
- More control but requires careful implementation to handle edge cases and ensure efficiency.

---

## 7. Graphs

Graphs are collections of nodes (vertices) connected by edges. They can be directed or undirected, weighted or unweighted.

### Adjacency Matrix

**Description:** A 2D array where `matrix[i][j]` indicates the presence (and possibly weight) of an edge from vertex `i` to vertex `j`.

**Implementation:**

```cpp
#include <iostream>
#include <vector>

class Graph {
private:
    int V;
    std::vector<std::vector<int>> adjMatrix;

public:
    Graph(int vertices) : V(vertices), adjMatrix(vertices, std::vector<int>(vertices, 0)) {}

    void addEdge(int u, int v, int weight=1){
        adjMatrix[u][v] = weight;
        // For undirected graph
        adjMatrix[v][u] = weight;
    }

    void display() const {
        for(int i=0; i<V; ++i){
            for(int j=0; j<V; ++j){
                std::cout << adjMatrix[i][j] << " ";
            }
            std::cout << std::endl;
        }
    }
};

int main(){
    Graph g(4);
    g.addEdge(0,1);
    g.addEdge(0,2);
    g.addEdge(1,2);
    g.addEdge(2,3);
    g.display();
    /*
    Outputs:
    0 1 1 0 
    1 0 1 0 
    1 1 0 1 
    0 0 1 0 
    */
    return 0;
}
```

**Characteristics:**
- Efficient for dense graphs.
- `O(V^2)` space complexity.
- Quick edge lookups (`O(1)`).

### Adjacency List

**Description:** An array of lists where each list contains the neighbors of a vertex.

**Implementation:**

```cpp
#include <iostream>
#include <vector>
#include <list>

class Graph {
private:
    int V;
    std::vector<std::list<int>> adjList;

public:
    Graph(int vertices) : V(vertices), adjList(vertices) {}

    void addEdge(int u, int v){
        adjList[u].push_back(v);
        adjList[v].push_back(u); // For undirected graph
    }

    void display() const {
        for(int i=0; i<V; ++i){
            std::cout << i << ": ";
            for(auto& neighbor : adjList[i]){
                std::cout << neighbor << " ";
            }
            std::cout << std::endl;
        }
    }
};

int main(){
    Graph g(4);
    g.addEdge(0,1);
    g.addEdge(0,2);
    g.addEdge(1,2);
    g.addEdge(2,3);
    g.display();
    /*
    Outputs:
    0: 1 2 
    1: 0 2 
    2: 0 1 3 
    3: 2 
    */
    return 0;
}
```

**Characteristics:**
- Efficient for sparse graphs.
- `O(V + E)` space complexity.
- Iterating over neighbors is efficient.

### Edge List

**Description:** A list of all edges represented as pairs or triplets (for weighted graphs).

**Implementation:**

```cpp
#include <iostream>
#include <vector>
#include <utility> // For std::pair

class Graph {
private:
    int V;
    std::vector<std::pair<int, int>> edgeList;

public:
    Graph(int vertices) : V(vertices) {}

    void addEdge(int u, int v){
        edgeList.emplace_back(u, v);
    }

    void display() const {
        for(auto& edge : edgeList){
            std::cout << edge.first << " - " << edge.second << std::endl;
        }
    }
};

int main(){
    Graph g(4);
    g.addEdge(0,1);
    g.addEdge(0,2);
    g.addEdge(1,2);
    g.addEdge(2,3);
    g.display();
    /*
    Outputs:
    0 - 1
    0 - 2
    1 - 2
    2 - 3
    */
    return 0;
}
```

**Characteristics:**
- Simple representation.
- `O(E)` space complexity.
- Useful for algorithms that process edges directly (e.g., Krusky's algorithm).

---

## 8. Sets and Maps

Sets and maps are collections of unique elements and key-value pairs, respectively. C++ offers both ordered and unordered variants.

### Using `std::set` and `std::map`

**Description:** Ordered containers typically implemented as red-black trees.

**Implementation of `std::set`:**

```cpp
#include <iostream>
#include <set>

int main(){
    std::set<int> orderedSet;
    orderedSet.insert(3);
    orderedSet.insert(1);
    orderedSet.insert(2);
    orderedSet.insert(2); // Duplicate ignored

    for(auto& val : orderedSet){
        std::cout << val << " "; // Outputs: 1 2 3
    }
    std::cout << std::endl;

    return 0;
}
```

**Implementation of `std::map`:**

```cpp
#include <iostream>
#include <map>
#include <string>

int main(){
    std::map<int, std::string> orderedMap;
    orderedMap[2] = "Two";
    orderedMap[1] = "One";
    orderedMap[3] = "Three";

    for(auto& pair : orderedMap){
        std::cout << pair.first << ": " << pair.second << std::endl;
    }
    /*
    Outputs:
    1: One
    2: Two
    3: Three
    */
    return 0;
}
```

**Characteristics:**
- Ordered by keys.
- `O(log n)` time complexity for insertions, deletions, and lookups.
- Automatically sorted.
- No duplicate keys.

### Using `std::unordered_set` and `std::unordered_map`

**Description:** Unordered containers implemented using hash tables.

**Implementation of `std::unordered_set`:**

```cpp
#include <iostream>
#include <unordered_set>

int main(){
    std::unordered_set<int> unorderedSet;
    unorderedSet.insert(3);
    unorderedSet.insert(1);
    unorderedSet.insert(2);
    unorderedSet.insert(2); // Duplicate ignored

    for(auto& val : unorderedSet){
        std::cout << val << " "; // Order not guaranteed
    }
    std::cout << std::endl;

    return 0;
}
```

**Implementation of `std::unordered_map`:**

```cpp
#include <iostream>
#include <unordered_map>
#include <string>

int main(){
    std::unordered_map<int, std::string> unorderedMap;
    unorderedMap[2] = "Two";
    unorderedMap[1] = "One";
    unorderedMap[3] = "Three";

    for(auto& pair : unorderedMap){
        std::cout << pair.first << ": " << pair.second << std::endl;
    }
    /*
    Outputs (order not guaranteed):
    1: One
    2: Two
    3: Three
    */
    return 0;
}
```

**Characteristics:**
- Unordered; no specific ordering of elements.
- Average-case `O(1)` time complexity for insertions, deletions, and lookups.
- No duplicate keys.

### Custom Implementation

Implementing ordered or unordered sets and maps manually involves replicating the underlying data structures like binary search trees or hash tables. Given the complexity, it's recommended to use the Standard Library unless specific custom behavior is required.

---

## 9. Disjoint Sets (Union-Find)

**Description:** Data structure that keeps track of a set of elements partitioned into disjoint (non-overlapping) subsets. Useful in algorithms like Krusky's for finding Minimum Spanning Trees.

**Implementation Using Parent Array and Union by Rank with Path Compression:**

```cpp
#include <iostream>
#include <vector>

class UnionFind {
private:
    std::vector<int> parent;
    std::vector<int> rank;

public:
    UnionFind(int size){
        parent.resize(size);
        rank.resize(size, 0);
        for(int i=0; i<size; ++i)
            parent[i] = i;
    }

    int findSet(int x){
        if(parent[x] != x)
            parent[x] = findSet(parent[x]); // Path compression
        return parent[x];
    }

    void unionSet(int x, int y){
        int rootX = findSet(x);
        int rootY = findSet(y);
        if(rootX == rootY) return;

        // Union by rank
        if(rank[rootX] < rank[rootY]){
            parent[rootX] = rootY;
        }
        else{
            parent[rootY] = rootX;
            if(rank[rootX] == rank[rootY])
                rank[rootX]++;
        }
    }
};

int main(){
    UnionFind uf(5);
    uf.unionSet(0,1);
    uf.unionSet(1,2);
    uf.unionSet(3,4);
    std::cout << uf.findSet(0) << std::endl; // Outputs root of set containing 0
    std::cout << uf.findSet(4) << std::endl; // Outputs root of set containing 4
    uf.unionSet(2,4);
    std::cout << uf.findSet(0) << std::endl; // Now 0 and 4 are in the same set
    return 0;
}
```

**Characteristics:**
- Efficient `find` and `union` operations (`O(α(n))`, where α is the inverse Ackermann function, practically constant).
- Useful in partitioning elements into disjoint sets.
- Optimized with path compression and union by rank.

---

## 10. Other Data Structures

### Bitset

**Description:** Fixed-size sequence of N bits. Efficient for space and certain bitwise operations.

**Implementation Using `std::bitset`:**

```cpp
#include <iostream>
#include <bitset>

int main(){
    std::bitset<8> bits(42); // 00101010
    std::cout << bits << std::endl;

    bits.set(0); // Set bit 0
    bits.reset(1); // Reset bit 1
    bits.flip(2); // Flip bit 2
    std::cout << bits << std::endl;

    std::cout << bits.to_ulong() << std::endl; // Convert to unsigned long
    return 0;
}
```

**Characteristics:**
- Fixed size known at compile time.
- Efficient for storing and manipulating bits.
- Supports bitwise operations.

### Bloom Filter

**Description:** Probabilistic data structure for set membership tests, allowing false positives but no false negatives.

**Implementation:**

Implementing a Bloom filter involves multiple hash functions and bit manipulation. Here's a simplified example:

```cpp
#include <iostream>
#include <vector>
#include <functional>

class BloomFilter {
private:
    std::vector<bool> bitArray;
    int size;
    std::hash<std::string> hashFn1;
    std::hash<std::string> hashFn2;

public:
    BloomFilter(int sz) : size(sz), bitArray(sz, false) {}

    void add(const std::string& s){
        size_t hash1 = hashFn1(s) % size;
        size_t hash2 = hashFn2(s) % size;
        bitArray[hash1] = true;
        bitArray[hash2] = true;
    }

    bool possiblyContains(const std::string& s) const {
        size_t hash1 = hashFn1(s) % size;
        size_t hash2 = hashFn2(s) % size;
        return bitArray[hash1] && bitArray[hash2];
    }
};

int main(){
    BloomFilter bf(100);
    bf.add("apple");
    bf.add("banana");

    std::cout << std::boolalpha;
    std::cout << bf.possiblyContains("apple") << std::endl;   // Outputs: true
    std::cout << bf.possiblyContains("banana") << std::endl;  // Outputs: true
    std::cout << bf.possiblyContains("orange") << std::endl;  // Outputs: false (most likely)
    return 0;
}
```

**Characteristics:**
- Space-efficient.
- Allows for fast set membership checks.
- Possibility of false positives, but no false negatives.
- Useful in scenarios where space is limited and some uncertainty is acceptable.

### Skip List

**Description:** Probabilistic data structure that allows fast search within an ordered sequence of elements, similar to balanced trees.

**Implementation:**

Implementing a full skip list is complex. Here's a simplified version focusing on insertion and search.

```cpp
#include <iostream>
#include <cstdlib>
#include <ctime>
#include <vector>

struct Node {
    int data;
    std::vector<Node*> forward;
    Node(int val, int level) : data(val), forward(level, nullptr) {}
};

class SkipList {
private:
    int MAX_LEVEL;
    float P;
    int level;
    Node* header;

    int randomLevel(){
        int lvl = 1;
        while(((float)std::rand()/RAND_MAX) < P && lvl < MAX_LEVEL)
            lvl++;
        return lvl;
    }

public:
    SkipList(int maxLevel=16, float p=0.5) : MAX_LEVEL(maxLevel), P(p), level(1){
        header = new Node(-1, MAX_LEVEL);
    }

    void insert(int val){
        std::vector<Node*> update(MAX_LEVEL, nullptr);
        Node* x = header;

        for(int i=level-1; i>=0; --i){
            while(x->forward[i] != nullptr && x->forward[i]->data < val)
                x = x->forward[i];
            update[i] = x;
        }

        x = x->forward[0];

        if(x == nullptr || x->data != val){
            int lvl = randomLevel();
            if(lvl > level){
                for(int i=level; i<lvl; ++i)
                    update[i] = header;
                level = lvl;
            }
            Node* newNode = new Node(val, lvl);
            for(int i=0; i<lvl; ++i){
                newNode->forward[i] = update[i]->forward[i];
                update[i]->forward[i] = newNode;
            }
        }
    }

    bool search(int val) const {
        Node* x = header;
        for(int i=level-1; i>=0; --i){
            while(x->forward[i] != nullptr && x->forward[i]->data < val)
                x = x->forward[i];
        }
        x = x->forward[0];
        return x != nullptr && x->data == val;
    }

    void display() const {
        for(int i=0; i<level; ++i){
            Node* x = header->forward[i];
            std::cout << "Level " << i+1 << ": ";
            while(x){
                std::cout << x->data << " ";
                x = x->forward[i];
            }
            std::cout << std::endl;
        }
    }

    ~SkipList(){
        Node* current = header->forward[0];
        while(current){
            Node* next = current->forward[0];
            delete current;
            current = next;
        }
        delete header;
    }
};

int main(){
    std::srand(std::time(0));
    SkipList sl;
    sl.insert(3);
    sl.insert(6);
    sl.insert(7);
    sl.insert(9);
    sl.insert(12);
    sl.insert(19);
    sl.insert(17);
    sl.insert(26);
    sl.insert(21);
    sl.insert(25);

    sl.display();

    std::cout << std::boolalpha;
    std::cout << sl.search(19) << std::endl; // Outputs: true
    std::cout << sl.search(15) << std::endl; // Outputs: false
    return 0;
}
```

**Characteristics:**
- Average-case `O(log n)` time complexity for search, insert, and delete.
- Simpler to implement than balanced trees.
- Uses multiple levels with probabilistic balancing.
