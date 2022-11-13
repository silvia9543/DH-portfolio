## Ch-8 Exercises: 8-1, 8-2, 8-3, 8-5, 8-6, 8-7

### 8-1. Message: Write a function called display_message() that prints one sentence telling everyone what you are learning about in this chapter. Call the function, and make sure the message displays correctly.


```python
def display_message():
    print("I'm learning about functions in this chapter!")
display_message()
```

    I'm learning about functions in this chapter!


### 8-2. Favorite Book: Write a function called favorite_book() that accepts one parameter, title. The function should print a message, such as One of my favorite books is Alice in Wonderland. Call the function, making sure to include a book title as an argument in the function call.


```python
def favorite_book(title):
    print("One of my favorite books is ", title)
favorite_book("Modern Romance")
```

    One of my favorite books is  Modern Romance


### 8-3. T-Shirt: Write a function called make_shirt() that accepts a size and the text of a message that should be printed on the shirt. The function should print a sentence summarizing the size of the shirt and the message printed on it.

Call the function once using positional arguments to make a shirt. Call the function a second time using keyword arguments.


```python
def make_shirt(size, text):
    print("The size of the shirt is ", size, " and the text is ", text)
make_shirt("small", "have a good day")
make_shirt(size="small", text="have a good day")
```

    The size of the shirt is  small  and the text is  have a good day
    The size of the shirt is  small  and the text is  have a good day


### 8-5. Cities: Write a function called describe_city() that accepts the name of a city and its country. The function should print a simple sentence, such as Reykjavik is in Iceland. Give the parameter for the country a default value. Call your function for three different cities, at least one of which is not in the default country.


```python
def describe_city(city, country='the US'):
    print(city, " is in ", country)
describe_city("New York City")
describe_city("Paris", "France")
describe_city("LA")
```

    New York City  is in  the US
    Paris  is in  France
    LA  is in  the US


### 8-6. City Names: Write a function called city_country() that takes in the name of a city and its country. The function should return a string formatted like this:




```python
def city_country(city, country):
    return city + ", " + country
print(city_country("Paris", "France"))
print(city_country("NYC", "USA"))
print(city_country("Beijing", "China"))
```

    Paris, France
    NYC, USA
    Beijing, China


### 8-7. Album: Write a function called make_album() that builds a dictionary describing a music album. The function should take in an artist name and an album title, and it should return a dictionary containing these two pieces of information. Use the function to make three dictionaries representing different albums. Print each return value to show that the dictionaries are storing the album information correctly.

Use None to add an optional parameter to make_album() that allows you to store the number of songs on an album. If the calling line includes a value for the number of songs, add that value to the album’s dictionary. Make at least one new function call that includes the number of songs on an album.


```python
def make_album(artist_name, album_title, num=None):
    toreturn= {"artist name":artist_name, "album title": album_title}
    if num:
        toreturn["num songs"] = num
    return toreturn
print(make_album("Bruno Mars", "Billionaire"))
print(make_album("Yoasobi", "Book1"))
print(make_album("Honne", "Free Love"))
print(make_album("Honne", "Free Love", 2))
```

    {'artist name': 'Bruno Mars', 'album title': 'Billionaire'}
    {'artist name': 'Yoasobi', 'album title': 'Book1'}
    {'artist name': 'Honne', 'album title': 'Free Love'}
    {'artist name': 'Honne', 'album title': 'Free Love', 'num songs': 2}



```python

```
