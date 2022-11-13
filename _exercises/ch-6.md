---
layout: page
title: Week 6, Exercises Ch. 6
description: Select exercises from Python Crash Course
---

## Chapter 6 Exercises
### 6-1: Person: Use a dictionary to store information about a person you know. Store their first name, last name, age, and the city in which they live. You should have keys such as first_name, last_name, age, and city. Print each piece of information stored in your dictionary.


```python
dict = {}
dict["first_name"] = "Daisy"
dict["last_name"] = "Porter"
dict["age"] = 23
dict["city"] = "New York City"
print(dict)
```

    {'first_name': 'Daisy', 'last_name': 'Porter', 'age': 23, 'city': 'New York City'}


### 6-2. Favorite Numbers: Use a dictionary to store people’s favorite numbers. Think of five names, and use them as keys in your dictionary. Think of a favorite number for each person, and store each as a value in your dictionary. Print each person’s name and their favorite number. For even more fun, poll a few friends and get some actual data for your program.


```python
dict = {}
dict["silvia"] = 9
dict["sammie"] = 20
dict["jeanne"] = 17
dict["elsie"] = 738
dict["janice"] = 3
print(dict)
```

    {'silvia': 9, 'sammie': 20, 'jeanne': 17, 'elsie': 738, 'janice': 3}


### 6-3. Glossary: A Python dictionary can be used to model an actual dictionary. However, to avoid confusion, let’s call it a glossary.


```python
programming_definitions = {"dict": "a data structure that stores key-value pairs", "loop": "a repeating process", "key-value pair": "a set of values associated with each other", "access":"retrieve a value using square brackets", "argument":"a parameter passed into a function"}
```


```python
print("dict: ", programming_definitions["dict"], "\n")
print("loop: ", programming_definitions["loop"], "\n")
print("key-value pair: ", programming_definitions["key-value pair"], "\n")
print("access: ", programming_definitions["access"], "\n")
print("argument: ", programming_definitions["argument"], "\n")
```

    dict:  a data structure that stores key-value pairs 
    
    loop:  a repeating process 
    
    key-value pair:  a set of values associated with each other 
    
    access:  retrieve a value using square brackets 
    
    argument:  a parameter passed into a function 
    


### 6-4. Glossary 2: Now that you know how to loop through a dictionary, clean up the code from Exercise 6-3 (page 99) by replacing your series of print() calls with a loop that runs through the dictionary’s keys and values. When you’re sure that your loop works, add five more Python terms to your glossary. When you run your program again, these new words and meanings should automatically be included in the output.


```python
for definition in programming_definitions:
    print(definition, ": ", programming_definitions[definition], '\n')
programming_definitions["syntax"] = "the language used in code"
programming_definitions["list"] = "a data structure that represents a collection of items"
programming_definitions["print"] = "output something to the console"
programming_definitions["iterate"] = "to go through something one by one"
programming_definitions["set"] = "a data structure with no repeating values"
for definition in programming_definitions:
    print(definition, ": ", programming_definitions[definition], '\n')

```

    dict :  a data structure that stores key-value pairs 
    
    loop :  a repeating process 
    
    key-value pair :  a set of values associated with each other 
    
    access :  retrieve a value using square brackets 
    
    argument :  a parameter passed into a function 
    
    dict :  a data structure that stores key-value pairs 
    
    loop :  a repeating process 
    
    key-value pair :  a set of values associated with each other 
    
    access :  retrieve a value using square brackets 
    
    argument :  a parameter passed into a function 
    
    syntax :  the language used in code 
    
    list :  a data structure that represents a collection of items 
    
    print :  output something to the console 
    
    iterate :  to go through something one by one 
    
    set :  a data structure with no repeating values 
    


### 6-5. Rivers: Make a dictionary containing three major rivers and the country each river runs through. One key-value pair might be 'nile': 'egypt'.


```python
rivers = {'nile':'egypt', 'yellow river':'china', 'hudson':'us'}
for river in rivers:
    print(river)
    print(rivers[river])
```

    nile
    egypt
    yellow river
    china
    hudson
    us


### 6-7. People: Start with the program you wrote for Exercise 6-1 (page 99). Make two new dictionaries representing different people, and store all three dictionaries in a list called people. Loop through your list of people. As you loop through the list, print everything you know about each person.


```python
dict = {}
dict["first_name"] = "Daisy"
dict["last_name"] = "Porter"
dict["age"] = 23
dict["city"] = "New York City"

dict1 = {'first_name':'sand', 'last_name':'shyam', 'age':21, 'city': 'Atlanta'}
dict2 = {'first_name':'Bradley', 'last_name':'May', 'age':21, 'city': 'Chicago'}
people = [dict, dict1, dict2]
for dicts in people:
    print(dicts)
```

    {'first_name': 'Daisy', 'last_name': 'Porter', 'age': 23, 'city': 'New York City'}
    {'first_name': 'sand', 'last_name': 'shyam', 'age': 21, 'city': 'Atlanta'}
    {'first_name': 'Bradley', 'last_name': 'May', 'age': 21, 'city': 'Chicago'}


### 6-8. Pets: Make several dictionaries, where each dictionary represents a different pet. In each dictionary, include the kind of animal and the owner’s name. Store these dictionaries in a list called pets. Next, loop through your list and as you do, print everything you know about each pet.


```python
ray = {'cat':'Silvia'}
golden = {"dog":'Thumper'}
deer = {"deer": 'Bambi'}
list1 = [ray, golden, deer]
for item in list1:
    print(item)
```

    {'cat': 'Silvia'}
    {'dog': 'Thumper'}
    {'deer': 'Bambi'}


### 6-9. Favorite Places: Make a dictionary called favorite_places. Think of three names to use as keys in the dictionary, and store one to three favorite places for each person. To make this exercise a bit more interesting, ask some friends to name a few of their favorite places. Loop through the dictionary, and print each person’s name and their favorite places.


```python
favorite_places = {"Silvia":["New York", "Boston"], "Jeanne":["Boston"], "Xueli":["Taiwan", "Paris", "Shanghai", "London", "NYC"]}
for person in favorite_places:
    print(person, favorite_places[person])
```

    Silvia ['New York', 'Boston']
    Jeanne ['Boston']
    Xueli ['Taiwan', 'Paris', 'Shanghai', 'London', 'NYC']


### 6-10. Favorite Numbers: Modify your program from Exercise 6-2 (page 99) so each person can have more than one favorite number. Then print each person’s name along with their favorite numbers.


```python
dict = {}
dict["silvia"] = [9, 22]
dict["sammie"] = [20, 230, 2]
dict["jeanne"] = [17, 18, 20, 1209, 39]
dict["elsie"] = [738, 29, 30]
dict["janice"] = [3, 5, 7, 44]
print(dict)
```

    {'silvia': [9, 22], 'sammie': [20, 230, 2], 'jeanne': [17, 18, 20, 1209, 39], 'elsie': [738, 29, 30], 'janice': [3, 5, 7, 44]}


### 6-11. Cities: Make a dictionary called cities. Use the names of three cities as keys in your dictionary. Create a dictionary of information about each city and include the country that the city is in, its approximate population, and one fact about that city. The keys for each city’s dictionary should be something like country, population, and fact. Print the name of each city and all of the information you have stored about it.




```python
cities = {"New York":{'country':'US', 'population':'8.4 million', 'fun fact': "It is the largest city in the US by population"}, "Los Angeles":{"country": "US", "population":"3.8 million", "fun fact":"It's the center of the nation's film and tv industry"}, "Paris":{"country":"France", "population": "2.1 million", "fun fact":"Paris is referred to as the city of light"}}
for city in cities:
    print(city, cities[city])
```

    New York {'country': 'US', 'population': '8.4 million', 'fun fact': 'It is the largest city in the US by population'}
    Los Angeles {'country': 'US', 'population': '3.8 million', 'fun fact': "It's the center of the nation's film and tv industry"}
    Paris {'country': 'France', 'population': '2.1 million', 'fun fact': 'Paris is referred to as the city of light'}



```python

```
