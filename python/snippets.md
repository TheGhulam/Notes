## Checking for uniqueness  
The next method checks if there are duplicate items in the given list. It uses a property set()that removes duplicate items from the list:

```python
def all_unique(lst):
    return len(lst) == len(set(lst))

x = [1,1,2,2,3,2,3,4,5,6]
y = [1,2,3,4,5]
all_unique(x) # False
all_unique(y) # True
```

## Anagram
This method can be used to check if two strings are anagrams. An Anagram is a word or phrase formed by rearranging the letters of another word or phrase, usually using all the original letters exactly once:
```python
from collections import Counter

def anagram(first, second):
    return Counter(first) == Counter(second)

anagram("abcd3", "3acdb") # True
```
```python
is_anagram = lambda x1, x2: sorted(x1) == sorted(x2)
```

## Memory
And this can be used to check the memory usage of an object:
```python
import sys 

variable = 30 
print(sys.getsizeof(variable)) # 24
```

## Size in bytes
The method returns the length of the string in bytes:
```python
def byte_size(string):
    return(len(string.encode('utf-8')))
    
byte_size('?') # 4
byte_size('Hello World') # 11    
```
## Factorial
```python
factorial = lambda n: n * factorial(n-1) if n > 1 else 1
```

## Separation
This method splits the list into smaller lists of the specified size:
```python
def chunk(list, size):
    return [list[i:i+size] for i in range(0,len(list), size)]

print(chunk([1, 2, 3, 4, 5, 6], 2))
```

## Binary Search
```python
l = [0, 1, 2, 3, 4, 5, 6, 7, 8, 9] # List
x = 9 # To-Find

bs = lambda l, x, lo, hi: -1 if lo > hi else \
(lo + hi)//2 if l[(lo+hi)//2] == x else \
bs(l, x, lo, (lo+hi)//2-1) if l[(lo+hi)//2] > x else \
bs(l, x, (lo+hi)//2+1, hi)

print(bs(l, x, 0, len(l)-1))
```

## Quicksort
```python
# Data 
unsorted = [5, 3, 15, 5]

q = lambda l:q([x for x in l[1:] if x <= l[0]]) + [l[0]] + q([x for x in l if x > l[0]]) if l else []
```

## Removing false values
So you remove the false values ( False, None, 0and «») from the list using filter():
```python
def compact(lst):
    return list(filter(bool, lst))
  
compact([0, 1, False, 2, '', 3, 'a', 's', 34]) # [ 1, 2, 3, 'a', 's', 34 ]
```

## Transpose
The following code can be used to transpose a 2D array:
```python
array = [['a', 'b'], ['c', 'd'], ['e', 'f']]
transposed = zip(*array)
print(transposed) # [('a', 'c', 'e'), ('b', 'd', 'f')]
```

## Count the vowels
This method counts the number of vowels (“a”, “e”, “i”, “o”, “u”) found in the string:
```python
import re

def count_vowels(str):
    return len(len(re.findall(r'[aeiou]', str, re.IGNORECASE)))

count_vowels('foobar') # 3
count_vowels('gym') # 0
```

## Levenshtein distance
```python
ls = lambda a, b: len(b) if not a else len(a) if not b else min(
	ls(a[1:], b[1:]) + (a[0] != b[0]),
	ls(a[1:], b) + 1,
	ls(a, b[1:]) + 1)
```

## Prime numbers (Sieve of Eratosthenes)
```python
from functools import reduce

# Data
n = 100

primes = reduce(lambda r, x: r - set(range(x**2, n, x)) if x in r else r, range(2, int(n**0.5) + 1), set(range(2, n)))
```

## Fibonacci
```python
from functools import reduce

# Data
n = 10

fibs = reduce(lambda x,_:x + [x[-2] + x[-1]], [0] * (n-2), [0, 1]) 
```
```python
# Data
n = 10

x=[0, 1]
fibs = x[0:2] + [x.append(x[-1] + x[-2]) or x[-1] for i in range(n-2)]
```

## ROT13 algo
```python
abc = "abcdefghijklmnopqrstuvwxyz"

rt13 = lambda x: "".join([abc[(abc.find(c) + 13) % 26] for c in x])
```

## Powerset of a set s
```python
from functools import reduce

ps = lambda s: reduce(lambda P, x: P + [subset | {x} for subset in P], s, [set()])
```

## Converting the first letter of a string to lowercase
Use to convert the first letter of your specified string to lowercase:
```python
def decapitalize(string):
    return string[:1].lower() + string[1:]
  
decapitalize('FooBar') # 'fooBar'
decapitalize('FooBar') # 'fooBar'
```

## Anti-aliasing
The following methods flatten out a potentially deep list using recursion:
```python
def spread(arg):
    ret = []
    for i in arg:
        if isinstance(i, list):
            ret.extend(i)
        else:
            ret.append(i)
    return ret

def deep_flatten(xs):
    flat_list = []
    [flat_list.extend(deep_flatten(x)) for x in xs] if isinstance(xs, list) else flat_list.append(xs)
    return flat_list

deep_flatten([1, [2], [[3], 4], 5]) # [1,2,3,4,5]
```

## Difference
The method finds the difference between the two iterations, keeping only the values that are in the first:
```python
def difference(a, b):
    set_a = set(a)
    set_b = set(b)
    comparison = set_a.difference(set_b)
    return list(comparison)

difference([1,2,3], [1,2,4]) # [3]
```

## The difference between lists
The following method returns the difference between the two lists after applying this function to each element of both lists:
```python
def difference_by(a, b, fn):
    b = set(map(fn, b))
    return [item for item in a if fn(item) not in b]


from math import floor
difference_by([2.1, 1.2], [2.3, 3.4],floor) # [1.2]
difference_by([{ 'x': 2 }, { 'x': 1 }], [{ 'x': 1 }], lambda v : v['x']) # [ { x: 2 } ]
```

## Chained function call
You can call multiple functions on one line:
```python
def add(a, b):
    return a + b

def subtract(a, b):
    return a - b

a, b = 4, 5
print((subtract if a > b else add)(a, b)) # 9   
```

## Finding Duplicates
This code checks to see if there are duplicate values ​​in the list using the fact that set()it only contains unique values:
```python
def has_duplicates(lst):
    return len(lst) != len(set(lst))
    
x = [1,2,3,4,5,5]
y = [1,2,3,4,5]
has_duplicates(x) # True
has_duplicates(y) # False
```

## Time spent
Use to calculate the time it takes for a specific code to run:
```python
import time

start_time = time.time()

a = 1
b = 2
c = a + b
print(c) #3

end_time = time.time()
total_time = end_time - start_time
print("Time: ", total_time)

# ('Time: ', 1.1205673217773438e-05)
```

## The element that appears most often
This method returns the most frequent item that appears in the list:
```python
def most_frequent(list):
    return max(set(list), key = list.count)

numbers = [1,2,1,2,3,2,1,4,2]
most_frequent(numbers)  
```

## Palindrome
The method checks if the given string is a palindrome:
```python
def palindrome(a):
    return a == a[::-1]

palindrome('mom') # True
```

## Shuffle
This code can be used to randomize the order of items in a list. Note that shuffleworks in place and returns None:
```python
from random import shuffle

foo = [1, 2, 3, 4]
shuffle(foo) 
print(foo) # [1, 4, 3, 2] , foo = [1, 2, 3, 4]
```

## Get default value for missing keys
The code shows how you can get the default value if the key you are looking for is not included in the dictionary:
```python

```
