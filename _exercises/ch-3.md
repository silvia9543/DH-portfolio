---
layout: page
title: Week 4, Exercises Ch. 3
description: Select exercises from Python Crash Course
---

### 3-1: Names




```python
names = ['john', 'sally', 'rachel', 'leo']
for name in names:
    print(name)
```

    john
    sally
    rachel
    leo


### 3-2: Greetings


```python
for name in names:
    print(f"hey {name}, I hope you're doing well")
```

    hey john, I hope you're doing well
    hey sally, I hope you're doing well
    hey rachel, I hope you're doing well
    hey leo, I hope you're doing well


### 3-3: Your Own List


```python
transports = ['bike', 'train', 'plane', 'private jet', 'hangglider']
for transport in transports:
    print(f"I would like to own a {transport}.")
```

    I would like to own a bike.
    I would like to own a train.
    I would like to own a plane.
    I would like to own a private jet.
    I would like to own a hangglider.


### 3-4: Guest List



```python
guests = ['Whitney Houston', 'Michael Jackson', 'Trevor Noah', 'Hasan Minhaj']
for guest in guests:
    print(f"Dear {guest}, I would like to invite you to dinner today at 7pm.")
```

    Dear Whitney Houston, I would like to invite you to dinner today at 7pm.
    Dear Michael Jackson, I would like to invite you to dinner today at 7pm.
    Dear Trevor Noah, I would like to invite you to dinner today at 7pm.
    Dear Hasan Minhaj, I would like to invite you to dinner today at 7pm.


### 3-5: Changing Guest List


```python
guests = ['Whitney Houston', 'Michael Jackson', 'Trevor Noah', 'Hasan Minhaj']
for guest in guests:
    print(f"Dear {guest}, I would like to invite you to dinner today at 7pm.")
print(guests[0])
guests[0] = 'Matt Bomer'
for guest in guests:
    print(f"Dear {guest}, I would like to invite you to dinner today at 7pm.")

```

    Whitney Houston
    Dear Matt Bomer, I would like to invite you to dinner today at 7pm.
    Dear Michael Jackson, I would like to invite you to dinner today at 7pm.
    Dear Trevor Noah, I would like to invite you to dinner today at 7pm.
    Dear Hasan Minhaj, I would like to invite you to dinner today at 7pm.


### 3-6: Shrinking Guest List


```python
guests = ['Whitney Houston', 'Michael Jackson', 'Trevor Noah', 'Hasan Minhaj']
for guest in guests:
    print(f"Dear {guest}, I would like to invite you to dinner today at 7pm.")
print(guests[0])
guests[0] = 'Matt Bomer'
for guest in guests:
    print(f"Dear {guest}, I would like to invite you to dinner today at 7pm.")
print("I can only invite two people to dinner")
while len(guests) != 2:
    bye_guest = guests.pop()
    print(f"I'm sorry {bye_guest}, I can't invite you to dinner")
for guest in guests:
    print(f"Hey {guest}, you're still invited to dinner.")
while guests:
    del guests[0]
print(guests)
```

    Dear Whitney Houston, I would like to invite you to dinner today at 7pm.
    Dear Michael Jackson, I would like to invite you to dinner today at 7pm.
    Dear Trevor Noah, I would like to invite you to dinner today at 7pm.
    Dear Hasan Minhaj, I would like to invite you to dinner today at 7pm.
    Whitney Houston
    Dear Matt Bomer, I would like to invite you to dinner today at 7pm.
    Dear Michael Jackson, I would like to invite you to dinner today at 7pm.
    Dear Trevor Noah, I would like to invite you to dinner today at 7pm.
    Dear Hasan Minhaj, I would like to invite you to dinner today at 7pm.
    I can only invite two people to dinner
    I'm sorry Hasan Minhaj, I can't invite you to dinner
    I'm sorry Trevor Noah, I can't invite you to dinner
    Hey Matt Bomer, you're still invited to dinner.
    Hey Michael Jackson, you're still invited to dinner.
    []


### 3-8: Seeing the World


```python
places = ['Paris', 'Taiwan', 'Barcelona', 'Venice', 'China', 'Canada', 'Iceland']
print(places)
print(sorted(places))
print(places)
print(sorted(places, reverse=True))
print(places)
places.reverse()
print(places)
places.sort()
print(places)
places.sort(reverse=True)
print(places)


```

    ['Paris', 'Taiwan', 'Barcelona', 'Venice', 'China', 'Canada', 'Iceland']
    ['Barcelona', 'Canada', 'China', 'Iceland', 'Paris', 'Taiwan', 'Venice']
    ['Paris', 'Taiwan', 'Barcelona', 'Venice', 'China', 'Canada', 'Iceland']
    ['Venice', 'Taiwan', 'Paris', 'Iceland', 'China', 'Canada', 'Barcelona']
    ['Paris', 'Taiwan', 'Barcelona', 'Venice', 'China', 'Canada', 'Iceland']
    ['Iceland', 'Canada', 'China', 'Venice', 'Barcelona', 'Taiwan', 'Paris']
    ['Barcelona', 'Canada', 'China', 'Iceland', 'Paris', 'Taiwan', 'Venice']
    ['Venice', 'Taiwan', 'Paris', 'Iceland', 'China', 'Canada', 'Barcelona']


### 4-1: Pizzas


```python
pizzas = ['pepperoni', 'cheese', 'pepper']
for pizza in pizzas:
    print(f"I like {pizza} pizza")
    
```

    I like pepperoni pizza
    I like cheese pizza
    I like pepper pizza


### 4-2: Animals


```python
animals = ['giraffe', 'deer', 'horse']
for animal in animals:
    print(f"I want to see a {animal}")
print("Any of these animals can run fast")
```

    I want to see a giraffe
    I want to see a deer
    I want to see a horse
    Any of these animals can run fast


### 4-3: Counting to Twenty


```python
for i in range(1, 21):
    print(i)
```

    1
    2
    3
    4
    5
    6
    7
    8
    9
    10
    11
    12
    13
    14
    15
    16
    17
    18
    19
    20


### 4-6: Odd Numbers


```python
for i in range(1, 21, 2):
    print(i)
```

    1
    3
    5
    7
    9
    11
    13
    15
    17
    19


### 4-10: Slices


```python
animals = ['giraffe', 'deer', 'horse', 'antelope', 'stallion', 'goat', 'duck', 'chinchilla','ape']
print("The first three animals in the list are:")
for animal in animals[0:3]:
    print("\t" + animal)
print("Three animals from the middle of the list are:")
for animal in animals[3:6]:
    print("\t" + animal)
print("The last three animals in the list are:")
for animal in animals[6:9]:
    print("\t" + animal)
```

    The first three animals in the list are:
    	giraffe
    	deer
    	horse
    Three animals from the middle of the list are:
    	antelope
    	stallion
    	goat
    The last three animals in the list are:
    	duck
    	chinchilla
    	ape


### 4-11: My Pizzas, Your Pizzas


```python
pizzas = ['pepperoni', 'cheese', 'pepper']
friend_pizzas = pizzas
pizzas.append("sausage")
friend_pizzas.append("broccoli")
print("My favorite pizzas are:")
for pizza in pizzas:
    print(pizza)
print("My friend's facorite pizzas are:")
for pizza in friend_pizzas:
    print(pizza)
```

    My favorite pizzas are:
    pepperoni
    cheese
    pepper
    sausage
    broccoli
    My friend's facorite pizzas are:
    pepperoni
    cheese
    pepper
    sausage
    broccoli



```python

```
