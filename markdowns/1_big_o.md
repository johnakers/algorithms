## Big O

![Big O](images/bigO_1_final.png)

"Big O", or "Big O Notation", is a term used to describe a wider field of study. It is notation and related math that allows us to denote how big and how slow our programs are. Whether it be a video game, launching a rocket, a phone app or this web page, we want our apps to run fast and use as little memory as possible. Therefore, Big O is a notation that states the worst case scenario, or a "high water mark".

There are other notations (omega and theta), and they're interesting and I highly encourage you to read about them but for our purposes, and the practical purposes of writing code, we will solely focus on _O_ (Big O).

Below are some examples of Big O Notation ([also called the Bachmann-Landau notation](https://en.wikipedia.org/wiki/Big_O_notation#Family_of_Bachmann%E2%80%93Landau_notations)).

### Notation

#### O(1)

O(1), pronounced "Oh of one", means our program executes immediately, or in constant time, the same time in which our program was run. Regardless of the size of our data. Examples of this are conditionals and assigments.

```
var x = 5
if (x == 5) {
  console.log('x is five!')
}
```

Our program does not have to loop. We assigned `x`, and we put it through a conditional.

#### O(n)

_n_ is the number of items in our input. If we don't know exactly the number of items in our input to our program, as in algebra, we use _n_ by convention to denote it.

Our program will grow to the size of our input. This is called linear growth, where the number of operations our program has is in direct correlation to the input. In the below program, we would have to hypothetically go through every item in the collection to determine whether or not it is 5, in the worst case scenario. Hence, _O(n)_.

```
array = [ ? ] // an Array of unknown length

for (var i = 0; i < array.length; i++) {
  if (array[i] == 5) {
    return i
  }
}
```

#### O(n<sup>2</sup>)

While _O(n)_ grows to the same size as our input, _O(n<sup>2</sup>)_ grows to the square of our input. Meaning, if our input is a list of 4 items, we may have up to 16 operations. This usually comes about from the nesting of loops. The below code shows an example of this:

```
array = [ ? ] // an Array of unknown length

for (var i = 0; i < array.length; i++) {
  for (var j = 0; j < array.length; j++) {
    console.log('i is: ' + i)
    console.log('j is: ' + j)
  }
}
```

Another, perhaps more common example, that can occur during something like an API request or getting two distinct pices of data and then having to merge or alter them in some way.

```
array1 = [ ? ] // an Array of unknown length
array2 = [ ? ] // a separate Array of unknown length

for (var i = 0; i < array1.length; i++) {
  for (var j = 0; j < array1.length; j++) {
    console.log(array1[i] + array2[j])
  }
}
```

If we have a triple nested loop, using this above example, as you may have guessed we could say _O(n<sup>3</sup>)_.

While we can say that this should be _O(n * m)_ as they are distinct Arrays. Which does seem more algebraic at first glance, by convention we say this is still _O(n<sup>2</sup>)_.

The reason for this is, _n_ is entirely unknown. _m_ is also entirely unknown. They could be the same length, different, or having nothing them. Therefore _m_ is theorettically the same as _n_ in regards to a conceptual point of view on how our program speed will grow. Arguably, it makes it perhaps slightly easier to represent what is going on. For instance, what if we have 3 lists noted above? _O(n * m * o)_ doesn't roll off the tongue as well as "Oh of n cubed".

#### O(log n)

_O(log n)_ denotes that our program will grow with the log<sub>2</sub> of _n_. There are quite a few divide-and-conquer algorithms that filter our inputs log<sub>2</sub> times.

Logarithms can be thought of as "reverse exponents". For instance, 2^<sup>3</sup> is 8. Therefloore log<sub>2</sub>8 is 3. 

A great example of this is the [binary-search algorithm](https://en.wikipedia.org/wiki/Binary_search_algorithm#Procedure).

#### More notation

There are _O(n!)_ and _O(2<sup>n</sup>)_ notations as well. They are interesting but less common.

### Analyzing a program

When evaluating an entire program, we remove the constants.

```
a = [ ? ] // an Array of unknown length

for (var i = 0; i < array.length; i++) {
  console.log(i)
}

for (var i = 0; i < array.length; i++) {
  console.log(array[i])
}
```

We could say the above program would be _O(2n)_. We have 2 loops, not nested, that iterate over our entire list. For Big O, we care about the trend or rather "how" our program grows. _n_, versus _2n_, versus _100n_, they all grow in linear time.

We drop the constant, the 2, and say our program's Big O is _O(n)_.

Consider the below program:

```
array = [ ? ] // an Array of unknown length

for (var i = 0; i < array.length; i++) {
  if (array[i] == 5) {
    console.log('Found 5')
  }
}

for (var i = 0; i < array.length; i++) {
  for (var j = 0; j < array.length; j++) {
    if (j == i) {
      console.log('Found an interesting match!')
    }
  }
}

for (var i = 0; i < array.length; i++) {
  for (var j = 0; j < array.length; j++) {
    if (j == i) {
      console.log('Found an interesting match again!')
    }
  }
}
```

There's a lot going on in this program.

- The fist `array` assignment runs in _O(1)_
- The next loop runs in _O(n)_
- The next nested loop runs in _O(n<sup>2</sup>)
- The next nested loop runs in _O(n<sup>2</sup>) again

Mathematically, our program could look like:

```
O(1) + O(n) + O(n^2) + O(n^2)
```

We can then combine like terms:

```
O(1) + O(n) + 2O(n^2)
```

Drop our constants (remember, _O(1)_ is considered "constant time"):

```
O(n) + O(n^2)
```

And finally, for this example, we use the largest Big O found to represent our whole program.

```
O(n^2)
```

We do this because, what if our program had nothing but super fast _O(1)_ code but then we have our _O(n<sup>2</sup>)_ loop? Our program _has_ to run it and therefore, it becomes our "choke point". The slowest element that dictates the growth trend.

![Big O](images/bigO_2_final.png)

### Conclusion

Big O Notation is important for any field of software development. With that said, it is also a very deep and involved field that requires a lot of time to understand. Below, I've posted some links that I suggest reading or at least glancing at. The important "tweet sized" takeaway from this section is:

> _Nested loops are something to stray away from whenever possible. We determine the Big O of our program by the slowest block found, regardless of how fast everything else is. Big O is an indication of growth, not an exact amount._

### Questions

#### #1

We have a jar of 100 marbles. 50 red. 50 blue. They are mixed up randomly in the jar, and we cannot see into the jar. We pull a marble at random.

- How many pulls would it require to "prove" there are in fact 2 colors in the jar? (hint: What is the worst case scenario?)
- What is the Big O of our marble pulling?

[Answer](https://en.wikipedia.org/wiki/51)

#### #2

We created a sorting algorithm for a list that works as follows:

```
Start at the beginning of the list
Traverse the list
  Compare the current item, and the next, if there is one
  If the current item is greater than the next, swap them

Do this "n" number of times
```

An example is, the list `[ 5, 3, 7, 2, 1 ]` would look like `[ 5, 3, 2, 1, 7 ]` after the first traversal.

- Write code for the full function. Your code should take an Array/List as an argument and return a sorted Array/List.
- What is the Big O of this function?

[Answer](https://en.wikipedia.org/wiki/Bubble_sort)

#### #3

Write code to reverse a String in O(n) time? (Meaning we go through the String only once). Your code should accept a String, such as "John", and return a String "nhoJ".

For a more advanced challenge, do not create a new String. Return the same String.

[Answer](https://repl.it/repls/JovialPushyAquaticleech)

#### #4

[Merge sort](https://en.wikipedia.org/wiki/Merge_sort) runs in _O(n * log n)_. Implement this sort in JavaScript, or another language of your choice. In addition, understand why, for this algorithm, we multiplied the run times instead of adding them together to determine the overall Big O.

### More sites

- [Sorting Visualizations](https://www.youtube.com/watch?v=kPRA0W1kECg)
- [Big O Cheat Sheet](http://bigocheatsheet.com/)
- [Big O Notation by Rob Bell](https://rob-bell.net/2009/06/a-beginners-guide-to-big-o-notation/)
- [Logarithms](https://www.youtube.com/watch?v=AAW7WRFBKdw)
- [Factorials](http://www.purplemath.com/modules/factorial.htm)
- [Permuations & Combinations](https://www.youtube.com/watch?v=DJlOxOmmp9Y)
- [Combinatorics](https://www.youtube.com/watch?v=3Ry7gl-LSGA)
- [Amortized analysis](https://en.wikipedia.org/wiki/Amortized_analysis)
- [Sorting Visualizations via dance](https://www.youtube.com/watch?v=ywWBy6J5gz8)

And finally, see you if you can determine the Big O of the [Stable Marriage Problem](https://www.youtube.com/watch?v=Qcv1IqHWAzg), before you Google the answer.
