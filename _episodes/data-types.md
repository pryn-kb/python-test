---
title: "Data Types"
teaching: 0
exercises: 0
questions:
- "FIXME"
objectives:
- "Learning objective (FIXME)"
keypoints:
- "FIXME"
---
## Data Types

There are four essential kinds of Python data with different powers and capabilities:

*   Strings (Text)
*   Integers (Whole Numbers)
*   Floats (Decimal Numbers)
*   Booleans (True/False)

Take a look at the variables `filepath_of_text` and `number_of_desired_word` in the word count code below.

What differences do you notice between these two variables and their corresponding values?

~~~
'Here is a some text'
42
~~~
{: .python}

You might be wondering…

Why is 'Here is some text' surrounded by quotation marks while 42 is not?\
Because these are two different “types” of Python data.

<table class="colwidths-auto table" style="width:50%; border:1px solid black">
<thead>
<tr class="row-odd"><th class="head"><p>Data Type</p></th>
<th class="head"><p>Explanation</p></th>
<th class="head"><p>Example</p></th>
</tr>
</thead>
<tbody>
<tr class="row-even"><td><p>String</p></td>
<td><p>Text</p></td>
<td><div class="highlight-default notranslate"><div class="highlight"><pre><span></span> <span class="s2">&quot;Beyonce-Lemonade.txt&quot;</span><span class="p">,</span>
 <span class="s2">&quot;lemonade&quot;</span>
</pre></div>
</div>
</td>
</tr>
<tr class="row-odd"><td><p>Integer</p></td>
<td><p>Whole Numbers</p></td>
<td><div class="highlight-default notranslate"><div class="highlight"><pre><span></span><span class="mi">40</span>
</pre></div>
</div>
</td>
</tr>
<tr class="row-even"><td><p>Float</p></td>
<td><p>Decimal Numbers</p></td>
<td><div class="highlight-default notranslate"><div class="highlight"><pre><span></span><span class="mf">40.2</span>
</pre></div>
</div>
</td>
</tr>
<tr class="row-odd"><td><p>Boolean</p></td>
<td><p>True/False</p></td>
<td><div class="highlight-default notranslate"><div class="highlight"><pre><span></span><span class="kc">False</span>
</pre></div>
</div>
</td>
</tr>
</tbody>
</table>

## Check Data Types

You can check the data type of any value by using the function `type()`.

~~~
type('Here is some text')
~~~
{: .python}
~~~
str
~~~
{: .output}

~~~
type(42)
~~~
{: .python}
~~~
int
~~~
{: .output}

## Strings

A _string_ is a Python data type that is treated like text, even if it contains a number. Strings are always enclosed by either single quotation marks `'this is a string'` or double quotation marks `"this is a string"`.

~~~
'this is a string'
~~~
{: .python}

~~~
"this is also a string, even though it contains a number like 42"
~~~
{: .python}

~~~
this is not a string
~~~
{: .python}

It doesn’t matter whether you use single or double quotation marks with strings, as long as you use the same kind on either side of the string.

If you need to include a single or double quotation mark _inside_ of a string, then you need to either:

*   use the opposite kind of quotation mark inside the string
*   or “escape” the quotation mark by using a backslash `\` before it
    

**Escape characters**

A backslash character `\` tells Python to treat the next character like a normal character and to ignore any special meaning

~~~
"She exclaimed, 'This is a quotation inside a string!''"
~~~
{: .python}

~~~
"She exclaimed, \"This is also a quotation inside a string!\""
~~~
{: .python}

## String Methods

Each data type has different properties and capabilities. So there are special things that only strings can do, and there are special ways of interacting with strings.

For example, you can _index_ and _slice_ strings, you can _add_ strings together, and you can transform strings to uppercase or lowercase.\
Here are a few examples using a snippet from Beyoncé’s song “Hold Up.”

lemonade\_snippet \= "Hold up, they don't love you like I love you"

### Index

lemonade\_snippet\[0\]

'H'

### Slice[¶](#slice "Permalink to this headline")

lemonade\_snippet\[0:20\]

"Hold up, they don't "

### Add[¶](#add "Permalink to this headline")

lemonade\_snippet + " // Slow down, they don't love you like I love you"

"Hold up, they don't love you like I love you // Slow down, they don't love you like I love you"

### Make uppercase[¶](#make-uppercase "Permalink to this headline")

lemonade\_snippet.upper()

"HOLD UP, THEY DON'T LOVE YOU LIKE I LOVE YOU"

## f-Strings[¶](#f-strings "Permalink to this headline")

A special kind of string that we’re going to use in this class is called an _f-string_. An f-string, short for formatted string literal, allows you to insert a variable directly into a string. [f-strings were introduced with Python version 3.6](https://docs.python.org/3/whatsnew/3.6.html#new-features).

An f-string must begin with an `f` outside the quotation marks. Then, inside the quotation marks, the inserted variable must be placed within curly brackets `{}`.

What does \\n mean?

\\n = new line

print(f"Beyonce burst out of the building and sang: \\n\\n'{lemonade\_snippet}'")

Beyonce burst out of the building and sang: 

'Hold up, they don't love you like I love you'

## Integers & Floats[¶](#integers-floats "Permalink to this headline")
-------------------------------------------------------------------

An _integer_ and a _float_ (short for _floating point number_) are two Python data types for representing numbers. Integers represent whole numbers. Floats represent numbers with decimal points. They do not need to be placed in quotation marks.

type(40)

int

type(40.5)

float

type(40.555555)

float

You can do a large range of mathematical calculations and operations with integers and floats. The table below is taken from Python’s documentation about [Numeric Types](https://docs.python.org/3/library/stdtypes.html#numeric-types-int-float-complex).

<table class="colwidths-auto table">
<thead>
<tr class="row-odd"><th class="head"><p>Operation</p></th>
<th class="head"><p>Explanation</p></th>
</tr>
</thead>
<tbody>
<tr class="row-even"><td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> + <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
<td><p>sum of <code class="docutils literal notranslate"><span class="pre">x</span></code> and <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
</tr>
<tr class="row-odd"><td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> - <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
<td><p>difference of <code class="docutils literal notranslate"><span class="pre">x</span></code> and <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
</tr>
<tr class="row-even"><td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> * <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
<td><p>product of <code class="docutils literal notranslate"><span class="pre">x</span></code> and <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
</tr>
<tr class="row-odd"><td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> / <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
<td><p>quotient of <code class="docutils literal notranslate"><span class="pre">x</span></code> and <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
</tr>
<tr class="row-even"><td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> // <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
<td><p>floored quotient of <code class="docutils literal notranslate"><span class="pre">x</span></code> and</p></td>
</tr>
<tr class="row-even"><td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> % <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
<td><p>remainder of <code class="docutils literal notranslate"><span class="pre">x</span></code> / <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
</tr>
<tr class="row-odd"><td><p>-<code class="docutils literal notranslate"><span class="pre">x</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> negated</p></td>
</tr>
<tr class="row-even"><td><p>+<code class="docutils literal notranslate"><span class="pre">x</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> unchanged</p></td>
</tr>
<tr class="row-odd"><td><p><code class="docutils literal notranslate"><span class="pre">abs(x)</span></code></p></td>
<td><p>absolute value or magnitude of <code class="docutils literal notranslate"><span class="pre">x</span></code></p></td>
</tr>
<tr class="row-even"><td><p><code class="docutils literal notranslate"><span class="pre">int(x)</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> converted to integer</p></td>
</tr>
<tr class="row-odd"><td><p><code class="docutils literal notranslate"><span class="pre">float(x)</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> converted to floating point</p></td>
</tr>
<tr class="row-even"><td><p><code class="docutils literal notranslate"><span class="pre">pow(x,</span> <span class="pre">y)</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> to the power <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
</tr>
<tr class="row-odd"><td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> ** <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
<td><p><code class="docutils literal notranslate"><span class="pre">x</span></code> to the power <code class="docutils literal notranslate"><span class="pre">y</span></code></p></td>
</tr>
</tbody>
</table>

### Multiplication[¶](#multiplication "Permalink to this headline")

variable1 \= 4
variable2 \= 2
variable1 \* variable2

8

### Exponents[¶](#exponents "Permalink to this headline")

variable1 \*\* variable2

16

### Remainder[¶](#remainder "Permalink to this headline")

72 % 10

2

## Booleans

Booleans are “truth” values. They report on whether things in your Python universe are `True` or `False`. There are the only two options for a boolean: `True` or `False`.

For example, let’s assign the variable `beyonce` the value `"Grammy award-winner"`

beyonce \= "Grammy award-winner"

Python Review

Remember the difference between a single equals sign `=` and a double equals sign `==`?

*   A single equals sign \`=\` is used for variable assignment
*   A double equals sign \`==\` is used as the equals operator

We can “test” whether the variable `beyonce` equals `"Grammy award-winner"` by using the equals operator `==`. This will return a boolean.

beyonce \== "Grammy award-winner"

True

type(beyonce \== "Grammy award-winner")

bool

If we evaluate whether `beyonce` instead equals `"Oscar award-winner"`, we will get the boolean answer.

beyonce \== "Oscar award-winner"

False

## TypeError

If you don’t use the right data “type” for a particular method or function, you will get a `TypeError.`

Let’s look at what happens if we change the data type `number_of_desired_words` to a string `"40"` instead of an integer.

import re
from collections import Counter

def split\_into\_words(any\_chunk\_of\_text):
    lowercase\_text \= any\_chunk\_of\_text.lower()
    split\_words \= re.split("\\W+", lowercase\_text)
    return split\_words

filepath\_of\_text \= "../texts/music/Beyonce-Lemonade.txt"
number\_of\_desired\_words \= "40"
stopwords \= \['i', 'me', 'my', 'myself', 'we', 'our', 'ours', 'ourselves', 'you', 'your', 'yours',
 'yourself', 'yourselves', 'he', 'him', 'his', 'himself', 'she', 'her', 'hers',
 'herself', 'it', 'its', 'itself', 'they', 'them', 'their', 'theirs', 'themselves',
 'what', 'which', 'who', 'whom', 'this', 'that', 'these', 'those', 'am', 'is', 'are',
 'was', 'were', 'be', 'been', 'being', 'have', 'has', 'had', 'having', 'do', 'does',
 'did', 'doing', 'a', 'an', 'the', 'and', 'but', 'if', 'or', 'because', 'as', 'until',
 'while', 'of', 'at', 'by', 'for', 'with', 'about', 'against', 'between', 'into',
 'through', 'during', 'before', 'after', 'above', 'below', 'to', 'from', 'up', 'down',
 'in', 'out', 'on', 'off', 'over', 'under', 'again', 'further', 'then', 'once', 'here',
 'there', 'when', 'where', 'why', 'how', 'all', 'any', 'both', 'each', 'few', 'more',
 'most', 'other', 'some', 'such', 'no', 'nor', 'not', 'only', 'own', 'same', 'so',
 'than', 'too', 'very', 's', 't', 'can', 'will', 'just', 'don', 'should', 'now', 've', 'll', 'amp'\]

full\_text \= open(filepath\_of\_text, encoding\="utf-8").read()

all\_the\_words \= split\_into\_words(full\_text)
meaningful\_words \= \[word for word in all\_the\_words if word not in stopwords\]
meaningful\_words\_tally \= Counter(meaningful\_words)
most\_frequent\_meaningful\_words \= meaningful\_words\_tally.most\_common(number\_of\_desired\_words)

most\_frequent\_meaningful\_words

\---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython\-input\-7\-a142b58e454a\> in <module\>
     29 meaningful\_words \= \[word for word in all\_the\_words if word not in stopwords\]
     30 meaningful\_words\_tally \= Counter(meaningful\_words)
\---> 31 most\_frequent\_meaningful\_words \= meaningful\_words\_tally.most\_common(number\_of\_desired\_words)
     32 
     33 most\_frequent\_meaningful\_words

~/opt/anaconda3/lib/python3.7/collections/\_\_init\_\_.py in most\_common(self, n)
    584         if n is None:
    585             return sorted(self.items(), key\=\_itemgetter(1), reverse\=True)
\--> 586         return \_heapq.nlargest(n, self.items(), key\=\_itemgetter(1))
    587 
    588     def elements(self):

~/opt/anaconda3/lib/python3.7/heapq.py in nlargest(n, iterable, key)
    544         pass
    545     else:
\--> 546         if n \>= size:
    547             return sorted(iterable, key\=key, reverse\=True)\[:n\]
    548 

TypeError: '>=' not supported between instances of 'str' and 'int'
