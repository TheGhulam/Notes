#


## 1. Sort Sequences of Data

### Data
```python
grades = [{'name':'Jennifer', 'final':95}, {'name': 'David', 'final': 92}, {'name': 'Aaron', 'final': 98}]
```

### Sort by name
```python
sorted(grades, key=lambda x:x['name'])

[{'name': 'Aaron', 'final': 98}, {'name': 'David', 'final': 92}, {'name': 'Jennifer', 'final': 95}]
```

### Sort by final grades, descending
```python
sorted(grades, key=lambda x: x['final'], reverse=True)
[{'name': 'Aaron', 'final': 98}, {'name': 'Jennifer', 'final': 95}, {'name': 'David', 'final': 92}]
```

## 2. Find the Minimal and Maximal Values

### Create a sequence of data
```python
grades = [{'name':'Jennifer', 'final':95}, {'name': 'David', 'final': 92}, {'name': 'Aaron', 'final': 98}]
```

### Get the highest final score
```python
max(grades, key=lambda x: x['final'])
{'name': 'Aaron', 'final': 98}
```

### Get the lowest final score
```python
min(grades, key=lambda x: x['final'])
{'name': 'David', 'final': 92}
```

## 3. Serve as a factory function
```python
from collections import defaultdict

# Create a defaultdict
known_points = {'first': (2, 3), 'second': (4, 2)}
points = defaultdict(lambda: (0, 0), known_points)

# Retrive some points
points['first']
(2, 3)
points['second']
(4, 2)
points['three']
(0, 0)
```
