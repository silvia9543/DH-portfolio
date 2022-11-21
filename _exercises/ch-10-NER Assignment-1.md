---
layout: page
title: Week 9, NER Assignment
description: Named Entity Recognition
---

# NER Assignment
Georeferencing automatically detected place names in Edward Gibbon's *Decline and Fall of the Roman Empire* using the Pleiades gazatteer and `spaCy`.

Your assignment this week is to output a `CSV` file of place names, frequency and coordinates, as we did in class for a chapter of Gibbon of your choice. Try to find a chapter with a lot of places as we will be turning this data into an online map next week. The steps are:

* Choose a chapter from the text
* Begin a function by parsing input text
* Create a `spaCy` dictionary of entities and frequency
* Use the Pleiaes data from class to find coordinates for each place name
* Run your function on your chosen chapter
* Save your final `CSV`
* Come to class on Monday, ready to use it


```python
# import and download any relevant data
import pandas as pd
import collections
import spacy
nlp = spacy.load('en_core_web_sm')
import wget
import os
if not os.path.isfile('gibbon_text.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/gibbon_text.csv')
gibbon_by_chapter = pd.read_csv('gibbon_text.csv').rename(columns={'Unnamed: 0':'chapter'})
third_chapter = gibbon_by_chapter['StringText'][2]
names = pd.read_csv('names.csv')
places = pd.read_csv('places.csv')

# downloading the Pleiades data we need:
if not os.path.isfile('places.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/places.csv')
if not os.path.isfile('names.csv'):
    wget.download('https://raw.githubusercontent.com/pnadelofficial/FallDHCourseMaterials/main/names.csv')
```


```python
# any helper functions you may need
def get_pleiades_id(term):
    """
    Iterates through all of the possible names in the names.csv file
    Returns None if no matched names
    """
    name_row = names.loc[names['attested_form'] == term]
    if len(name_row) == 1:
        return int(name_row.place_id.iloc[0])
    else:
        name_row = names.loc[names['romanized_form_1'] == term]
        if len(name_row) == 1:
            return int(name_row.place_id.iloc[0])
        else:
            name_row = names.loc[names['romanized_form_2'] == term]
            if len(name_row) == 1:
                return int(name_row.place_id.iloc[0])
            else:
                name_row = names.loc[names['romanized_form_3'] == term]
                if len(name_row) == 1:
                    return int(name_row.place_id.iloc[0])
                else:
                    return None
def get_lat(pl_id):
    places_row = places.loc[places['id'] == pl_id]
    if len(places_row) == 1:
        return places_row.representative_latitude.iloc[0]
    
def get_long(pl_id):
    places_row = places.loc[places['id'] == pl_id]
    if len(places_row) == 1:
        return places_row.representative_longitude.iloc[0]
                
```


```python
# final functions
def get_locations_dict(text):
    doc = nlp(text)
    place_freq = collections.defaultdict(int)
    for entity in doc.ents:
        if (entity.label_ == 'GPE') or (entity.label_ == 'LOC'):
            place_freq[entity.text] += 1
    place_freq = dict(place_freq)
    place_freq_df = pd.DataFrame.from_dict(place_freq, orient='index').reset_index().rename(columns={'index':'place_name',0:'frequency'})
    places = pd.read_csv('places.csv')
    names = pd.read_csv('names.csv')
    place_freq_df['pleiades_id'] = place_freq_df['place_name'].apply(get_pleiades_id)
    place_freq_final = place_freq_df.dropna().reset_index(drop=True)
    rid = place_freq_final.pleiades_id.iloc[0]
    places.loc[places['id'] == rid].representative_latitude
    place_freq_final['lat'] = place_freq_final['pleiades_id'].apply(get_lat)
    place_freq_final['long'] = place_freq_final['pleiades_id'].apply(get_long)
    return place_freq_final
```


```python
# try your function out
print(get_locations_dict(third_chapter))
```

      place_name  frequency  pleiades_id        lat       long
    0       Rome         17     423025.0  41.891775  12.486137
    1     Africa          1        775.0  32.500000   7.500000
    2   Hercules          1     266032.0  37.500000  -0.500000
    3     Aricia          1     422844.0  41.721400  12.673347
    4      Cinna          1     483971.0        NaN        NaN



```python
# save result as CSV
get_locations_dict(third_chapter).to_csv('ch3gibbon_places.csv')
```


```python

```


```python

```
