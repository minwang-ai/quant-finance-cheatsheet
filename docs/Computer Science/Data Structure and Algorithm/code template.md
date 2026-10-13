# Data Structure
## Linked List
Tips:
It's important to build an intuition behind how to correctly **re-assign pointers**. The best way is to see the process visually through **examples**. 
### Singly-Linked List

#### Definition - Singly-Linked List - Use Raw Pointer
Python
```python
class ListNode:
    def __init__(self, val):        # O(1)
        self.val = val
        self.next = None
    
    # get the node with specific offset away
    def later_node_recursion(self, offset):
        if offset == 0:     # base case
            return self
        
        if offset < 0:
            raise ValueError("offset must be non-negative")   
        if self.next is None:
            raise IndexError("offset exceeds list length")

        return self.next.later_node_recursion(offset - 1)   # time complexity: O(offset), space: O(offset)
    
    def later_node_iterative(self, offset):
        if offset < 0:
            raise ValueError("offset must be non-negative")
        
        curr_node = self
        for _ in range(offset): # time complexity: O(offset), space: O(1)
            if curr_node.next is None:
                raise IndexError("offset exceeds list length")
            curr_node = curr_node.next

        return curr_node

# example linked list
one = ListNode(1)
two = ListNode(2)
three = ListNode(3)
head = one
one.next = two
two.next = three
```
C++
```cpp
struct ListNode {
      int val;
      ListNode *next;
      // constructor overloading
      ListNode() : val(0), next(nullptr) {}
      ListNode(int val) : val(val), next(nullptr) {}
      ListNode(int val, ListNode *next) : val(val), next(next) {}
  };


int main() {
    // Dynamically allocate nodes on heap memory
    LinkedListNode* one = new LinkedListNode(1);  
    LinkedListNode* two = new LinkedListNode(2); 
    LinkedListNode* three = new LinkedListNode(3);

    LinkedListNode* head = one; // head points to the first node (one)
    // Connecting the nodes to form: one -> two -> three
    one->next = two; // memory address assignment    
    two->next = three;      

    // In practice, we need to delete these nodes using `delete` to avoid memory leaks.
}
```
#### Definition - Singly-Linked List - Use Modern C++ Smart Pointer
```cpp
#include <memory>

struct ListNode {
    int val;
    std::unique_ptr<LinkedListNode> next; // unique ownership
    // constructor overloading
    ListNode() : val(0), next(nullptr) {}
    ListNode(int val) : val(val), next(nullptr) {}
    ListNode(int val, ListNode *next) : val(val), next(next) {}
};

int main() {
    // no raw pointers or manual deletion
    auto one = std::make_unique<LinkedListNode>(1); // create ListNode object, smart unique pointer own this node 1.
    auto two = std::make_unique<LinkedListNode>(2);
    one->next = std::move(two); // ownership transferred (then previous pointer two becomes nullptr)

    // No need for manual delete, smart pointers handle it automatically
}
```
#### Add/Delete Node - Singly-Linked List
At first, obtain the **reference** to the **previous node** `prev` (the node at position $i - 1$) by iterating from the head.
Typically we do these operations **on the fly**, when iterating through the list (these functions are just demonstration). 

*Figure: **Singly Linked List** - **insert** at **random** position: `node_to_add.next`  points to `preNode.next`, then change `preNode.next` points to `node_to_add`*
![linked list Insert](figures/singly-linked-list-insert-random.png)

*Figure: **Singly Linked List** - **Delete** at **random** position: change `preNode.next` pointer to `preNode.next.next`*
![linked list Insert](figures/singly-linked-list-delete-random.png)

Python
```python
# Obtain the reference by iterating from the head - time: O(n)
def add_node(prev_node, node_to_add):   # Time: O(1)
    node_to_add.next = prev_node.next
    prev_node.next = node_to_add

def delete_node(prev_node):
    prev_node.next = prev_node.next.next
```
C++
```cpp
// Obtain the reference by iterating from the head - time: O(n)
void addNode(ListNode* prevNode, ListNode* nodeToAdd) {
    nodeToAdd->next = prevNode->next;   // Time: O(1)
    prevNode->next = nodeToAdd;
}

void deleteNode(ListNode* prevNode) {
    prevNode->next = prevNode->next->next;
}
```

### Traverse the Linked List 
Example: 
get the sum of all values from an integer linked list.
#### Traverse - Iterative
Using **dummy pointers** `curr` **without losing** a reference to the **head**.


Python
```python 
def get_sum(head):
    # ans = 0
    curr = head
    
    while curr: # The final node's next pointer is null. Therefore, after the final node, the while loop ends.
        # ans += curr.val
        curr = curr.next   

    return ans
```
C++
```cpp
int getSum(ListNode* head) {
    //int ans = 0;
    ListNode* curr = head;
    while (curr != nullptr) {
        // ans += curr->val;
        curr = curr->next;
    }

    return ans;
}
```
#### Traverse - Recursive
Python
```python 
def get_sum(curr):
    if not curr:
        return 0
    
    return curr.val + get_sum(curr.next)
```
C++
```cpp
int getSum(ListNode* curr) {
    if (curr == nullptr) {
        return 0;
    }

    return curr->val + getSum(curr->next);
}
```


### Doubly linked list
*Figure: **Doubly linked list** - similar to singly linked list, but each node also contains a pointer to the **previous** node `prev`, and it allows iteration in **both directions**.*
![Doubly linked list](figures/doubly-linked-list.png)

#### Definition - Doubly linked list
Python
```python
class ListNode:
    def __init__(self, val):
        self.val = val
        self.next = None
        self.prev = None
```
C++
```cpp
struct ListNode {
    int val;
    ListNode *next;
    ListNode *prev;

    ListNode() : val(0), next(nullptr), prev(nullptr) {}
    ListNode(int val) : val(val), next(nullptr), prev(nullptr) {}
    ListNode(int val, ListNode* next, ListNode* prev) : val(val), next(next), prev(prev) {}
};
```

#### Add/Delete Node - Doubly-Linked List
With a doubly linked list, we only need a reference to the **current node** at $i$, because we can simply reference the `prev` pointer of that node to get the node at $i - 1$, and `next` pointer of that node to get the node at $i + 1$,

Extra work: **update** the **`prev`** pointers


*Figure: **Doubly Linked List** - **insert** at **random** position: `node_to_add.next` points to `curr_node`, `node_to_add.prev` points to `prev_node`, `prev_node.next` points to `curr_node`, `curr_node.prev` points to `curr_node`*
![linked list Insert](figures/doubly-linked-list-insert-random.png)
Python
```python
def add_node(curr_node, node_to_add):
    # get prev node reference
    prev_node = curr_node.prev  
    # relink
    node_to_add.next = curr_node
    node_to_add.prev = prev_node
    prev_node.next = node_to_add
    curr_node.prev = node_to_add
```
C++
```cpp
void addNode(ListNode* currNode, ListNode* nodeToAdd) {
    ListNode* prevNode = currNode->prev;
    nodeToAdd->next = currNode;
    nodeToAdd->prev = prevNode;
    prevNode->next = nodeToAdd;
    currNode->prev = nodeToAdd;
}
```
*Figure: **Doubly Linked List** - **delete** at **random** position: `prev_node_next`  points to `next_node`, then change `next_node.prev` points to `prev_node`*
![Doubly linked list Delete](figures/doubly-linked-list-delete-random.png)


```python
def delete_node(curr_node):
    # get prev, next node reference
    prev_node = curr_node.prev
    next_node = curr_node.next  
    # relink
    prev_node.next = next_node
    next_node.prev = prev_node
```
C++
```cpp
void deleteNode(ListNode* currNode) {
    ListNode* prevNode = currNode->prev;
    ListNode* nextNode = currNode->next;
    prevNode->next = nextNode;
    nextNode->prev = prevNode;
}
```
#### Add/Delete First/Last node using sentinel nodes(`head`, `tail`) - Doubly-Linked lists 
To easily add and remove at the end or tail of the linked list


*Figure: **Doubly Linked List** - with **sentinel nodes**(`head`, `tail`). Even when there are no nodes in a linked list, you still keep a head and tail. The real head node of the linked list is **`head.next`** and the real tail node is **`tail.prev`**. The sentinel nodes themselves are not part of linked list.*
![Doubly linked list with sentinel](figures/doubly-linked-list-w-sentinel-nodes.png)

*Figure: **Doubly Linked List** - with **sentinel nodes**(`head`, `tail`). **insert** at start/end*
![Doubly linked list with sentinel insert](figures/doubly-linked-list-w-sentinel-nodes-insert-start-end.png)

*Figure: **Doubly Linked List** - with **sentinel nodes**(`head`, `tail`). **delete** at start/end*
![Doubly linked list with sentinel delete](figures/doubly-linked-list-w-sentinel-nodes-delete-start-end.png)


Python
```python
def add_to_start(node_to_add):
    node_to_add.prev = head
    node_to_add.next = head.next
    head.next.prev = node_to_add
    head.next = node_to_add

def add_to_end(node_to_add):
    node_to_add.next = tail
    node_to_add.prev = tail.prev
    tail.prev.next = node_to_add
    tail.prev = node_to_add

def remove_from_start():
    if head.next == tail:   # special case: empty 
        return
    # get reference
    node_to_remove = head.next  
    # relink
    node_to_remove.next.prev = head
    head.next = node_to_remove.next

def remove_from_end():
    if head.next == tail:   # special case: empty
        return
    # get reference
    node_to_remove = tail.prev
    # relink
    node_to_remove.prev.next = tail
    tail.prev = node_to_remove.prev

# create empty linked list with sentinel nodes
head = ListNode(None)
tail = ListNode(None)
head.next = tail
tail.prev = head
```
C++
```cpp
void addToStart(ListNode* nodeToAdd) {
    nodeToAdd->prev = head;
    nodeToAdd->next = head->next;
    head->next->prev = nodeToAdd;
    head->next = nodeToAdd;
}

void addToEnd(ListNode* nodeToAdd) {
    nodeToAdd->next = tail;
    nodeToAdd->prev = tail->prev;
    tail->prev->next = nodeToAdd;
    tail->prev = nodeToAdd;
}

void removeFromStart() {
    if (head->next == tail) {
        return;
    }

    ListNode* nodeToRemove = head->next;
    nodeToRemove->next->prev = head;
    head->next = nodeToRemove->next;
}

void removeFromEnd() {
    if (head->next == tail) {
        return;
    }

    ListNode* nodeToRemove = tail->prev;
    nodeToRemove->prev->next = tail;
    tail->prev = nodeToRemove->prev;
}

ListNode* head = new ListNode(-1);
ListNode* tail = new ListNode(-1);
head->next = tail;
tail->prev = head;
```

### Reversing a singly-linked list 
a typical **problem** or an **intermediate step**

Python
```python
def reverse_list(head):
    prev = None               # to track the previous node
    curr = head               # to track the current node 

    while curr:               # traverse until the tail 
        next_node = curr.next # 1. keep a reference to the original next node, make sure we don't lose it
        curr.next = prev      # 2. reverse the direction of the next pointer
        prev = curr           # 3. Update prev for the next iteration
        curr = next_node      # 4. Update curr for the next iteration
        
    return prev               # After the final iteration, prev points to the original tail, which is the new head
``` 


