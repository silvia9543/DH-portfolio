---
layout: page
title: Week 5, Exercises Ch. 5
description: Select exercises from Python Crash Course
---
### 5-1: Conditional Tests


```python
car = 'tesla'
print("Is car == 'tesla'? I predict True.")
print(car == 'tesla')

print("\nIs car == 'audi'? I predict False.")
print(car == 'audi')
```

    Is car == 'tesla'? I predict True.
    True
    
    Is car == 'audi'? I predict False.
    False


### 5-2: More Conditional Tests


```python
print("string" == "not_string")
print("string" == "string")
print("string" == "STRING".lower())
print("string" == "NOTSTRING".lower())
print(5>6)
print(5<6)
print(5==6)
print(5==5)
print(5<6)
print(6<5)
print(5>=6)
print(5<=6)
print(True and True)
print(True and False)
print(False and False)
print(True or False)
print(False or False)
print(True or True)
print("hi" in ["hi","hello"])
print("hi" not in ["hell0"])

```

    False
    True
    True
    False
    False
    True
    False
    True
    True
    False
    False
    True
    True
    False
    False
    True
    False
    True
    True
    True


### 5-6: Stages of Life


```python
age = 21
if age < 2:
    print("person is a baby")
elif age < 4 and age < 13:
    print("person is a toddler")
elif age < 20:
    print("person is a teenager")
elif age < 65:
    print("person is an adult")
else:
    print("person is an elder")
```

    person is an adult


### 5-7: Favorite Fruit


```python
favorite_fruits = ["apple", 'banana', 'grapes']
if "apple" in favorite_fruits:
    print("You really like apples!")
if "banana" in favorite_fruits:
    print("You really like bananas!")
if "pear" in favorite_fruits:
    print("You really like pears!")
if "grapes" in favorite_fruits:
    print("You really like grapes!")
if "lychee" in favorite_fruits:
    print("You really like lychees!")

```

    You really like apples!
    You really like bananas!
    You really like grapes!


### 5-8: Hello Admin


```python
usernames = ['admin', 'silvs123', 'user23', 'cat03', 'dog13']
for user in usernames:
    if user == 'admin':
        print("Hello admin, would you like to see a status report?")
    else:
        print(f"Hello {user}, thank you for logging in again.")
```

    Hello admin, would you like to see a status report?
    Hello silvs123, thank you for logging in again.
    Hello user23, thank you for logging in again.
    Hello cat03, thank you for logging in again.
    Hello dog13, thank you for logging in again.


### 5-9: No Users


```python
usernames = []
if not usernames:
    print("We need to find some users!")
for user in usernames:
    if user == 'admin':
        print("Hello admin, would you like to see a status report?")
    else:
        print(f"Hello {user}, thank you for logging in again.")
```

    We need to find some users!


### 5-10: Checking Usernames


```python
current_users = ['john123', 'marie9', 'sw938', 'user1', 'admin']
new_users = ['john123', 'marie9', 'jayden', 'sally']
for user in new_users:
    if user.lower() in current_users:
        print("You need to enter a new username.")
    else:
        print("Username is available!")
```

    You need to enter a new username.
    You need to enter a new username.
    Username is available!
    Username is available!



```python

```
