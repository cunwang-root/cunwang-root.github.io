---
layout: post
title:  "my python cookbook"
date:   2018-01-31
categories: [LANGUAGES]
mathjax: true
---
## 0. useful points

* list slicing does not produce index out of bound error
    Slicing is used to create a new list. If the indices don't fall within the
    range of the number of elements in the list, we can return an empty list.

## 1. argparse

```python
import argparse
parser = argparse.ArgumentParser()
description keyword tell users the main purpose of the program
parser = argparse.ArgumentParser(description="get the maximum of a list")
```

1.1 add postional arguments

```python
parser.add_argument("square", help="display a square of a given number",
                    type=int)
```

argparse treats the options we give it as strings, unless we tell it
otherwise.

1.2 add optional arguments

```python
parser.add_argument("--verbose", help="increase output verbosity",
                    action="store_true")

provide short options
parser.add_argument("-v", "--verbose", help="increase output verbosity",
                    action="store_true")

restrict the values an option can accept
parser.add_argument("-v", "--verbosity", type=int, choices=[0, 1, 2],
                    help="increase output verbosity")

set the default value
Remember that by default, if an optional argument isn’t specified, it gets
the None value, and that cannot be compared to an int value
```

1.3 add subcommands

1.4 
```python
args = parser.parse_args()
```




