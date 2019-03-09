## Linked Lists

![Linked Lists](images/linkedlists_final.png)

Linked Lists are a reference based data structure. This is opposed to an indexed or key based data structure such as a JavaScript Array or Object. An exmaple of this is a Linked List is a train.

We have our engine, and an arbitrary number of following cars. The _n<sup>th</sup>_ car is reliant on the _n<sup>th</sup> - 1_ to stay connected. It does not "know" about the other cars in the train, just the one before it.

### History

In a language like C, Arrays are instantiated as follows:

```
int integerArray[10]
```

This defines an Array, that only is allowed to possess Integers, and can have no more than 10 items in it. We were not allowed to just `.push` an arbitrary amount of items, of multiple types, into an Array like in JavaScript.

When we want to add items to this C Array, we would need to create a new one of double the length (by convention), copy over all the current items, and add the new ones, then delete the old Array.

This can get either tedious, or expensive, particularly based on the data.

Linked Lists are a way to keep adding items to an Array, without having to go through the whole protocol of Array doublling and copying.

### Structure

```
// Array
  0  1  2  3
[ 4, 5, 2, 7 ]

// Linked List
(4) -> (5) -> (2) -> (7)
```

Linked Lists are comprised of Nodes. A Node has a value (in the example above, an Integer), and a reference, which is always another Node. Some skeleton code for a Node is below.

```
function Node(val, ref) {
  this.value = val
  this.reference = ref
}

var n = new Node(1)
var m = new Node(2, n)
```

We could call methods like `n.reference` or `n.value` but we always need to remember that `n` is our first Node. Which can get tough in a program to remember. We need something to wrap all these Nodes and be able to call functions. This is where a Linked List object comes in.

Below is the `LinkedList` object, in conjunction with a recursive add function. By default, in our Linked List, we add to the end of the list. We call the first Node in the LinkedList the `head`. This is always our starting point for operating on a LinkedList due to our reference based structure.

```
function Node(val) {
  this.value = val
  this.reference = null
}

function LinkedList() {
  this.head = null

  this.add = function(val) {
    if (this.head == null) {
      this.head = new Node(val)
    } else {
      recursiveAdd(val, this.head)
    }
  }

  // a closure to keep the concept of a "private" function
  function recursiveAdd(val, node) {
    if (node.reference == null) {
      node.reference = new Node(val)
    } else {
      recursiveAdd(val, node.reference)
    }
  }
}
```
[repl.it](https://repl.it/repls/JointPeachpuffAgama)

Instantiation and calling methods on our Linked List would look like:
```
ll = new LinkedList()
ll.add(1) // HEAD -> (1)
ll.add(2) // HEAD -> (1) -> (2)
// etc.
```

### Advantages

Using the Array `[1,2,3]` as an example. What if we wanted to add `4` in between the `2` and `3`?

If we're in C, and have no more room, we need to do our double/copy/delete original funciton. If we're in JavaScript, or C when we have room, we need to then shift every element over in the Array, the place the item at the correct index. This is an _O(n)_ function.

For a LinkedList, placing at the a new Node/value anywhere but the end of will be less than _n_ operations. We can simply re-arrange the references. There is not shifting of Nodes.

```
// Pseudocode for addBefore(beforeVal, val)

Traverse Nodes
  If the current Node's reference's value is equal to what we're looking for
    The Node to be inserted's reference becomes the current Node's reference
    The current Node's reference becomes the Node to be inserted
```

### Disadvantages

When we want to add on to our list, we need to iterate over the size of the list in order to get to the end, then append. It is an _O(n)_ function.

In addition, retrieving a specific element is also an _O(n)_ operation.

Because Arrays operate in an indexed fashion, and if it does not need to grow (sucy as a JavaScript or other scripting langauge Array), it is an O(1) operation.

### Conclusion

Linked Lists are an important structure for allowing operations to be done and our list to be maintained in a better fashion than an Array, based on their use case.

Today, Ruby's Array, Python's List, Java's ArrayList and so forth are dynamic. They grow and resize for us and we don't need to need work about our C Array protocols. In addition, they have a lot of useful methods already built in. While they, Linked Lists, may go unused, other structures utilize them and are built off of Linked Lists (such as Trees). It is useful to understand the concept of a Linked List in order to grasp further concepts in this text.

### Questions

#### #1

Implement the above `addBefore` function. It should accept two arguments, the value to find and the value to add before the "found" value.

#### #2

Implement `remove`. This function accepts one argument of a value to be removed from the LinkedList.

> _Hint: Be careful with references_

#### #3

Implement `clear`. This clears the Linked List, meaning it is empty.

[Answers to 1 through 3](https://repl.it/repls/RegularMundaneSpiketail)

#### #4

Implement a "tail pointer" in a Linked List. In addition, add `.previous` to your Node object. This is called a "doubly linked list".

[Answer](https://repl.it/repls/TransparentFavoriteWolverine)

### More Sites

- [HackerRank on Linked Lists](https://www.youtube.com/watch?v=njTh_OwMljA)
- [Wikipedia](https://en.wikipedia.org/wiki/Linked_list)
- [Dynamic Arrays](https://en.wikipedia.org/wiki/Dynamic_array)


