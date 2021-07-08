# Stacks and Queues

## What is a Stack

- its data structure for node ,every nod point to the next node not to previous.

- Common terminology for a stack is :

1. push : added node to the last .
2. pop  remove last last node.
3. top  : review the last node .
4. peek : review the value of teh top (the last node).
5. IsEmpty : returns true when stack is empty otherwise returns false.

- Stacks follow these concepts:

1. FILO :  First In Last Out

- mean the first node added to the stack will be the last node will pop out from the stack.

2. LIFO: Last In First Out

- mean the last node added to the stack will be the first node will pop out from the stack.

## Stack Visualization

- Example of stack :

![img](./stack1.png)

### Push O(1)

- Push node to the stack will be always O(1) operation because it will take the same amount of time no matter how many nodes in the stack .

### Pop O(1)

- pop-off(remove) the last node of the stack ;we will check if the stack is empty first and then pop .

1. make node have the same point of the top named temp.
2. re-assign the top of the next node .
3. we can remove the node safely

### Peek O(1)

- When conducting a peek, you will only be inspecting the top Node of the stack.

### IsEmpty O(1)

- when its empty the top will be null .

## What is a Queue

- Common terminology for a queue is :

1. Enqueue : its node or item that added to the queue
2. Dequeue :  its node or item that remove to the queue and when the queue is empty.
3. Front  : the first node of the queue.
4. Rear  : the last node of the queue.
5. Peek  : see the value of the first node .
6. IsEmpty : returns true when queue is empty otherwise returns false.

- Queues follow these concepts:

1. FIFO : First In First Out

- its mean the first item of the queue will be the first item removed.

2. LILO : Last In Last Out

- its mean the last item of the queue will be the last item removed.

### Queue Visualization

- Example :

![img](./Queue.png)

### Enqueue O(1)

- when add item to the queue ,this have O(1) mean it will the same time how matter item in the queue.

- its done by make the last node (Rear) point to the new node .

### Dequeue O(1)

- remove an item from a queue and its have O(1) mean it will the same time how matter item in the queue.

- its done by create a temp and make it point to the front then make the next of the front the new front then we can remove the item .

### Peek O(1)

- you will see the value of the front(the first item)

### IsEmpty O(1)

- it will return true if the list not empty else will return false.
