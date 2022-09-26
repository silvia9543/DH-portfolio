---
layout: page
title: Variables, Strings, and Numbers
description: This notebook has code about variables, strings, numbers, and lists
---

## Whitespace


```python
print("\ttab")
```

    	tab



```python
str_rspace = "string            "
print(str_rspace)
```

    string            



```python
example = str_rspace + ","
print(example)
```

    string            ,



```python
example_2 = str_rspace.rstrip() + ","
print(example_2)
```

    string,


## Numbers



```python
# integers
238 + 4834
```




    5072




```python
num = 50
```


```python
num
```




    50




```python
type(num)
```




    int




```python
30/10
```




    3.0




```python
f = 30/7
```


```python
f
```




    4.285714285714286




```python
type(f)
```




    float




```python
3 ** 3
```




    27



## Lists


```python
subjects= []
```


```python
subjects = ['classics', 'history', 'philosophy']
message = f"My most difficult subject is {subjects[1].title()}."
print(message)
```

    My most difficult subject is History.



```python
# how to modify a list
subjects[1] = 'sociology'

# append
subjects.append('history')
```


```python
print(subjects)
```

    ['classics', 'sociology', 'philosophy', 'history', 'history']



```python
subjects.insert(2, 'latin')
```


```python
print(subjects)
```

    ['classics', 'sociology', 'latin', 'philosophy', 'history', 'history']



```python
#delete item 
del subjects[-1]
print(subjects)
```

    ['classics', 'sociology', 'latin', 'philosophy', 'history']



```python
# pop method
popped_subject = subjects.pop(0)
print(popped_subject)
```

    classics



```python

```
