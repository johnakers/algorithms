## Trees

![Trees](images/trees_1_final.png)

Trees, at first glance, are very similar to Linked Lists. They are comprised of Nodes, just like a Linked List but they have two main differences.

1. Terminology
2. Each Every Node can have multiple references

```
Fig. 1

         (A)
        /   \
     (B)     (C)
    /           \
 (D)             (E)
```

Instead of a `head`, we have a `root`, our Node labelled _A_. _A_'s `children` (not `references`) are _B_ and _C_. There _B_ and _C_'s `parent` is _A_. We would say our "leaf Nodes", Nodes that have no `children`, are _D_ and _E_. In addition, _D_ and _E_ have a common `ancestor` in _A_.

In addition, this Tree would have a depth of 2. We can also have a Tree that looks like the below. Unless we specify a type of Tree, by default there are no limit to the number of `children` per Node but a Tree is always defined by having a `root`.

The above figure is a very simple Tree. Each Node (called `TreeNode` for this instance) would look like the below, in code:

```
function TreeNode(value) {
  this.value = value
  this.children = []
}
```

```
Fig. 2

             (A)
            / | \
         (B) (C) (D)
```

### Breadth First Search

Breadth First Search (BFS) is an algorithm that goes through our Tree, in each level, and returns and/or examines in the Nodes, by level of the Tree.

For instance, in _Fig. 1_, we would return the following order: _A_, _B_, _C_, __D, _E_.

When our Tree is very wide, this algorithm can be a bit slow but may be advisable to use when our Tree is a skinny and has many levels.

### Depth First Search

Depth First Search (DFS) is an algorithm that goes through our Tree, getting all the way to the bottom, then coming back up, going through each first child, recursively, labelling it discovered and moving on to the next.

In _Fig. 2_, we would return the following order: _A_, _B_, _D_, _C_, _E_.

Notice the difference from BFS, where we get to the bottom of the Tree quickly. This is optimal for a shallow Tree, that may be a bit on the wider side.

### Binary Trees

Binary Trees put some conditions are our Nodes.

1. Each Node may only have 2 children
2. The `left_child` must have a lesser value than the `parent`
3. The `right_child` must have an equal or greater value than the `parent`

An example of our Binary Tree Node (`BTNode`) would look like, in code:

```
function BTNode(value) {
  this.value = value
  this.left_child = null
  this.right_child = null
}
```

And we will use a `BinaryTree` wrapper Object around our Nodes, much like our Linked List chapter.

```
function BinaryTree() {
  this.root = null

  this.add = function(value) {
    if (this.root == null) {
      this.root = new BTNode(value)
    } else {
      recursiveAdd(this.root, value)
    }
  }

  function recursiveAdd(node, value) {
    if (value >= node.value) {
      if (node.right_child == null) {
        node.right_child = new BTNode(value)
      } else {
        recursiveAdd(node.right_child, value)
      }
    } else {
      if (node.left_child == null) {
        node.left_child = new BTNode(value)
      } else {
        recursiveAdd(node.left_child, value)
      }
    }
  }
}
```

Like our LinkedList, we can utilize recursion for additions to our Binary Tree.

![trees2](images/trees_2_final.png)

### Questions

#### #1

Morse Code is an alphabet broken up into dashes and dots. [It is actually broken into a Binary Tree structure](https://en.wikipedia.org/wiki/Morse_code#/media/File:Morse_code_tree3.png).

Using the image provided, implement a Morse reader, that accepts a String as an argument

### #2

Implement a `delete(value)` method on our `BinaryTree`.

[Answer](#)

### #3

Based on the [Wikipedia Pseudocode](https://en.wikipedia.org/wiki/Breadth-first_search#Pseudocode), implement BFS on a Tree.

### #4

Based on the [Wikipedia Pseudocode](https://en.wikipedia.org/wiki/Depth-first_search), implement DFS on a Tree.

### Conclusion

Trees are an important data structure. The DOM in this webpage is a Tree. MongoDB, a popular No-SQL database, uses Trees. Object hierarchy and understanding inheritance as it pertains to programming can be displayed with a Tree.

Understanding them is important and leads into further data structures, such as the below mentioned Graphs.

### A quick note on Graphs

Graphs, to keep it short, are a "root-less" Tree. There is no one single starting point. They have Vertices (instead of Nodes) and Edges (instead of Children). They can be directional:

```
// B is an Edge to A but A is not an Edge to B

(A) -> (B)
```

Bi-directional:

```
// A and B are Edges to each other

(A) <-> (B)
```

or even contain a cycle:

```
// A to B to C to A ... etc.

(A) -> (B)
  ^    /
   \  v
    (C)
```

LinkedIn, your friends on Twitter or Facebook and other popular apps all utilize a Graph in order to give you "2nd degree relationships" and so forth.

In addition, we can use our DFS/BFS algorithms to search for a Vertex. For the purpose overall of this text, I won't go into them too much but if you have the time and are interested, I highly reccomend checking it out.

We can also weight the Edges in a Graph. This allows us to represent travel time, scheduling and other applications.

## More Reading

- [Infix, Postfix and Prefi Notation](http://www.cs.man.ac.uk/~pjj/cs212/fix.html)
- [Other Types of Trees](https://en.wikipedia.org/wiki/List_of_data_structures#Trees)
- [Dijkstra's Algorithm](https://en.wikipedia.org/wiki/Dijkstra%27s_algorithm)



