---
layout: page
title: Text Mining in Python through the HTRC Feature Reader
description: Explains how to use Python to summarize and visualize data on millions of texts from the HathiTrust Research Center's Extracted Features dataset.
---
## Source
[Peter Organisciak, "Text Mining in Python through the HTRC Feature Reader," Programming Historian 7 (2018), https://doi.org/10.46430/phen0058.](https://programminghistorian.org/en/lessons/text-mining-with-extracted-features)

## Reflection

Through this tutorial, I learned the fundamentals of using the Extracted Features dataset with the HTRC Feature Reader, which is designed to make use of data structures from the most popular scientific tools in Python. I looked at data structures for holding text, patterns for querying and filtering that information, and ways to summarize, group, and visualize the data. 

I was able to follow along with the code, but it was a little difficult not to get lost in all of the syntax in the library and keeping track of what each one was for, and what the parameters were for functions like sort(). But I learned how you can extract specific data from text, including specific words, parts of speech, and filter out by pages and other criteria. I also learned how you can find frequencies of words/forms of words and how to see these patterns visually using plt.plot().

```python
from htrc_features import FeatureReader
import os
paths = [os.path.join('data', 'sample-file1.json.bz2'), os.path.join('data', 'sample-file2.json.bz2')]
fr = FeatureReader(paths)
for vol in fr.volumes():
    print(vol.title)
```

    June / by Edith Barnard Delano ; with illustrations.
    You never know your luck; being the story of a matrimonial deserter, by Gilbert Parker ... illustrated by W.L. Jacobs.



```python
vol = fr.first() #reading a single volume
vol
```




<strong><a href='http://hdl.handle.net/2027/nyp.33433074811310'>June / by Edith Barnard Delano ; with illustrations.</a></strong> by <em>Delano, Edith Barnard 1874-1946 , Storer, Florence. ill , Riverside Press prt , Houghton Mifflin Company pbl </em> (1916, 274 pages) - <code>nyp.33433074811310</code>




```python
print(vol.handle_url)
```

    http://hdl.handle.net/2027/nyp.33433074811310



```python
tokens = vol.tokens_per_page()
#Shows just the first few rows, so we can look at what it looks like
tokens.head()
```




    page
    1    5
    2    0
    3    1
    4    0
    5    1
    Name: tokenCount, dtype: int64




```python
%matplotlib inline
tokens.plot()
```




    <AxesSubplot:xlabel='page'>




    
![png](output_6_1.png)
    



```python
tl = vol.tokenlist()
tl[1000:1100:15]

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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>24</th>
      <th>body</th>
      <th>went</th>
      <th>VBD</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="6" valign="top">25</th>
      <th rowspan="6" valign="top">body</th>
      <th>.</th>
      <th>.</th>
      <td>4</td>
    </tr>
    <tr>
      <th>added</th>
      <th>VBD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>come</th>
      <th>VB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>green</th>
      <th>JJ</th>
      <td>1</td>
    </tr>
    <tr>
      <th>knew</th>
      <th>VBD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>moment</th>
      <th>NN</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl_simple = vol.tokenlist(pos=False, pages=False)
# .sample(5) returns five random words from the full result
tl_simple.sample(5)
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>grown-up</th>
      <td>1</td>
    </tr>
    <tr>
      <th>gits</th>
      <td>4</td>
    </tr>
    <tr>
      <th>Many</th>
      <td>1</td>
    </tr>
    <tr>
      <th>goal</th>
      <td>2</td>
    </tr>
    <tr>
      <th>silently</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl_simple['count'] > 100

```




    section  token
    body     !         True
             !'       False
             !u       False
             !—why    False
             "         True
                      ...  
             —         True
             •        False
             •5       False
             •;       False
             ••       False
    Name: count, Length: 4892, dtype: bool




```python
matches = tl_simple['count'] > 100
tl_simple[matches].sample(5)
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>her</th>
      <td>781</td>
    </tr>
    <tr>
      <th>he</th>
      <td>370</td>
    </tr>
    <tr>
      <th>and</th>
      <td>1249</td>
    </tr>
    <tr>
      <th>very</th>
      <td>135</td>
    </tr>
    <tr>
      <th>do</th>
      <td>179</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl_simple[tl_simple['count'] > 100].sample(5)

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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>he</th>
      <td>370</td>
    </tr>
    <tr>
      <th>But</th>
      <td>119</td>
    </tr>
    <tr>
      <th>there</th>
      <td>109</td>
    </tr>
    <tr>
      <th>,</th>
      <td>3251</td>
    </tr>
    <tr>
      <th>who</th>
      <td>110</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl.loc[(17),]
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
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="11" valign="top">body</th>
      <th rowspan="2" valign="top">"</th>
      <th>''</th>
      <td>5</td>
    </tr>
    <tr>
      <th>``</th>
      <td>5</td>
    </tr>
    <tr>
      <th>'m</th>
      <th>VBP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>,</th>
      <th>,</th>
      <td>5</td>
    </tr>
    <tr>
      <th>.</th>
      <th>.</th>
      <td>10</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>we</th>
      <th>PRP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>when</th>
      <th>WRB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>why</th>
      <th>WRB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>within</th>
      <th>IN</th>
      <td>1</td>
    </tr>
    <tr>
      <th>you</th>
      <th>PRP</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
<p>113 rows × 1 columns</p>
</div>




```python
tl.loc[(17, 'body'),]
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="2" valign="top">"</th>
      <th>''</th>
      <td>5</td>
    </tr>
    <tr>
      <th>``</th>
      <td>5</td>
    </tr>
    <tr>
      <th>'m</th>
      <th>VBP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>,</th>
      <th>,</th>
      <td>5</td>
    </tr>
    <tr>
      <th>.</th>
      <th>.</th>
      <td>10</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>we</th>
      <th>PRP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>when</th>
      <th>WRB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>why</th>
      <th>WRB</th>
      <td>1</td>
    </tr>
    <tr>
      <th>within</th>
      <th>IN</th>
      <td>1</td>
    </tr>
    <tr>
      <th>you</th>
      <th>PRP</th>
      <td>5</td>
    </tr>
  </tbody>
</table>
<p>113 rows × 1 columns</p>
</div>




```python
tl.loc[(17, 'body', 'Anne'),]
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
      <th>count</th>
    </tr>
    <tr>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl.loc[(slice(None), slice(None), "Anne"),]

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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>56</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>59</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>64</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>73</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>74</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>75</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>86</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>90</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>91</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>95</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>102</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>109</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>110</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>113</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>115</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>116</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>118</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>119</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>120</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>4</td>
    </tr>
    <tr>
      <th>121</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>122</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>126</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>127</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>129</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>139</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>142</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>143</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>145</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>146</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>147</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>149</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>152</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>157</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>159</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>160</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>162</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>164</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>166</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>171</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>179</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>182</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>185</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>192</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>194</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>195</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>197</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>201</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>219</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>224</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>225</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>264</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl.loc[([37, 38, 52]),]
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">37</th>
      <th rowspan="5" valign="top">body</th>
      <th>!</th>
      <th>.</th>
      <td>5</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">"</th>
      <th>''</th>
      <td>6</td>
    </tr>
    <tr>
      <th>``</th>
      <td>6</td>
    </tr>
    <tr>
      <th>'</th>
      <th>''</th>
      <td>1</td>
    </tr>
    <tr>
      <th>'cause</th>
      <th>,</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">52</th>
      <th rowspan="5" valign="top">body</th>
      <th>wrinkled</th>
      <th>JJ</th>
      <td>1</td>
    </tr>
    <tr>
      <th>you</th>
      <th>PRP</th>
      <td>4</td>
    </tr>
    <tr>
      <th>yours</th>
      <th>PRP</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">—</th>
      <th>CC</th>
      <td>1</td>
    </tr>
    <tr>
      <th>RB</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>377 rows × 1 columns</p>
</div>




```python
tl.loc[(slice(37, 40)),]
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">37</th>
      <th rowspan="5" valign="top">body</th>
      <th>!</th>
      <th>.</th>
      <td>5</td>
    </tr>
    <tr>
      <th rowspan="2" valign="top">"</th>
      <th>''</th>
      <td>6</td>
    </tr>
    <tr>
      <th>``</th>
      <td>6</td>
    </tr>
    <tr>
      <th>'</th>
      <th>''</th>
      <td>1</td>
    </tr>
    <tr>
      <th>'cause</th>
      <th>,</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">40</th>
      <th rowspan="5" valign="top">body</th>
      <th>wore</th>
      <th>VBD</th>
      <td>1</td>
    </tr>
    <tr>
      <th>worth</th>
      <th>JJ</th>
      <td>1</td>
    </tr>
    <tr>
      <th>you</th>
      <th>PRP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>your</th>
      <th>PRP$</th>
      <td>1</td>
    </tr>
    <tr>
      <th>—</th>
      <th>IN</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>481 rows × 1 columns</p>
</div>




```python
tl.loc[(slice(None), slice(None), ["Anne", "Hilary"]),]
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>17</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>19</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>20</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>21</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>23</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>3</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th>259</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>264</th>
      <th>body</th>
      <th>Anne</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>265</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>266</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>2</td>
    </tr>
    <tr>
      <th>267</th>
      <th>body</th>
      <th>Hilary</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>115 rows × 1 columns</p>
</div>




```python
tl_all = vol.tokenlist(section='all')
chapter_pages = tl_all.loc[(slice(None), slice(None), "CHAPTER"),]
chapter_pages
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>19</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>35</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>56</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>73</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>91</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>115</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>141</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>158</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>174</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>193</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>217</th>
      <th>body</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>231</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>246</th>
      <th>header</th>
      <th>CHAPTER</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
# Get just the page numbers from the search for "CHAPTER"
page_numbers = chapter_pages.index.get_level_values('page')

# Visualize the tokens-per-page from before
tokens.plot()

# Add vertical lines for pages with "CHAPTER"
import matplotlib.pyplot as plt
for page_number in page_numbers:
    plt.axvline(x=page_number, color='red')
```


    
![png](output_20_0.png)
    



```python
token_idx = tl.index.get_level_values("token")
tl[token_idx.str.isalpha()]
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
      <th></th>
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>page</th>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>5</th>
      <th>body</th>
      <th>JUNE</th>
      <th>NN</th>
      <td>1</td>
    </tr>
    <tr>
      <th rowspan="4" valign="top">7</th>
      <th rowspan="4" valign="top">body</th>
      <th>LIBRARY</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>MEW</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>OF</th>
      <th>IN</th>
      <td>1</td>
    </tr>
    <tr>
      <th>YORK</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <th>...</th>
      <td>...</td>
    </tr>
    <tr>
      <th rowspan="5" valign="top">268</th>
      <th rowspan="5" valign="top">body</th>
      <th>A</th>
      <th>DT</th>
      <td>1</td>
    </tr>
    <tr>
      <th>CAMBRIDGE</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>MASSACHUSETTS</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>U</th>
      <th>NNP</th>
      <td>1</td>
    </tr>
    <tr>
      <th>cbe</th>
      <th>NN</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
<p>26199 rows × 1 columns</p>
</div>




```python
tl_simple.sort_values('count').head()
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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>dangers</th>
      <td>1</td>
    </tr>
    <tr>
      <th>falsely</th>
      <td>1</td>
    </tr>
    <tr>
      <th>smilingly</th>
      <td>1</td>
    </tr>
    <tr>
      <th>fancy</th>
      <td>1</td>
    </tr>
    <tr>
      <th>smashed</th>
      <td>1</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl_simple.sort_values('count', ascending=False).head()

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
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>,</th>
      <td>3251</td>
    </tr>
    <tr>
      <th>"</th>
      <td>1666</td>
    </tr>
    <tr>
      <th>the</th>
      <td>1565</td>
    </tr>
    <tr>
      <th>.</th>
      <td>1534</td>
    </tr>
    <tr>
      <th>and</th>
      <td>1249</td>
    </tr>
  </tbody>
</table>
</div>




```python
#Exercise: Try to retrieve the five most-common tokens used as a noun (‘NNP’) 
#or a plural noun (‘NNS’) in the book. You will have to get a new tokenlist, 
#without pages but with parts-of-speech, then slice by the criteria, sort, and output the first five rows. 
tl = vol.tokenlist(pages=False)
just_nouns = tl.loc[(slice(None), slice(None), ["NN", "NNS"]),]
top_nouns = just_nouns.sort_values('count', ascending=False)
top_nouns.head(5)
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
      <th></th>
      <th></th>
      <th>count</th>
    </tr>
    <tr>
      <th>section</th>
      <th>token</th>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th rowspan="5" valign="top">body</th>
      <th>doctor</th>
      <th>NN</th>
      <td>83</td>
    </tr>
    <tr>
      <th>time</th>
      <th>NN</th>
      <td>80</td>
    </tr>
    <tr>
      <th>day</th>
      <th>NN</th>
      <td>73</td>
    </tr>
    <tr>
      <th>eyes</th>
      <th>NNS</th>
      <td>61</td>
    </tr>
    <tr>
      <th>way</th>
      <th>NN</th>
      <td>57</td>
    </tr>
  </tbody>
</table>
</div>




```python
tl.groupby(level=["pos"]).sum()

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
      <th>count</th>
    </tr>
    <tr>
      <th>pos</th>
      <th></th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>$</th>
      <td>2</td>
    </tr>
    <tr>
      <th>''</th>
      <td>954</td>
    </tr>
    <tr>
      <th>,</th>
      <td>3276</td>
    </tr>
    <tr>
      <th>-LRB-</th>
      <td>4</td>
    </tr>
    <tr>
      <th>-RRB-</th>
      <td>6</td>
    </tr>
    <tr>
      <th>.</th>
      <td>2345</td>
    </tr>
    <tr>
      <th>:</th>
      <td>398</td>
    </tr>
    <tr>
      <th>CC</th>
      <td>1731</td>
    </tr>
    <tr>
      <th>CD</th>
      <td>509</td>
    </tr>
    <tr>
      <th>DT</th>
      <td>3224</td>
    </tr>
    <tr>
      <th>EX</th>
      <td>90</td>
    </tr>
    <tr>
      <th>FW</th>
      <td>27</td>
    </tr>
    <tr>
      <th>IN</th>
      <td>4541</td>
    </tr>
    <tr>
      <th>JJ</th>
      <td>2457</td>
    </tr>
    <tr>
      <th>JJR</th>
      <td>101</td>
    </tr>
    <tr>
      <th>JJS</th>
      <td>66</td>
    </tr>
    <tr>
      <th>MD</th>
      <td>663</td>
    </tr>
    <tr>
      <th>NC</th>
      <td>4</td>
    </tr>
    <tr>
      <th>NN</th>
      <td>4700</td>
    </tr>
    <tr>
      <th>NNP</th>
      <td>2686</td>
    </tr>
    <tr>
      <th>NNPS</th>
      <td>9</td>
    </tr>
    <tr>
      <th>NNS</th>
      <td>1342</td>
    </tr>
    <tr>
      <th>PDT</th>
      <td>36</td>
    </tr>
    <tr>
      <th>POS</th>
      <td>376</td>
    </tr>
    <tr>
      <th>PRP</th>
      <td>3845</td>
    </tr>
    <tr>
      <th>PRP$</th>
      <td>1062</td>
    </tr>
    <tr>
      <th>RB</th>
      <td>2939</td>
    </tr>
    <tr>
      <th>RBR</th>
      <td>74</td>
    </tr>
    <tr>
      <th>RBS</th>
      <td>20</td>
    </tr>
    <tr>
      <th>RP</th>
      <td>192</td>
    </tr>
    <tr>
      <th>SYM</th>
      <td>2</td>
    </tr>
    <tr>
      <th>TO</th>
      <td>1102</td>
    </tr>
    <tr>
      <th>UH</th>
      <td>231</td>
    </tr>
    <tr>
      <th>VB</th>
      <td>1776</td>
    </tr>
    <tr>
      <th>VBD</th>
      <td>3445</td>
    </tr>
    <tr>
      <th>VBG</th>
      <td>601</td>
    </tr>
    <tr>
      <th>VBN</th>
      <td>933</td>
    </tr>
    <tr>
      <th>VBP</th>
      <td>702</td>
    </tr>
    <tr>
      <th>VBZ</th>
      <td>417</td>
    </tr>
    <tr>
      <th>WDT</th>
      <td>105</td>
    </tr>
    <tr>
      <th>WP</th>
      <td>244</td>
    </tr>
    <tr>
      <th>WP$</th>
      <td>2</td>
    </tr>
    <tr>
      <th>WRB</th>
      <td>309</td>
    </tr>
    <tr>
      <th>XP</th>
      <td>5</td>
    </tr>
    <tr>
      <th>``</th>
      <td>812</td>
    </tr>
  </tbody>
</table>
</div>




```python
line_counts = vol.line_counts()
plt.plot(line_counts)
```




    [<matplotlib.lines.Line2D at 0x7fb73ef74ee0>]




    
![png](output_26_1.png)
    



```python

```
