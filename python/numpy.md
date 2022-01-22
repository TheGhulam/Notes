
## Numpy Arrays

### Initialization
```python
n = np.array([
	[1, 2, 3],
	[4, 5, 6],
])

np.zeros((2,4))
np.ones((4, 2, 2), dtype='int32')
np.full((2,2), 99)
np.full_like(a, 4)
np.random.rand(4, 2)
np.random.random_sample(a.shape)
np.random.randint(<start_num>, <end_num>, size=(3,3))
np.identity(5)
cost = np.squeeze(cost)      # To make sure your cost's shape is what we expect (e.g. this turns [[17]] into 17).
 

arr = np.array([[1, 2, 3]])
r1 = np.repeat(arr, 2, axis=0)

n = np.array([1, 2, 3], dtype=np.float)

# Indexing and Slicing arrays
n[1] # np.array([1, 2, 3])
n[1][2] # 6 
n[1, 2] # 6
n[0, 1:6:2]

# Operations
n.mean(axis=0)
n.std(axis=0)
n.var()
n.dtype()
n.shape()
n.ndim()
n.size()
n.sum(axis=0)
n.itemsize()


# Easier way to get slices
a =  np.array([0, .5, 1, 1.5, 2])
a[0], a[2], a[-1] # (0.0, 1.0, 2.0)
a[[0, 2, -1]] # array([0.0, 1.0, 2.0])
a[[True, False, True, False, True]] # array([0.0, 1.0, 2.0])

```

## Mathematical Operations
```python
# Broadcasting and Vectorized operations
a = np.arange(4)

a + 10 # Broadcasted to each individual elements
# New array returned
# Similar to [ i + 10 for i in a]

np.cos(a)
```
### Linear Algebra
```python
A = np.array([
	[1, 2, 3],
	[4, 5, 6],
	[7, 8, 9],
])

B = np.array([
	[6, 5],
	[4, 3],
	[2, 1],
])

np.matmul(A, B)

A.dot(B)
array([[20, 14], 
	   [56, 41], 
	   [92, 68]])

A @ B
array([[20, 14], 
	   [56, 41], 
	   [92, 68]])

B.T (Trancpose)


# Find the determinant
c = np.identity(5)
np.linalg.det(c) # 1
```

### Normalizing
```python
# Compute x_norm as the norm 2 of x. Use np.linalg.norm(..., ord = 2, axis = ..., keepdims = True)
x_norm = np.linalg.norm(x, ord=2, axis=1, keepdims=True)
    
# Divide x by its norm.
x = x / x_norm
```

### Stastistics
```python
a = np.ones((2,3))

np.min(a)
np.max(a, axis=1)
np.sum(a, axis=0)
```
### Iterating
```python
# 1D array
for x in my_array :
    ...
	
# 2D array
for x in np.nditer(my_array) :
    ...
```
## Copying Arrays
```python
# WRONG
b = a

# CORRECT
b = a.copy()

# .copy() creates a new array instead of creating a new pointer to the original array
```

## Reorganizing Arrays
```python
before = np.array([[1,2,3,4], [5,6,7,8]])
after = before.reshape((2,2,2))

a = np.array([1, 2, 3, 4, 5, 6])
b = a.reshape((2, -1)) 
# -1: NumPy figures out automatically

# Vertical stack
v1 = np.array([1,2,3,4])
v2 = np.array([5,6,7,8])

np.vstack([v1, v2])

# Horizontal stack
v1 = np.array([1,2,3,4])
v2 = np.array([5,6,7,8])

np.hstack([v1, v2])
```

## Boolean operations
```python
a >= 2
array([False, False, True, True])

a[a >= 2]
array([2, 3])

np.any(a > 2, axis=0)
np.all(a > 2, axis=0)
```
## Miscellaneous
```python
# Load Data from file
filedata = np.genfromtxt('data.txt', delimiter=',')

filedat = filedata.astype('int32')

# Indexing with a list in numpy
a = np.array([1,2,4,5])
a[[2,3]]

# List indexing helps in slicing a diagonal
a[[0,1,2,3], [1,2,3,4]]
```

