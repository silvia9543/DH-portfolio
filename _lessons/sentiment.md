---
layout: page
title: Sentiment Analysis for Exploratory Data Analysis
description: Teaches how to conduct 'sentiment analysis' on texts and to interpret the results. This is a form fo exploratory data analysis based on natural language processing. 
---
## Source
[Zoe Wilkinson Saldana, "Sentiment Analysis for Exploratory Data Analysis," Programming Historian 7 (2018), https://doi.org/10.46430/phen0079.](https://programminghistorian.org/en/lessons/sentiment-analysis)

## Reflection

Through this tutorial, I learned how to use natural language processing to conduct sentiment analysis on texts, which seeks to quantify the emotional intensity of words and phrases in a text. Specifically, the tutorial provided sample e-mails in the use case of analyzing Enron's emails as they went bankrupt after concealing a variety of illegal accounting practicies. I really liked how the tutorial used an interesting case study to pull me into the topic, since at the time, the Enron Scandal was the largest collapse of a publicly traded company in history. 

It was interesting to use NTLK, the natural language toolkit since I had never heard about it before. It was relatively simple to understand and the output of the function was also extremely concise and easy to understand. The three categories, neg, neu, and pos give you the quantified values of negativity, neutrality, and positivity in the text provided. I was able to follow along with the code, along with the discussion about sentimental analysis's limitations and warnings, since the text warns against using it too heavily to draw conclusions, but that it can provide valuable empirical analyses. I also liked being able to apply the code to different texts to see the differences between them.

This lesson could be applied to all kinds of projects that involve analyzing humanities text, such as stories, songs, poetry, or even emails and text messages. It could be used to investigate general patterns in society, for example, looking at how men might write emails differently from women in the workplace. And I think it'd be particularly fascinating to use on historical letters or journal entries during significant periods of time, such as during a war, to identify shifts in emotions, relationships, and general sentiment over time. 

```python
import nltk
nltk.download('vader_lexicon')
nltk.download('punkt')

```

    [nltk_data] Downloading package vader_lexicon to
    [nltk_data]     /Users/silviawang/nltk_data...
    [nltk_data] Downloading package punkt to
    [nltk_data]     /Users/silviawang/nltk_data...
    [nltk_data]   Package punkt is already up-to-date!





    True




```python
from nltk.sentiment.vader import SentimentIntensityAnalyzer

```


```python
sid = SentimentIntensityAnalyzer()
```


```python
message_text = '''Like you, I am getting very frustrated with this process. I am genuinely trying to be as reasonable as possible. I am not trying to "hold up" the deal at the last minute. I'm afraid that I am being asked to take a fairly large leap of faith after this company (I don't mean the two of you -- I mean Enron) has screwed me and the people who work for me.'''

```


```python
print(message_text)
scores = sid.polarity_scores(message_text)

```

    Like you, I am getting very frustrated with this process. I am genuinely trying to be as reasonable as possible. I am not trying to "hold up" the deal at the last minute. I'm afraid that I am being asked to take a fairly large leap of faith after this company (I don't mean the two of you -- I mean Enron) has screwed me and the people who work for me.



```python
for key in sorted(scores):
        print('{0}: {1}, '.format(key, scores[key]), end='')
```

    compound: -0.3804, neg: 0.093, neu: 0.836, pos: 0.071, 


```python

sid = SentimentIntensityAnalyzer()

message_text = 'Looks great.  I think we should have a least 1 or 2 real time traders in Calgary.'

print(message_text)

# Calling the polarity_scores method on sid and passing in the message_text outputs a dictionary with negative, neutral, positive, and compound scores for the input text
scores = sid.polarity_scores(message_text)

# Here we loop through the keys contained in scores (pos, neu, neg, and compound scores) and print the key-value pairs on the screen

for key in sorted(scores):
        print('{0}: {1}, '.format(key, scores[key]), end='')
```

    Looks great.  I think we should have a least 1 or 2 real time traders in Calgary.
    compound: 0.6249, neg: 0.0, neu: 0.745, pos: 0.255, 


```python

sid = SentimentIntensityAnalyzer()

message_text = "I think we are making great progress on the systems side.  I would like to set a deadline of November 10th to have a plan on all North American projects (I'm ok if fundementals groups are excluded) that is signed off on by commercial, Sally's world, and Beth's world.  When I say signed off I mean that I want signitures on a piece of paper that everyone is onside with the plan for each project.  If you don't agree don't sign. If certain projects (ie. the gas plan) are not done yet then lay out a timeframe that the plan will be complete.  I want much more in the way of specifics about objectives and timeframe. Thanks for everyone's hard work on this."

print(message_text)

# Calling the polarity_scores method on sid and passing in the message_text outputs a dictionary with negative, neutral, positive, and compound scores for the input text
scores = sid.polarity_scores(message_text)

# Here we loop through the keys contained in scores (pos, neu, neg, and compound scores) and print the key-value pairs on the screen

for key in sorted(scores):
        print('{0}: {1}, '.format(key, scores[key]), end='')
```

    I think we are making great progress on the systems side.  I would like to set a deadline of November 10th to have a plan on all North American projects (I'm ok if fundementals groups are excluded) that is signed off on by commercial, Sally's world, and Beth's world.  When I say signed off I mean that I want signitures on a piece of paper that everyone is onside with the plan for each project.  If you don't agree don't sign. If certain projects (ie. the gas plan) are not done yet then lay out a timeframe that the plan will be complete.  I want much more in the way of specifics about objectives and timeframe. Thanks for everyone's hard work on this.
    compound: 0.8951, neg: 0.042, neu: 0.821, pos: 0.136, 


```python

sid = SentimentIntensityAnalyzer()

message_text = '''It seems to me we are in the middle of no man's land with respect to the  following:  Opec production speculation, Mid east crisis and renewed  tensions, US elections and what looks like a slowing economy (?), and no real weather anywhere in the world. I think it would be most prudent to play  the markets from a very flat price position and try to day trade more aggressively. I have no intentions of outguessing Mr. Greenspan, the US. electorate, the Opec ministers and their new important roles, The Israeli and Palestinian leaders, and somewhat importantly, Mother Nature.  Given that, and that we cannot afford to lose any more money, and that Var seems to be a problem, let's be as flat as possible. I'm ok with spread risk  (not front to backs, but commodity spreads). The morning meetings are not inspiring, and I don't have a real feel for  everyone's passion with respect to the markets.  As such, I'd like to ask  John N. to run the morning meetings on Mon. and Wed.  Thanks. Jeff'''

print(message_text)

# Calling the polarity_scores method on sid and passing in the message_text outputs a dictionary with negative, neutral, positive, and compound scores for the input text
scores = sid.polarity_scores(message_text)

# Here we loop through the keys contained in scores (pos, neu, neg, and compound scores) and print the key-value pairs on the screen

for key in sorted(scores):
        print('{0}: {1}, '.format(key, scores[key]), end='')
```

    It seems to me we are in the middle of no man's land with respect to the  following:  Opec production speculation, Mid east crisis and renewed  tensions, US elections and what looks like a slowing economy (?), and no real weather anywhere in the world. I think it would be most prudent to play  the markets from a very flat price position and try to day trade more aggressively. I have no intentions of outguessing Mr. Greenspan, the US. electorate, the Opec ministers and their new important roles, The Israeli and Palestinian leaders, and somewhat importantly, Mother Nature.  Given that, and that we cannot afford to lose any more money, and that Var seems to be a problem, let's be as flat as possible. I'm ok with spread risk  (not front to backs, but commodity spreads). The morning meetings are not inspiring, and I don't have a real feel for  everyone's passion with respect to the markets.  As such, I'd like to ask  John N. to run the morning meetings on Mon. and Wed.  Thanks. Jeff
    compound: 0.889, neg: 0.096, neu: 0.765, pos: 0.14, 


```python
import nltk.data
from nltk.sentiment.vader import SentimentIntensityAnalyzer
from nltk import sentiment
from nltk import word_tokenize

sid = SentimentIntensityAnalyzer()

tokenizer = nltk.data.load('tokenizers/punkt/english.pickle')

message_text = '''It seems to me we are in the middle of no man's land with respect to the  following:  Opec production speculation, Mid east crisis and renewed  tensions, US elections and what looks like a slowing economy (?), and no real weather anywhere in the world. I think it would be most prudent to play  the markets from a very flat price position and try to day trade more aggressively. I have no intentions of outguessing Mr. Greenspan, the US. electorate, the Opec ministers and their new important roles, The Israeli and Palestinian leaders, and somewhat importantly, Mother Nature.  Given that, and that we cannot afford to lose any more money, and that Var seems to be a problem, let's be as flat as possible. I'm ok with spread risk  (not front to backs, but commodity spreads). The morning meetings are not inspiring, and I don't have a real feel for  everyone's passion with respect to the markets.  As such, I'd like to ask  John N. to run the morning meetings on Mon. and Wed.  Thanks. Jeff'''

sentences = tokenizer.tokenize(message_text)

for sentence in sentences:
        print(sentence)
        scores = sid.polarity_scores(sentence)
        for key in sorted(scores):
                print('{0}: {1}, '.format(key, scores[key]), end='')
        print()

```

    It seems to me we are in the middle of no man's land with respect to the  following:  Opec production speculation, Mid east crisis and renewed  tensions, US elections and what looks like a slowing economy (?
    compound: -0.5267, neg: 0.197, neu: 0.68, pos: 0.123, 
    ), and no real weather anywhere in the world.
    compound: -0.296, neg: 0.216, neu: 0.784, pos: 0.0, 
    I think it would be most prudent to play  the markets from a very flat price position and try to day trade more aggressively.
    compound: 0.0183, neg: 0.103, neu: 0.792, pos: 0.105, 
    I have no intentions of outguessing Mr. Greenspan, the US.
    compound: -0.296, neg: 0.216, neu: 0.784, pos: 0.0, 
    electorate, the Opec ministers and their new important roles, The Israeli and Palestinian leaders, and somewhat importantly, Mother Nature.
    compound: 0.4228, neg: 0.0, neu: 0.817, pos: 0.183, 
    Given that, and that we cannot afford to lose any more money, and that Var seems to be a problem, let's be as flat as possible.
    compound: -0.1134, neg: 0.097, neu: 0.823, pos: 0.081, 
    I'm ok with spread risk  (not front to backs, but commodity spreads).
    compound: -0.0129, neg: 0.2, neu: 0.679, pos: 0.121, 
    The morning meetings are not inspiring, and I don't have a real feel for  everyone's passion with respect to the markets.
    compound: 0.5815, neg: 0.095, neu: 0.655, pos: 0.25, 
    As such, I'd like to ask  John N. to run the morning meetings on Mon.
    compound: 0.3612, neg: 0.0, neu: 0.848, pos: 0.152, 
    and Wed.
    compound: 0.0, neg: 0.0, neu: 1.0, pos: 0.0, 
    Thanks.
    compound: 0.4404, neg: 0.0, neu: 0.0, pos: 1.0, 
    Jeff
    compound: 0.0, neg: 0.0, neu: 1.0, pos: 0.0, 



```python

```
