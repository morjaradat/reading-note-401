# Trees

## Common Terminology

A tree node is a component which may contain it’s own values, and references to other nodes .the node in the beginning of the tree called a Root and the number of children that any node can handle is called K ;In binary tree there are two references on called right and other called left and the link between the parent and the child is called edge and the node that does not have and children called leaf and the number if links from the Root(the beginning) to the grater distance  of leaf called height.

## Traversals

- There are two categories of traversals in trees:

1. Depth First
2. Breadth First

### Depth First

- traversal is where we prioritize going through the depth (height) of the tree first.
- there are multiple ways to traverse by depth first and each method have its own direction to start travel .
- there are three methods for the depth first :

1. Pre-order: root >> left >> right
2. In-order: left >> root >> right
3. Post-order: left >> right >> root

- The most common way to traverse in tree is use recursion .

**pre-order**

- its mean with way the root will look first and that depend on the value of left or right
- its order left > root > right
- we pop up only the node when its a leaf (dose not have any children)

- that applied on other depth first method.
- The biggest difference between each of the traversals is when you are looking at the root node.

### Breadth First

- its done by travel level by level in the tree.
- breadth first traversal uses a queue .

## Binary Tree Vs K-ary Trees

- Binary Trees restrict the number of children to two.

### K-ary Trees

- when node have more than two children we called k-ary
- k is the maximum number of children than node can have .

**Breadth First Traversal**

- Traversing a K-ary tree requires a similar approach to the breadth first traversal.
- we travel in the tree depend on the number of node that connect to the root node.
- With every Node we dequeue, we check it’s list of children and enqueue each one the child that have most of children will be the first .
- when we dequeue a node we enqueue his children.

### Adding a node

- because there are no structures in tree that mean its doesn't matter where you add new node .
- to add a new node its with strategy that fill all child spot from top to bottom.
- if the node have no child we fill it from left to right.

### Big O

- The Big O time complexity  :

1. its for inserting a new node is O(n)
2. Searching for a specific node will also be O(n); where the n is the number of item.

- The Big O space complexity  :

1. its for a node insertion using breadth first insertion will be O(w)
2. where w is the largest width of the tree.

- A “perfect” binary tree is one where every non-leaf node has exactly two children.
- The maximum width for a perfect binary tree, is 2^(h-1) .
- h is the height of the tree.
- Height can be calculated as log n, where n is the number of nodes.

## Binary Search Trees (BST)

- its type of tree that have some structure attached to it.
- node are arranged on order where is the the value highest than the Root are go to teh right and the value its smaller than the Root go to the left.

### Searching a BST

- Searching a BST can be done quickly, because all you do is compare the node you are searching for against the root of the tree or sub-tree.
- if the value smaller you will travel to the left else you will travel to the right.
- The best way to approach a BST search is with a while loop.

### Big O

- The Big O time complexity of a Binary Search Tree’s insertion and search operations is O(h), or O(height).
- The Big O space complexity of a BST search would be O(1).
