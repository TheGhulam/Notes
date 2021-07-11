[explanation](http://psung.blogspot.com/2007/12/for-else-in-python.html)

```python
for x in xrange(10):
    for y in xrange(10):
        print x*y
        if x*y > 50:
            break
    else:
        continue  # only executed if the inner loop did NOT break
    break  # only executed if the inner loop DID break
```

The same works for deeper loops:
```python
for x in xrange(10):
    for y in xrange(10):
        for z in xrange(10):
            print x,y,z
            if x*y*z == 30:
                break
        else:
            continue
        break
    else:
        continue
    break
```
