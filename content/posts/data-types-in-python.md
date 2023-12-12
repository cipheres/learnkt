---
title: 'Data Types in Python'
date: 2023-12-12T20:31:07+05:30
# weight: 1
# aliases: ["/first"]
tags: ["python", "variables", "data type", "reference type", "value type"]
author: "Me"
# author: ["Me", "You"] # multiple authors
showToc: true
TocOpen: false
draft: false
hidemeta: false
comments: false
# description: "Desc Text."
# canonicalURL: "https://canonical.url/to/page"
disableHLJS: false # to enable highlightjs
disableShare: false
hideSummary: false
searchHidden: true
ShowReadingTime: true
ShowBreadCrumbs: true
ShowPostNavLinks: true
ShowWordCount: true
ShowRssButtonInSectionTermList: true
UseHugoToc: true
# cover:
#     image: "<image path/url>" # image path/url
#     alt: "<alt text>" # alt text
#     caption: "<text>" # display caption under cover
#     relative: false # when using page bundles set this to true
#     hidden: true # only hide on current single page
# editPost:
#     URL: "https://github.com/<path_to_repo>/content"
#     Text: "Suggest Changes" # edit text
#     appendFilePath: true # to append file path to Edit link
---

In Python, equal sign (=) is used to assign a value to variable. 

```python
greeting = "Hello, World!"
```

A variable can be assigned different data types. Generally “Data types” are classified as either “value types” or “reference types”, where reference types are always implicitly accessed via references, whereas value type variables directly contain the values themselves. Languages like C/C++ use value types, whereas python uses “reference type” data type.

## What is “refrence type” & “value type” data type means?

Variables of reference types store references to their data (objects), while variables of value types directly contain their data. With reference types, two variables can reference the same object; therefore, operations on one variable can affect the object referenced by the other variable. They are like labels to container. A container can have multiple labels. With value types, each variable has its own copy of the data, and it is not possible for operations on one variable to affect the other(expect using pointers or something similar). This holds the value itself. It is the container. Two variables can't share them. Changing one variable will not lead to change in other variable.


That is why, a variable in Python is a name that refers to a value stored in the computer memory, like a label on a box.

To prove this point let do a expirement. Let's try to share a variable in python & C++. 

**Python**
```python
class Foo:
    x = 1

foo = Foo()
bar = foo
bar.x = 10

print(foo.x)
```
**Output**
```bash
10
```

![Python Memory](/python-memory.jpg)

On `line 6` we are only changing `bar.x` but when we print output `foo.x` also changed. Actually they both were referencing the same variable hence the same output. Now let's check what happens in C++.

**C++**
```C++
#include <iostream>

class Foo {
    public:
        int x;
};

int main() {
    // Creating foo object
    Foo foo = Foo();
    // Setting x of foo to 0
    foo.x = 0;
    // Creating bar, assigning bar to foo
    Foo bar = foo;
    // Setting x of bar to 10
    bar.x = 10;
    // priting value of x of foo
    std::cout << foo.x;

    return 0;
}
```

**Output**
```
0
```
As we can clearly see that output C++ is very different from Python. In C++ only the value of `bar.x` changed & not value of `foo.x`.

## Mutability
An immutable object (unchangeable object) is an object whose state cannot be modified after it is created. This is in contrast to a mutable object (changeable object), which can be modified after it is created.

**Immutable Data Types**
- Numbers (Integer, Rational, Float, Decimal, Complex & Booleans)
- Strings
- Tuples
- Frozen Sets

**Mutable Data Types**
- Lists
- Dictionary
- Sets
- User-Defined Class



