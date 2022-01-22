
# Sorting dicts 

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
