---
title: "Lists"
teaching: 10
exercises: 10
questions:
- "How can I store multiple values?"
objectives:
- "Explain why programs need collections of values."
- "Write programs that create flat lists, index them, slice them, and modify them through assignment and method calls."
keypoints:
- "A list stores many values in a single structure."
- "Use an item's index to fetch it from a list."
- "Lists' values can be replaced by assigning to them."
- "Appending items to a list lengthens it."
- "Use `del` to remove items from a list entirely."
- "The empty list contains no values."
- "Lists may contain values of different types."
# - "Character strings can be indexed like lists."
# - "Character strings are immutable."
- "Indexing beyond the end of the collection is an error."
---
## A list stores many values in a single structure

*   Scenario: You have set up an Arduino to do temperature measurements
    in a storage room for rare books.
*   Doing calculations with a hundred variables called `temperature_001`, `temperature_002`, etc.,
    would be at least as slow as doing them by hand.
*   Use a *list* to store many values together.
    *   Contained within square brackets `[...]`.
    *   Values separated by commas `,`.
*   Use `len` to find out how many values are in a list.

~~~
temperatures = [17.3, 17.5, 17.7, 17.5, 17.6]
print('temperatures:', temperatures)
print('length:', len(temperatures))
~~~
{: .python}
~~~
temperatures: [17.3, 17.5, 17.7, 17.5, 17.6]
length: 5
~~~
{: .output}

For some purposes, a string can also be considered as a list of letters. For example, we can also use `len` on a string:

~~~
len('Here is a string')
~~~
{: .python}
~~~
16
~~~
{: .output}

## Use an item's index to fetch it from a list

Often in programming languages, individual items in an ordered set of data can be accessed directly using a numeric index or key value. This process is referred to as indexing.

In Python, lists are ordered sequences of items, and thus can be indexed in this way. Individual items in a list can be accessed by specifying the list name followed by a number in square brackets `[]`. 

List indexing in Python is zero-based: the first item in the list has index 0, the next has index 1, and so on. The index of the last item will be the length of the list minus one.

The individual items can be accessed by index:

~~~
print('zeroth item of temperatures:', temperatures[0])
print('fourth item of temperatures:', temperatures[4])
~~~
{: .python}
~~~
zeroth item of temperatures: 17.3
fourth item of temperatures: 17.6
~~~
{: .output}

## Lists' values can be replaced by assigning to them

*   Use an index expression on the left of assignment to replace a value.

~~~
temperatures[0] = 16.5
print('temperatures is now:', temperatures)
~~~
{: .python}
~~~
temperatures is now: [16.5, 17.5, 17.7, 17.5, 17.6]
~~~
{: .output}

## Appending items to a list lengthens it

*   Use `list_name.append` to add items to the end of a list.

~~~
print('temperatures is initially:', temperatures)
temperatures.append(17.9)
temperatures.append(18.2)
print('temperatures has become:', temperatures)
~~~
{: .python}
~~~
temperatures is initially: [16.5, 17.5, 17.7, 17.5, 17.6]
temperatures has become: [16.5, 17.5, 17.7, 17.5, 17.6, 17.9, 18.2]
~~~
{: .output}

*   `append` is a *method* of lists.
    *   Like a function, but tied to a particular object.
*   Use `object_name.method_name` to call methods.
    *   Deliberately resembles the way we refer to things in a library.
*   We will meet other methods of lists as we go along.
    *   Use `help(list)` for a preview.

## Use `del` to remove items from a list entirely

*   `del list_name[index]` removes an item from a list and shortens the list.
*   Not a function or a method, but a statement in the language.

~~~
primes = [2, 3, 5, 7, 11]
print('primes before removing last item:', primes)
del primes[4]
print('primes after removing last item:', primes)
~~~
{: .python}
~~~
primes before removing last item: [2, 3, 5, 7, 11]
primes after removing last item: [2, 3, 5, 7]
~~~
{: .output}

## The empty list contains no values

*   Use `[]` on its own to represent a list that doesn't contain any values.
    *   "The zero of lists."
*   Helpful as a starting point for collecting values
    (which we will see in the [next episode]({{page.root}}/12-for-loops/)).

## Lists may contain values of different types

*   A single list may contain numbers, strings, and anything else.

~~~
goals = [1, 'Create lists.', 2, 'Extract items from lists.', 3, 'Modify lists.']
~~~
{: .python}

<!-- ## Character strings can be indexed like lists

*   Get single characters from a character string using indexes in square brackets.

~~~
element = 'carbon'
print('zeroth character:', element[0])
print('third character:', element[3])
~~~
{: .python}
~~~
zeroth character: c
third character: b
~~~
{: .output}

## Character strings are immutable

*   Cannot change the characters in a string after it has been created.
    *   *Immutable*: cannot be changed after creation.
    *   In contrast, lists are *mutable*: they can be modified in place.
*   Python considers the string to be a single value with parts,
    not a collection of values.

~~~
element[0] = 'C'
~~~
{: .python}
~~~
TypeError: 'str' object does not support item assignment
~~~
{: .error}

*   Lists and character strings are both *collections*. -->

## Indexing beyond the end of the collection is an error

*   Python reports an `IndexError` if we attempt to access a value that doesn't exist.
    *   This is a kind of runtime error.
    *   Cannot be detected as the code is parsed
        because the index might be calculated based on data.

~~~
elements = ['Hydrogen', 'Helium', 'Lithium', 'Beryllium']
print('99th element of elements are:', elements[99])
~~~
{: .python}
~~~
IndexError: list index out of range
~~~
{: .output}

> ## Fill in the Blanks
>
> Fill in the blanks so that the program below produces the output shown.
>
> ~~~
> values = ____
> values.____(1)
> values.____(3)
> values.____(5)
> print('first time:', values)
> values = values[____]
> print('second time:', values)
> ~~~
> {: .python}
>
> ~~~
> first time: [1, 3, 5]
> second time: [3, 5]
> ~~~
> {: .output}
> > ## Solution
> > ~~~
> > values = []
> > values.append(1)
> > values.append(3)
> > values.append(5)
> > print('first time:', values)
> > values = values[1:3]
> > print('second time:', values)
> > ~~~
> > {: .python}
> > ~~~
> > first time [1, 3, 5]
> > second time [3, 5]
> > ~~~
> > {: .output}
> {: .solution}
{: .challenge}

> ## How Large is a Slice?
>
> If 'low' and 'high' are both non-negative integers,
> how long is the list `values[low:high]`?
> > ## Solution
> > The list's length would be equal to `high - low`.  
> {: .solution}
{: .challenge}

<!-- > ## From Strings to Lists and Back
>
> Given this:
>
> ~~~
> print('string to list:', list('tin'))
> print('list to string:', ''.join(['g', 'o', 'l', 'd']))
> ~~~
> {: .python}
> 
> ~~~
> ['t', 'i', 'n']
> 'gold'
> ~~~
> {: .output}
> 
> 1.  Explain in simple terms what `list('some string')` does.
> 2.  What does `'-'.join(['x', 'y'])` generate?  
> 
> > ## Solution
> >  1.  It creates a list of the `some string`s characters as elements. 
> >  2.  It creates a string composed of `x` and `y`, separated by a hyphen character(`-`).  
> {: .solution}
{: .challenge} -->

> ## Working With the End
>
> What does the following program print?
>
> ~~~
> elements = ['hydrogen', 'helium', 'lithium', 'berylium']
> print(elements[-1])
> ~~~
> {: .python}
>
> 1.  How does Python interpret a negative index?
> 2.  If a list or string has N elements,
>     what is the most negative index that can safely be used with it,
>     and what location does that index represent?
> 3.  If `elements` is a list, what does `del elements[-1]` do?
> 4.  How can you display all elements but the last one without changing `elements`?
>     (Hint: you will need to combine slicing and negative indexing.)  
> 
> > ## Solution
> > ~~~
> > berylium
> > ~~~
> > {: .output}
> > 1.  A negative index begins at the final element. 
> > 2.  `-(N)` corresponds to the first index, which is the [0] index.
> > 3.  It removes the final element of the list. 
> > 4.  You could do the following: `print(elements[0:-1])`
> {: .solution}
{: .challenge}

> ## Stepping Through a List
>
> What does the following program print?
>
> ~~~
> elements = ['hydrogen', 'helium', 'lithium', 'berylium']
> print(element[::2])
> print(element[::-1])
> ~~~
> {: .python}
>
> 1.  If we write a slice as `low:high:stride`, what does `stride` do?
> 2.  What expression would select all of the even-numbered items from a collection?  
> 
> > ## Solution
> > ~~~
> > ['hydrogen', 'lithium']
> > ['berylium', 'lithium', 'helium', 'hydrogen']
> > ~~~
> > {: .output}
> > 1.  `stride` indicates both the number of steps, and from which end: positive starts from first element, negative from the last element. 
> > 2.  `element[1::2]`
> {: .solution}
{: .challenge}

> ## Slice Bounds
>
> What does the following program print?
>
> ~~~
> elements = ['hydrogen', 'helium', 'lithium', 'berylium']
> print(elements[0:20])
> print(elements[-1:3])
> ~~~
> {: .python}
> > ## Solution
> > 
> > ~~~
> > ['hydrogen', 'helium', 'lithium', 'berylium']
> > []
> > ~~~
> > {: .output}
> > There is no 20th index, so the entire string is captured.  
> > There is no element after the -1 index.  
> {: .solution}
{: .challenge}

> ## Sort and Sorted
>
> What do these two programs print?
> In simple terms, explain the difference between `sorted(letters)` and `letters.sort()`.
>
> ~~~
> # Program A
> numbers = ['one', 'two', 'three', 'four']
> result = sorted(numbers)
> print('numbers is', numbers, 'and result is', result)
> ~~~
> {: .python}
>
> ~~~
> # Program B
> numbers = ['one', 'two', 'three', 'four']
> result = numbers.sort()
> print('numbers is', numbers, 'and result is', result)
> ~~~
> {: .python}
>
> > ## Solution
> > Program A:
> > ~~~
> > numbers is ['one', 'two', 'three', 'four'] and result is ['four', 'one', 'three', 'two']
> > ~~~
> > {: .output}
> > Program B:
> > ~~~
> > numbers is ['four', 'one', 'three', 'two'] and result is None
> > ~~~
> > {: .output}
> > `sorted(numbers)` returns a sorted copy of the list without changing the original list,
> > while `numbers.sort()` sorts the original list but does not return anything, i.e. returns `None`.
> {: .solution}
{: .challenge}

> ## Copying (or Not)
>
> What do these two programs print?
> In simple terms, explain the difference between `new = old` and `new = old[:]`.
>
> ~~~
> # Program A
> old = [1, 2, 3, 4]
> new = old      # simple assignment
> new[0] = 5
> print('new is', new, 'and old is', old)
> ~~~
> {: .python}
>
> ~~~
> # Program B
> old = [1, 2, 3, 4]
> new = old[:]   # assigning a slice
> new[0] = 5
> print('new is', new, 'and old is', old)
> ~~~
> {: .python}
>
> > ## Solution
> > Program A:
> > ~~~
> > new is [5, 2, 3, 4] and old is [5, 2, 3, 4]
> > ~~~
> > {: .output}
> > Program B:
> > ~~~
> > new is [5, 2, 3, 4] and old is [1, 2, 3, 4]
> > ~~~
> > {: .output}
> > 
> > `new = old` is assigning `old` to `new`. This means that the two variables both point to the same value. Thus, changing the contents of either variable will affect the other.
> > In contrast, `new = old[:]` is a **slice assignment**, which will only return a copy of `old`.
> {: .solution}
{: .challenge}
