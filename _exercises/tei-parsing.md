---
layout: page
title: Week 14, TEI Parsing
description: Parsing a TEI document and extracting its footnotes
---

# Parsing a TEI Document - Assignment

## Instructions

1. Parse the tei text of Gibbon's _Decline and Fall_ as found in `gibbon.xml`.
2. Extract all the footnotes and remove extraneous white space.
3. Place footnotes in a dataframe.
4. Save the dataframe as a csv file.

## Parsing TEI


```python
# imports
import pandas as pd
import re
from bs4 import BeautifulSoup
```


```python
# load xml file
with open('gibbon.xml', encoding='utf8', mode='r') as file:
    tei_string = file.read()
```


```python
# use BeatifulSoup to instantiate tei object
tei_object = BeautifulSoup(tei_string)
```


```python
# find all margin notes
foot_notes = tei_object.find_all('note', attrs={'place':'botton'})
```


```python
# clean margin notes and add to a list
foot_notes = tei_object.find_all('note', attrs={'place':'bottom'})
```


```python
# convert list to dataframe
cleaned_foot_notes = []
for foot_note in foot_notes:
    foot_note_contents = re.sub(r'[\ \n]{2,}' , '',  foot_note.text)
    cleaned_foot_notes.append(foot_note_contents)
```


```python
# check dataframe
df = pd.DataFrame(cleaned_foot_notes)
df.head()
```




<div>
<style scoped>
    .dataframe tbody tr th:only-of-type {
        vertical-align: middle;
    }

    .dataframe tbody tr th {
        vertical-align: top;
    }

    .dataframe thead th {
        text-align: right;
    }
</style>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>0</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>\nPons Aureoli,thirteen miles from Bergamo, an...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>On the death of Gallienus, ſee Trebellius Poll...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Some ſuppoſed him, oddly enough, to be a baſta...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>\nNotoria,a periodical and official diſpatch w...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Hiſt. Auguſt. p. 208. Gallienus deſcribes the ...</td>
    </tr>
  </tbody>
</table>
</div>




```python
# save datafram as csv
df.to_csv('foot_notes.csv')
```
