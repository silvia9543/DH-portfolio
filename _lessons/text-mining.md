---
layout: page
title: Text Mining in Python through the HTRC Feature Reader
description: Explains how to use Python to summarize and visualize data on millions of texts from the HathiTrust Research Center's Extracted Features dataset.
---
## Source
[Peter Organisciak, "Text Mining in Python through the HTRC Feature Reader," Programming Historian 7 (2018), https://doi.org/10.46430/phen0058.](https://programminghistorian.org/en/lessons/text-mining-with-extracted-features)

## Reflection

This tutorial teaches the fundamentals of using the Extracted Features dataset with the HTRC Feature Reader, which is designed to make use of data structures from the most popular scientific tools in Python. We will look at data structures for holding text, patterns for querying and filtering that information, and ways to summarize, group, and visualize the data. 

I couldn't get through the whole tutorial because I couldn't figure out this error:
---------------------------------------------------------------------------
ModuleNotFoundError                       Traceback (most recent call last)
Input In [3], in <cell line: 1>()
----> 1 from htrc_features import FeatureReader
      2 import os
      3 paths = [os.path.join('data', 'sample-file1.json.bz2'), os.path.join('data', 'sample-file2.json.bz2')]

ModuleNotFoundError: No module named 'htrc_features'

I tried reinstalling the library using their commands, but it still didn't get rid of the error. I'm not sure if I have to do something else in Jupiter Notebooks? I will finish the rest of this tutorial once I figure out the error, any help on this would be appreciated!