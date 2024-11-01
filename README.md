```python

```

# Project: Investigate a Dataset - [Gapminder world]

## Table of Contents
<ul>
<li><a href="#intro">Introduction</a></li>
<li><a href="#wrangling">Data Wrangling</a></li>
<li><a href="#eda">Exploratory Data Analysis</a></li>
<li><a href="#conclusions">Conclusions</a></li>
</ul>

<a id='intro'></a>
## Introduction

### Dataset Description 

> The data set of this project is from Gapminder, and contains a lot of information about how people live their lives in different countries, tracked across the years, and on a number of different indicators which are population, income per person, average child per woman (fertility), and life expectancy (average number of years a new born child would live)  


### Question(s) for Analysis
> Q1/ Are population levels of countries and income per person in those countries related?

> Q2/ Which continent has the highest in average income per person across the last 42 years? And wich continents come in the second and third places?

>  Q3/ Is there a relationship between population levels and child per woman (fertility)?

>  Q4/ Can we say that population and life expectancy are related to each other?


```python
# Use this cell to set up import statements for all of the packages that you
#   plan to use.
#import numpy as np
#import pandas as pd
#import matplotlib.pyplot as plt
#import seaborn as sns
#%matplotlib inline
```


```python
# Upgrade pandas to use dataframe.explode() function. 
#!pip install --upgrade pandas==0.25.0
```

    Requirement already up-to-date: pandas==0.25.0 in /opt/conda/lib/python3.6/site-packages (0.25.0)
    Requirement already satisfied, skipping upgrade: numpy>=1.13.3 in /opt/conda/lib/python3.6/site-packages (from pandas==0.25.0) (1.19.5)
    Requirement already satisfied, skipping upgrade: python-dateutil>=2.6.1 in /opt/conda/lib/python3.6/site-packages (from pandas==0.25.0) (2.6.1)
    Requirement already satisfied, skipping upgrade: pytz>=2017.2 in /opt/conda/lib/python3.6/site-packages (from pandas==0.25.0) (2017.3)
    Requirement already satisfied, skipping upgrade: six>=1.5 in /opt/conda/lib/python3.6/site-packages (from python-dateutil>=2.6.1->pandas==0.25.0) (1.11.0)


<a id='wrangling'></a>
## Data Wrangling


```python
# Load your data and print out a few lines. Perform operations to inspect data
#   types and look for instances of missing or possibly errant data.
df_pop = pd.read_csv('population_total.csv')
df_inc = pd.read_csv('income_per_person.csv')
df_fert = pd.read_csv('total_fertility.csv')
df_life = pd.read_csv('life_expectancy_years.csv')
```


```python
# inspecting the first rows of population
df_pop.head(5)
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
      <th>country</th>
      <th>1800</th>
      <th>1801</th>
      <th>1802</th>
      <th>1803</th>
      <th>1804</th>
      <th>1805</th>
      <th>1806</th>
      <th>1807</th>
      <th>1808</th>
      <th>...</th>
      <th>2091</th>
      <th>2092</th>
      <th>2093</th>
      <th>2094</th>
      <th>2095</th>
      <th>2096</th>
      <th>2097</th>
      <th>2098</th>
      <th>2099</th>
      <th>2100</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>3.28M</td>
      <td>3.28M</td>
      <td>3.28M</td>
      <td>3.28M</td>
      <td>3.28M</td>
      <td>3.28M</td>
      <td>3.28M</td>
      <td>3.28M</td>
      <td>3.28M</td>
      <td>...</td>
      <td>76.6M</td>
      <td>76.4M</td>
      <td>76.3M</td>
      <td>76.1M</td>
      <td>76M</td>
      <td>75.8M</td>
      <td>75.6M</td>
      <td>75.4M</td>
      <td>75.2M</td>
      <td>74.9M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>1.57M</td>
      <td>1.57M</td>
      <td>1.57M</td>
      <td>1.57M</td>
      <td>1.57M</td>
      <td>1.57M</td>
      <td>1.57M</td>
      <td>1.57M</td>
      <td>1.57M</td>
      <td>...</td>
      <td>168M</td>
      <td>170M</td>
      <td>172M</td>
      <td>175M</td>
      <td>177M</td>
      <td>179M</td>
      <td>182M</td>
      <td>184M</td>
      <td>186M</td>
      <td>188M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>400k</td>
      <td>402k</td>
      <td>404k</td>
      <td>405k</td>
      <td>407k</td>
      <td>409k</td>
      <td>411k</td>
      <td>413k</td>
      <td>414k</td>
      <td>...</td>
      <td>1.33M</td>
      <td>1.3M</td>
      <td>1.27M</td>
      <td>1.25M</td>
      <td>1.22M</td>
      <td>1.19M</td>
      <td>1.17M</td>
      <td>1.14M</td>
      <td>1.11M</td>
      <td>1.09M</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>2650</td>
      <td>2650</td>
      <td>2650</td>
      <td>2650</td>
      <td>2650</td>
      <td>2650</td>
      <td>2650</td>
      <td>2650</td>
      <td>2650</td>
      <td>...</td>
      <td>63k</td>
      <td>62.9k</td>
      <td>62.9k</td>
      <td>62.8k</td>
      <td>62.7k</td>
      <td>62.7k</td>
      <td>62.6k</td>
      <td>62.5k</td>
      <td>62.5k</td>
      <td>62.4k</td>
    </tr>
    <tr>
      <th>4</th>
      <td>United Arab Emirates</td>
      <td>40.2k</td>
      <td>40.2k</td>
      <td>40.2k</td>
      <td>40.2k</td>
      <td>40.2k</td>
      <td>40.2k</td>
      <td>40.2k</td>
      <td>40.2k</td>
      <td>40.2k</td>
      <td>...</td>
      <td>12.3M</td>
      <td>12.4M</td>
      <td>12.5M</td>
      <td>12.5M</td>
      <td>12.6M</td>
      <td>12.7M</td>
      <td>12.7M</td>
      <td>12.8M</td>
      <td>12.8M</td>
      <td>12.9M</td>
    </tr>
  </tbody>
</table>
<p>5 rows Ã— 302 columns</p>
</div>




```python
# inspecting the first rows of income
df_inc.head(5)
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
      <th>country</th>
      <th>1800</th>
      <th>1801</th>
      <th>1802</th>
      <th>1803</th>
      <th>1804</th>
      <th>1805</th>
      <th>1806</th>
      <th>1807</th>
      <th>1808</th>
      <th>...</th>
      <th>2041</th>
      <th>2042</th>
      <th>2043</th>
      <th>2044</th>
      <th>2045</th>
      <th>2046</th>
      <th>2047</th>
      <th>2048</th>
      <th>2049</th>
      <th>2050</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>683</td>
      <td>683</td>
      <td>683</td>
      <td>683</td>
      <td>683</td>
      <td>683</td>
      <td>683</td>
      <td>683</td>
      <td>683</td>
      <td>...</td>
      <td>2690</td>
      <td>2750</td>
      <td>2810</td>
      <td>2870</td>
      <td>2930</td>
      <td>2990</td>
      <td>3060</td>
      <td>3120</td>
      <td>3190</td>
      <td>3260</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>700</td>
      <td>702</td>
      <td>705</td>
      <td>709</td>
      <td>711</td>
      <td>714</td>
      <td>718</td>
      <td>721</td>
      <td>725</td>
      <td>...</td>
      <td>8000</td>
      <td>8170</td>
      <td>8350</td>
      <td>8530</td>
      <td>8710</td>
      <td>8900</td>
      <td>9090</td>
      <td>9280</td>
      <td>9480</td>
      <td>9690</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>755</td>
      <td>755</td>
      <td>755</td>
      <td>755</td>
      <td>755</td>
      <td>756</td>
      <td>756</td>
      <td>756</td>
      <td>756</td>
      <td>...</td>
      <td>25.1k</td>
      <td>25.6k</td>
      <td>26.2k</td>
      <td>26.7k</td>
      <td>27.3k</td>
      <td>27.9k</td>
      <td>28.5k</td>
      <td>29.1k</td>
      <td>29.7k</td>
      <td>30.4k</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>1360</td>
      <td>1360</td>
      <td>1360</td>
      <td>1360</td>
      <td>1370</td>
      <td>1370</td>
      <td>1370</td>
      <td>1370</td>
      <td>1380</td>
      <td>...</td>
      <td>68.9k</td>
      <td>70.4k</td>
      <td>71.9k</td>
      <td>73.4k</td>
      <td>75k</td>
      <td>76.6k</td>
      <td>78.3k</td>
      <td>80k</td>
      <td>81.7k</td>
      <td>83.4k</td>
    </tr>
    <tr>
      <th>4</th>
      <td>United Arab Emirates</td>
      <td>1130</td>
      <td>1130</td>
      <td>1140</td>
      <td>1140</td>
      <td>1150</td>
      <td>1150</td>
      <td>1160</td>
      <td>1160</td>
      <td>1160</td>
      <td>...</td>
      <td>101k</td>
      <td>103k</td>
      <td>105k</td>
      <td>107k</td>
      <td>110k</td>
      <td>112k</td>
      <td>114k</td>
      <td>117k</td>
      <td>119k</td>
      <td>122k</td>
    </tr>
  </tbody>
</table>
<p>5 rows Ã— 252 columns</p>
</div>




```python
# inspecting the first rows of fertility(child per woman)
df_fert.head(5)
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
      <th>country</th>
      <th>1800</th>
      <th>1801</th>
      <th>1802</th>
      <th>1803</th>
      <th>1804</th>
      <th>1805</th>
      <th>1806</th>
      <th>1807</th>
      <th>1808</th>
      <th>...</th>
      <th>2091</th>
      <th>2092</th>
      <th>2093</th>
      <th>2094</th>
      <th>2095</th>
      <th>2096</th>
      <th>2097</th>
      <th>2098</th>
      <th>2099</th>
      <th>2100</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aruba</td>
      <td>5.64</td>
      <td>5.64</td>
      <td>5.64</td>
      <td>5.64</td>
      <td>5.64</td>
      <td>5.64</td>
      <td>5.64</td>
      <td>5.64</td>
      <td>5.64</td>
      <td>...</td>
      <td>1.82</td>
      <td>1.82</td>
      <td>1.82</td>
      <td>1.82</td>
      <td>1.82</td>
      <td>1.82</td>
      <td>1.82</td>
      <td>1.82</td>
      <td>1.83</td>
      <td>1.83</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>7.00</td>
      <td>7.00</td>
      <td>7.00</td>
      <td>7.00</td>
      <td>7.00</td>
      <td>7.00</td>
      <td>7.00</td>
      <td>7.00</td>
      <td>7.00</td>
      <td>...</td>
      <td>1.74</td>
      <td>1.74</td>
      <td>1.74</td>
      <td>1.74</td>
      <td>1.74</td>
      <td>1.74</td>
      <td>1.74</td>
      <td>1.74</td>
      <td>1.74</td>
      <td>1.74</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Angola</td>
      <td>6.93</td>
      <td>6.93</td>
      <td>6.93</td>
      <td>6.93</td>
      <td>6.93</td>
      <td>6.93</td>
      <td>6.93</td>
      <td>6.94</td>
      <td>6.94</td>
      <td>...</td>
      <td>2.54</td>
      <td>2.52</td>
      <td>2.50</td>
      <td>2.48</td>
      <td>2.47</td>
      <td>2.45</td>
      <td>2.43</td>
      <td>2.42</td>
      <td>2.40</td>
      <td>2.40</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>4.60</td>
      <td>4.60</td>
      <td>4.60</td>
      <td>4.60</td>
      <td>4.60</td>
      <td>4.60</td>
      <td>4.60</td>
      <td>4.60</td>
      <td>4.60</td>
      <td>...</td>
      <td>1.78</td>
      <td>1.78</td>
      <td>1.78</td>
      <td>1.79</td>
      <td>1.79</td>
      <td>1.79</td>
      <td>1.79</td>
      <td>1.79</td>
      <td>1.79</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Netherlands Antilles</td>
      <td>5.80</td>
      <td>5.80</td>
      <td>5.80</td>
      <td>5.80</td>
      <td>5.80</td>
      <td>5.80</td>
      <td>5.80</td>
      <td>5.80</td>
      <td>5.80</td>
      <td>...</td>
      <td>2.00</td>
      <td>2.00</td>
      <td>2.01</td>
      <td>2.01</td>
      <td>2.01</td>
      <td>2.01</td>
      <td>2.01</td>
      <td>2.02</td>
      <td>2.02</td>
      <td>2.02</td>
    </tr>
  </tbody>
</table>
<p>5 rows Ã— 302 columns</p>
</div>




```python
# inspecting the first rows of life(averave life expactancy for new born child)
df_life.head(5)
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
      <th>country</th>
      <th>1800</th>
      <th>1801</th>
      <th>1802</th>
      <th>1803</th>
      <th>1804</th>
      <th>1805</th>
      <th>1806</th>
      <th>1807</th>
      <th>1808</th>
      <th>...</th>
      <th>2091</th>
      <th>2092</th>
      <th>2093</th>
      <th>2094</th>
      <th>2095</th>
      <th>2096</th>
      <th>2097</th>
      <th>2098</th>
      <th>2099</th>
      <th>2100</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>28.2</td>
      <td>28.2</td>
      <td>28.2</td>
      <td>28.2</td>
      <td>28.2</td>
      <td>28.2</td>
      <td>28.1</td>
      <td>28.1</td>
      <td>28.1</td>
      <td>...</td>
      <td>75.5</td>
      <td>75.7</td>
      <td>75.8</td>
      <td>76.0</td>
      <td>76.1</td>
      <td>76.2</td>
      <td>76.4</td>
      <td>76.5</td>
      <td>76.6</td>
      <td>76.8</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>27.0</td>
      <td>...</td>
      <td>78.8</td>
      <td>79.0</td>
      <td>79.1</td>
      <td>79.2</td>
      <td>79.3</td>
      <td>79.5</td>
      <td>79.6</td>
      <td>79.7</td>
      <td>79.9</td>
      <td>80.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>35.4</td>
      <td>35.4</td>
      <td>35.4</td>
      <td>35.4</td>
      <td>35.4</td>
      <td>35.4</td>
      <td>35.4</td>
      <td>35.4</td>
      <td>35.4</td>
      <td>...</td>
      <td>87.4</td>
      <td>87.5</td>
      <td>87.6</td>
      <td>87.7</td>
      <td>87.8</td>
      <td>87.9</td>
      <td>88.0</td>
      <td>88.2</td>
      <td>88.3</td>
      <td>88.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>...</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>United Arab Emirates</td>
      <td>30.7</td>
      <td>30.7</td>
      <td>30.7</td>
      <td>30.7</td>
      <td>30.7</td>
      <td>30.7</td>
      <td>30.7</td>
      <td>30.7</td>
      <td>30.7</td>
      <td>...</td>
      <td>82.4</td>
      <td>82.5</td>
      <td>82.6</td>
      <td>82.7</td>
      <td>82.8</td>
      <td>82.9</td>
      <td>83.0</td>
      <td>83.1</td>
      <td>83.2</td>
      <td>83.3</td>
    </tr>
  </tbody>
</table>
<p>5 rows Ã— 302 columns</p>
</div>




```python
# convert years from being a row into a column and giving it a column name year - poulation data, and check changes
df_pop = pd.melt(df_pop, id_vars=['country'], var_name="year", value_vars=df_pop.columns[1:], value_name= "population")
df_pop
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1800</td>
      <td>3.28M</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>1800</td>
      <td>1.57M</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>1800</td>
      <td>400k</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>1800</td>
      <td>2650</td>
    </tr>
    <tr>
      <th>4</th>
      <td>United Arab Emirates</td>
      <td>1800</td>
      <td>40.2k</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Argentina</td>
      <td>1800</td>
      <td>534k</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Armenia</td>
      <td>1800</td>
      <td>413k</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Antigua and Barbuda</td>
      <td>1800</td>
      <td>37k</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Australia</td>
      <td>1800</td>
      <td>200k</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Austria</td>
      <td>1800</td>
      <td>3M</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Azerbaijan</td>
      <td>1800</td>
      <td>880k</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Burundi</td>
      <td>1800</td>
      <td>899k</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Belgium</td>
      <td>1800</td>
      <td>3.25M</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Benin</td>
      <td>1800</td>
      <td>637k</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burkina Faso</td>
      <td>1800</td>
      <td>1.67M</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Bangladesh</td>
      <td>1800</td>
      <td>19.2M</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Bulgaria</td>
      <td>1800</td>
      <td>2.25M</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Bahrain</td>
      <td>1800</td>
      <td>64.5k</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Bahamas</td>
      <td>1800</td>
      <td>27.4k</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Bosnia and Herzegovina</td>
      <td>1800</td>
      <td>852k</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Belarus</td>
      <td>1800</td>
      <td>2.36M</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Belize</td>
      <td>1800</td>
      <td>25.5k</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Bolivia</td>
      <td>1800</td>
      <td>887k</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Brazil</td>
      <td>1800</td>
      <td>2.5M</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Barbados</td>
      <td>1800</td>
      <td>81.7k</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Brunei</td>
      <td>1800</td>
      <td>2260</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Bhutan</td>
      <td>1800</td>
      <td>392k</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Botswana</td>
      <td>1800</td>
      <td>121k</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Central African Republic</td>
      <td>1800</td>
      <td>479k</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Canada</td>
      <td>1800</td>
      <td>500k</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>59267</th>
      <td>Eswatini</td>
      <td>2100</td>
      <td>2.15M</td>
    </tr>
    <tr>
      <th>59268</th>
      <td>Seychelles</td>
      <td>2100</td>
      <td>88.3k</td>
    </tr>
    <tr>
      <th>59269</th>
      <td>Syria</td>
      <td>2100</td>
      <td>36.1M</td>
    </tr>
    <tr>
      <th>59270</th>
      <td>Chad</td>
      <td>2100</td>
      <td>61.8M</td>
    </tr>
    <tr>
      <th>59271</th>
      <td>Togo</td>
      <td>2100</td>
      <td>26.9M</td>
    </tr>
    <tr>
      <th>59272</th>
      <td>Thailand</td>
      <td>2100</td>
      <td>46M</td>
    </tr>
    <tr>
      <th>59273</th>
      <td>Tajikistan</td>
      <td>2100</td>
      <td>25.3M</td>
    </tr>
    <tr>
      <th>59274</th>
      <td>Turkmenistan</td>
      <td>2100</td>
      <td>8.42M</td>
    </tr>
    <tr>
      <th>59275</th>
      <td>Timor-Leste</td>
      <td>2100</td>
      <td>2.37M</td>
    </tr>
    <tr>
      <th>59276</th>
      <td>Tonga</td>
      <td>2100</td>
      <td>138k</td>
    </tr>
    <tr>
      <th>59277</th>
      <td>Trinidad and Tobago</td>
      <td>2100</td>
      <td>969k</td>
    </tr>
    <tr>
      <th>59278</th>
      <td>Tunisia</td>
      <td>2100</td>
      <td>13M</td>
    </tr>
    <tr>
      <th>59279</th>
      <td>Turkey</td>
      <td>2100</td>
      <td>86.2M</td>
    </tr>
    <tr>
      <th>59280</th>
      <td>Tuvalu</td>
      <td>2100</td>
      <td>20k</td>
    </tr>
    <tr>
      <th>59281</th>
      <td>Taiwan</td>
      <td>2100</td>
      <td>16.3M</td>
    </tr>
    <tr>
      <th>59282</th>
      <td>Tanzania</td>
      <td>2100</td>
      <td>286M</td>
    </tr>
    <tr>
      <th>59283</th>
      <td>Uganda</td>
      <td>2100</td>
      <td>137M</td>
    </tr>
    <tr>
      <th>59284</th>
      <td>Ukraine</td>
      <td>2100</td>
      <td>24.4M</td>
    </tr>
    <tr>
      <th>59285</th>
      <td>Uruguay</td>
      <td>2100</td>
      <td>3.18M</td>
    </tr>
    <tr>
      <th>59286</th>
      <td>United States</td>
      <td>2100</td>
      <td>434M</td>
    </tr>
    <tr>
      <th>59287</th>
      <td>Uzbekistan</td>
      <td>2100</td>
      <td>42.3M</td>
    </tr>
    <tr>
      <th>59288</th>
      <td>St. Vincent and the Grenadines</td>
      <td>2100</td>
      <td>74.6k</td>
    </tr>
    <tr>
      <th>59289</th>
      <td>Venezuela</td>
      <td>2100</td>
      <td>34.2M</td>
    </tr>
    <tr>
      <th>59290</th>
      <td>Vietnam</td>
      <td>2100</td>
      <td>97.4M</td>
    </tr>
    <tr>
      <th>59291</th>
      <td>Vanuatu</td>
      <td>2100</td>
      <td>968k</td>
    </tr>
    <tr>
      <th>59292</th>
      <td>Samoa</td>
      <td>2100</td>
      <td>310k</td>
    </tr>
    <tr>
      <th>59293</th>
      <td>Yemen</td>
      <td>2100</td>
      <td>53.2M</td>
    </tr>
    <tr>
      <th>59294</th>
      <td>South Africa</td>
      <td>2100</td>
      <td>79.2M</td>
    </tr>
    <tr>
      <th>59295</th>
      <td>Zambia</td>
      <td>2100</td>
      <td>81.5M</td>
    </tr>
    <tr>
      <th>59296</th>
      <td>Zimbabwe</td>
      <td>2100</td>
      <td>31M</td>
    </tr>
  </tbody>
</table>
<p>59297 rows Ã— 3 columns</p>
</div>




```python
# convert years from being a row into a column and giving it a column name year - income data, and check changes
df_inc = pd.melt(df_inc, id_vars=['country'], var_name="year", value_vars=df_inc.columns[1:], value_name= "income")
df_inc
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
      <th>country</th>
      <th>year</th>
      <th>income</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1800</td>
      <td>683</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>1800</td>
      <td>700</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>1800</td>
      <td>755</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>1800</td>
      <td>1360</td>
    </tr>
    <tr>
      <th>4</th>
      <td>United Arab Emirates</td>
      <td>1800</td>
      <td>1130</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Argentina</td>
      <td>1800</td>
      <td>1730</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Armenia</td>
      <td>1800</td>
      <td>582</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Antigua and Barbuda</td>
      <td>1800</td>
      <td>857</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Australia</td>
      <td>1800</td>
      <td>925</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Austria</td>
      <td>1800</td>
      <td>2090</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Azerbaijan</td>
      <td>1800</td>
      <td>877</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Burundi</td>
      <td>1800</td>
      <td>473</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Belgium</td>
      <td>1800</td>
      <td>2700</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Benin</td>
      <td>1800</td>
      <td>676</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burkina Faso</td>
      <td>1800</td>
      <td>543</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Bangladesh</td>
      <td>1800</td>
      <td>992</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Bulgaria</td>
      <td>1800</td>
      <td>1230</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Bahrain</td>
      <td>1800</td>
      <td>1400</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Bahamas</td>
      <td>1800</td>
      <td>1640</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Bosnia and Herzegovina</td>
      <td>1800</td>
      <td>757</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Belarus</td>
      <td>1800</td>
      <td>688</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Belize</td>
      <td>1800</td>
      <td>655</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Bolivia</td>
      <td>1800</td>
      <td>967</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Brazil</td>
      <td>1800</td>
      <td>1010</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Barbados</td>
      <td>1800</td>
      <td>1030</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Brunei</td>
      <td>1800</td>
      <td>1710</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Bhutan</td>
      <td>1800</td>
      <td>712</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Botswana</td>
      <td>1800</td>
      <td>449</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Central African Republic</td>
      <td>1800</td>
      <td>480</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Canada</td>
      <td>1800</td>
      <td>1490</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>48915</th>
      <td>Eswatini</td>
      <td>2050</td>
      <td>14.4k</td>
    </tr>
    <tr>
      <th>48916</th>
      <td>Seychelles</td>
      <td>2050</td>
      <td>58.4k</td>
    </tr>
    <tr>
      <th>48917</th>
      <td>Syria</td>
      <td>2050</td>
      <td>7110</td>
    </tr>
    <tr>
      <th>48918</th>
      <td>Chad</td>
      <td>2050</td>
      <td>2310</td>
    </tr>
    <tr>
      <th>48919</th>
      <td>Togo</td>
      <td>2050</td>
      <td>4690</td>
    </tr>
    <tr>
      <th>48920</th>
      <td>Thailand</td>
      <td>2050</td>
      <td>36.1k</td>
    </tr>
    <tr>
      <th>48921</th>
      <td>Tajikistan</td>
      <td>2050</td>
      <td>7240</td>
    </tr>
    <tr>
      <th>48922</th>
      <td>Turkmenistan</td>
      <td>2050</td>
      <td>24.5k</td>
    </tr>
    <tr>
      <th>48923</th>
      <td>Timor-Leste</td>
      <td>2050</td>
      <td>4600</td>
    </tr>
    <tr>
      <th>48924</th>
      <td>Tonga</td>
      <td>2050</td>
      <td>11.5k</td>
    </tr>
    <tr>
      <th>48925</th>
      <td>Trinidad and Tobago</td>
      <td>2050</td>
      <td>40.6k</td>
    </tr>
    <tr>
      <th>48926</th>
      <td>Tunisia</td>
      <td>2050</td>
      <td>16.4k</td>
    </tr>
    <tr>
      <th>48927</th>
      <td>Turkey</td>
      <td>2050</td>
      <td>58.1k</td>
    </tr>
    <tr>
      <th>48928</th>
      <td>Tuvalu</td>
      <td>2050</td>
      <td>8960</td>
    </tr>
    <tr>
      <th>48929</th>
      <td>Taiwan</td>
      <td>2050</td>
      <td>112k</td>
    </tr>
    <tr>
      <th>48930</th>
      <td>Tanzania</td>
      <td>2050</td>
      <td>5390</td>
    </tr>
    <tr>
      <th>48931</th>
      <td>Uganda</td>
      <td>2050</td>
      <td>4150</td>
    </tr>
    <tr>
      <th>48932</th>
      <td>Ukraine</td>
      <td>2050</td>
      <td>28.1k</td>
    </tr>
    <tr>
      <th>48933</th>
      <td>Uruguay</td>
      <td>2050</td>
      <td>41.8k</td>
    </tr>
    <tr>
      <th>48934</th>
      <td>United States</td>
      <td>2050</td>
      <td>110k</td>
    </tr>
    <tr>
      <th>48935</th>
      <td>Uzbekistan</td>
      <td>2050</td>
      <td>15.7k</td>
    </tr>
    <tr>
      <th>48936</th>
      <td>St. Vincent and the Grenadines</td>
      <td>2050</td>
      <td>24.2k</td>
    </tr>
    <tr>
      <th>48937</th>
      <td>Venezuela</td>
      <td>2050</td>
      <td>2070</td>
    </tr>
    <tr>
      <th>48938</th>
      <td>Vietnam</td>
      <td>2050</td>
      <td>22.1k</td>
    </tr>
    <tr>
      <th>48939</th>
      <td>Vanuatu</td>
      <td>2050</td>
      <td>4040</td>
    </tr>
    <tr>
      <th>48940</th>
      <td>Samoa</td>
      <td>2050</td>
      <td>10.7k</td>
    </tr>
    <tr>
      <th>48941</th>
      <td>Yemen</td>
      <td>2050</td>
      <td>4540</td>
    </tr>
    <tr>
      <th>48942</th>
      <td>South Africa</td>
      <td>2050</td>
      <td>19.7k</td>
    </tr>
    <tr>
      <th>48943</th>
      <td>Zambia</td>
      <td>2050</td>
      <td>5680</td>
    </tr>
    <tr>
      <th>48944</th>
      <td>Zimbabwe</td>
      <td>2050</td>
      <td>5920</td>
    </tr>
  </tbody>
</table>
<p>48945 rows Ã— 3 columns</p>
</div>




```python
# convert years from being a row into a column and giving it a column name year - fertility data, and check changes
df_fert = pd.melt(df_fert, id_vars=['country'], var_name="year", value_vars=df_fert.columns[1:], value_name= "child_per_woman")
df_fert
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
      <th>country</th>
      <th>year</th>
      <th>child_per_woman</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Aruba</td>
      <td>1800</td>
      <td>5.64</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Afghanistan</td>
      <td>1800</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Angola</td>
      <td>1800</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Albania</td>
      <td>1800</td>
      <td>4.60</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Netherlands Antilles</td>
      <td>1800</td>
      <td>5.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>United Arab Emirates</td>
      <td>1800</td>
      <td>6.94</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Argentina</td>
      <td>1800</td>
      <td>6.80</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Armenia</td>
      <td>1800</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Antigua and Barbuda</td>
      <td>1800</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Australia</td>
      <td>1800</td>
      <td>6.50</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Austria</td>
      <td>1800</td>
      <td>5.10</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Azerbaijan</td>
      <td>1800</td>
      <td>8.10</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Burundi</td>
      <td>1800</td>
      <td>6.80</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Belgium</td>
      <td>1800</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Benin</td>
      <td>1800</td>
      <td>5.55</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Burkina Faso</td>
      <td>1800</td>
      <td>6.03</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Bangladesh</td>
      <td>1800</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Bulgaria</td>
      <td>1800</td>
      <td>5.16</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Bahrain</td>
      <td>1800</td>
      <td>7.03</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Bahamas</td>
      <td>1800</td>
      <td>5.90</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Bosnia and Herzegovina</td>
      <td>1800</td>
      <td>5.91</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Belarus</td>
      <td>1800</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Belize</td>
      <td>1800</td>
      <td>6.69</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Bolivia</td>
      <td>1800</td>
      <td>6.48</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Brazil</td>
      <td>1800</td>
      <td>6.26</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Barbados</td>
      <td>1800</td>
      <td>4.96</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Brunei</td>
      <td>1800</td>
      <td>7.06</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Bhutan</td>
      <td>1800</td>
      <td>6.67</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Botswana</td>
      <td>1800</td>
      <td>6.47</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Central African Republic</td>
      <td>1800</td>
      <td>6.51</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>60772</th>
      <td>Eswatini</td>
      <td>2100</td>
      <td>1.78</td>
    </tr>
    <tr>
      <th>60773</th>
      <td>Seychelles</td>
      <td>2100</td>
      <td>1.83</td>
    </tr>
    <tr>
      <th>60774</th>
      <td>Syria</td>
      <td>2100</td>
      <td>1.77</td>
    </tr>
    <tr>
      <th>60775</th>
      <td>Chad</td>
      <td>2100</td>
      <td>2.11</td>
    </tr>
    <tr>
      <th>60776</th>
      <td>Togo</td>
      <td>2100</td>
      <td>2.07</td>
    </tr>
    <tr>
      <th>60777</th>
      <td>Thailand</td>
      <td>2100</td>
      <td>1.77</td>
    </tr>
    <tr>
      <th>60778</th>
      <td>Tajikistan</td>
      <td>2100</td>
      <td>1.87</td>
    </tr>
    <tr>
      <th>60779</th>
      <td>Turkmenistan</td>
      <td>2100</td>
      <td>1.83</td>
    </tr>
    <tr>
      <th>60780</th>
      <td>Timor-Leste</td>
      <td>2100</td>
      <td>1.94</td>
    </tr>
    <tr>
      <th>60781</th>
      <td>Tonga</td>
      <td>2100</td>
      <td>1.99</td>
    </tr>
    <tr>
      <th>60782</th>
      <td>Trinidad and Tobago</td>
      <td>2100</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>60783</th>
      <td>Tunisia</td>
      <td>2100</td>
      <td>1.84</td>
    </tr>
    <tr>
      <th>60784</th>
      <td>Turkey</td>
      <td>2100</td>
      <td>1.78</td>
    </tr>
    <tr>
      <th>60785</th>
      <td>Taiwan</td>
      <td>2100</td>
      <td>1.76</td>
    </tr>
    <tr>
      <th>60786</th>
      <td>Tanzania</td>
      <td>2100</td>
      <td>2.32</td>
    </tr>
    <tr>
      <th>60787</th>
      <td>Uganda</td>
      <td>2100</td>
      <td>2.09</td>
    </tr>
    <tr>
      <th>60788</th>
      <td>Ukraine</td>
      <td>2100</td>
      <td>1.83</td>
    </tr>
    <tr>
      <th>60789</th>
      <td>Uruguay</td>
      <td>2100</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>60790</th>
      <td>United States</td>
      <td>2100</td>
      <td>1.92</td>
    </tr>
    <tr>
      <th>60791</th>
      <td>Uzbekistan</td>
      <td>2100</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>60792</th>
      <td>St. Vincent and the Grenadines</td>
      <td>2100</td>
      <td>1.78</td>
    </tr>
    <tr>
      <th>60793</th>
      <td>Venezuela</td>
      <td>2100</td>
      <td>1.79</td>
    </tr>
    <tr>
      <th>60794</th>
      <td>Virgin Islands (U.S.)</td>
      <td>2100</td>
      <td>1.82</td>
    </tr>
    <tr>
      <th>60795</th>
      <td>Vietnam</td>
      <td>2100</td>
      <td>1.89</td>
    </tr>
    <tr>
      <th>60796</th>
      <td>Vanuatu</td>
      <td>2100</td>
      <td>1.89</td>
    </tr>
    <tr>
      <th>60797</th>
      <td>Samoa</td>
      <td>2100</td>
      <td>2.02</td>
    </tr>
    <tr>
      <th>60798</th>
      <td>Yemen</td>
      <td>2100</td>
      <td>1.70</td>
    </tr>
    <tr>
      <th>60799</th>
      <td>South Africa</td>
      <td>2100</td>
      <td>1.80</td>
    </tr>
    <tr>
      <th>60800</th>
      <td>Zambia</td>
      <td>2100</td>
      <td>2.46</td>
    </tr>
    <tr>
      <th>60801</th>
      <td>Zimbabwe</td>
      <td>2100</td>
      <td>1.83</td>
    </tr>
  </tbody>
</table>
<p>60802 rows Ã— 3 columns</p>
</div>




```python
# convert years from being a row into a column and giving it a column name year - life expectancy data, and check changes
df_life = pd.melt(df_life, id_vars=['country'], var_name="year", value_vars=df_life.columns[1:], value_name= "life_expectancy")
df_life
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
      <th>country</th>
      <th>year</th>
      <th>life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1800</td>
      <td>28.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>1800</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>1800</td>
      <td>35.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>1800</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>4</th>
      <td>United Arab Emirates</td>
      <td>1800</td>
      <td>30.7</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Argentina</td>
      <td>1800</td>
      <td>33.2</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Armenia</td>
      <td>1800</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Antigua and Barbuda</td>
      <td>1800</td>
      <td>33.5</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Australia</td>
      <td>1800</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Austria</td>
      <td>1800</td>
      <td>34.4</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Azerbaijan</td>
      <td>1800</td>
      <td>29.2</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Burundi</td>
      <td>1800</td>
      <td>31.5</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Belgium</td>
      <td>1800</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Benin</td>
      <td>1800</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burkina Faso</td>
      <td>1800</td>
      <td>29.2</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Bangladesh</td>
      <td>1800</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Bulgaria</td>
      <td>1800</td>
      <td>35.8</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Bahrain</td>
      <td>1800</td>
      <td>30.3</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Bahamas</td>
      <td>1800</td>
      <td>35.2</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Bosnia and Herzegovina</td>
      <td>1800</td>
      <td>35.1</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Belarus</td>
      <td>1800</td>
      <td>36.2</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Belize</td>
      <td>1800</td>
      <td>26.5</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Bolivia</td>
      <td>1800</td>
      <td>33.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Brazil</td>
      <td>1800</td>
      <td>32.0</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Barbados</td>
      <td>1800</td>
      <td>32.1</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Brunei</td>
      <td>1800</td>
      <td>29.2</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Bhutan</td>
      <td>1800</td>
      <td>28.8</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Botswana</td>
      <td>1800</td>
      <td>33.6</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Central African Republic</td>
      <td>1800</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Canada</td>
      <td>1800</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>58665</th>
      <td>Eswatini</td>
      <td>2100</td>
      <td>71.8</td>
    </tr>
    <tr>
      <th>58666</th>
      <td>Seychelles</td>
      <td>2100</td>
      <td>84.8</td>
    </tr>
    <tr>
      <th>58667</th>
      <td>Syria</td>
      <td>2100</td>
      <td>87.9</td>
    </tr>
    <tr>
      <th>58668</th>
      <td>Chad</td>
      <td>2100</td>
      <td>77.6</td>
    </tr>
    <tr>
      <th>58669</th>
      <td>Togo</td>
      <td>2100</td>
      <td>79.1</td>
    </tr>
    <tr>
      <th>58670</th>
      <td>Thailand</td>
      <td>2100</td>
      <td>89.8</td>
    </tr>
    <tr>
      <th>58671</th>
      <td>Tajikistan</td>
      <td>2100</td>
      <td>81.3</td>
    </tr>
    <tr>
      <th>58672</th>
      <td>Turkmenistan</td>
      <td>2100</td>
      <td>81.3</td>
    </tr>
    <tr>
      <th>58673</th>
      <td>Timor-Leste</td>
      <td>2100</td>
      <td>82.4</td>
    </tr>
    <tr>
      <th>58674</th>
      <td>Tonga</td>
      <td>2100</td>
      <td>82.7</td>
    </tr>
    <tr>
      <th>58675</th>
      <td>Trinidad and Tobago</td>
      <td>2100</td>
      <td>85.6</td>
    </tr>
    <tr>
      <th>58676</th>
      <td>Tunisia</td>
      <td>2100</td>
      <td>88.9</td>
    </tr>
    <tr>
      <th>58677</th>
      <td>Turkey</td>
      <td>2100</td>
      <td>90.5</td>
    </tr>
    <tr>
      <th>58678</th>
      <td>Tuvalu</td>
      <td>2100</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>58679</th>
      <td>Taiwan</td>
      <td>2100</td>
      <td>90.5</td>
    </tr>
    <tr>
      <th>58680</th>
      <td>Tanzania</td>
      <td>2100</td>
      <td>82.0</td>
    </tr>
    <tr>
      <th>58681</th>
      <td>Uganda</td>
      <td>2100</td>
      <td>81.8</td>
    </tr>
    <tr>
      <th>58682</th>
      <td>Ukraine</td>
      <td>2100</td>
      <td>85.1</td>
    </tr>
    <tr>
      <th>58683</th>
      <td>Uruguay</td>
      <td>2100</td>
      <td>87.8</td>
    </tr>
    <tr>
      <th>58684</th>
      <td>United States</td>
      <td>2100</td>
      <td>88.9</td>
    </tr>
    <tr>
      <th>58685</th>
      <td>Uzbekistan</td>
      <td>2100</td>
      <td>77.5</td>
    </tr>
    <tr>
      <th>58686</th>
      <td>St. Vincent and the Grenadines</td>
      <td>2100</td>
      <td>83.5</td>
    </tr>
    <tr>
      <th>58687</th>
      <td>Venezuela</td>
      <td>2100</td>
      <td>87.3</td>
    </tr>
    <tr>
      <th>58688</th>
      <td>Vietnam</td>
      <td>2100</td>
      <td>85.0</td>
    </tr>
    <tr>
      <th>58689</th>
      <td>Vanuatu</td>
      <td>2100</td>
      <td>75.1</td>
    </tr>
    <tr>
      <th>58690</th>
      <td>Samoa</td>
      <td>2100</td>
      <td>80.8</td>
    </tr>
    <tr>
      <th>58691</th>
      <td>Yemen</td>
      <td>2100</td>
      <td>78.0</td>
    </tr>
    <tr>
      <th>58692</th>
      <td>South Africa</td>
      <td>2100</td>
      <td>77.7</td>
    </tr>
    <tr>
      <th>58693</th>
      <td>Zambia</td>
      <td>2100</td>
      <td>77.1</td>
    </tr>
    <tr>
      <th>58694</th>
      <td>Zimbabwe</td>
      <td>2100</td>
      <td>74.4</td>
    </tr>
  </tbody>
</table>
<p>58695 rows Ã— 3 columns</p>
</div>




```python
# merge data of population and income into a single dataframe, and show the dataframe 
df = pd.merge(df_pop, df_inc, on = ['country', 'year'])
df
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>income</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1800</td>
      <td>3.28M</td>
      <td>683</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>1800</td>
      <td>1.57M</td>
      <td>700</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>1800</td>
      <td>400k</td>
      <td>755</td>
    </tr>
    <tr>
      <th>3</th>
      <td>Andorra</td>
      <td>1800</td>
      <td>2650</td>
      <td>1360</td>
    </tr>
    <tr>
      <th>4</th>
      <td>United Arab Emirates</td>
      <td>1800</td>
      <td>40.2k</td>
      <td>1130</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Argentina</td>
      <td>1800</td>
      <td>534k</td>
      <td>1730</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Armenia</td>
      <td>1800</td>
      <td>413k</td>
      <td>582</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Antigua and Barbuda</td>
      <td>1800</td>
      <td>37k</td>
      <td>857</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Australia</td>
      <td>1800</td>
      <td>200k</td>
      <td>925</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Austria</td>
      <td>1800</td>
      <td>3M</td>
      <td>2090</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Azerbaijan</td>
      <td>1800</td>
      <td>880k</td>
      <td>877</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Burundi</td>
      <td>1800</td>
      <td>899k</td>
      <td>473</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Belgium</td>
      <td>1800</td>
      <td>3.25M</td>
      <td>2700</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Benin</td>
      <td>1800</td>
      <td>637k</td>
      <td>676</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Burkina Faso</td>
      <td>1800</td>
      <td>1.67M</td>
      <td>543</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Bangladesh</td>
      <td>1800</td>
      <td>19.2M</td>
      <td>992</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Bulgaria</td>
      <td>1800</td>
      <td>2.25M</td>
      <td>1230</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Bahrain</td>
      <td>1800</td>
      <td>64.5k</td>
      <td>1400</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Bahamas</td>
      <td>1800</td>
      <td>27.4k</td>
      <td>1640</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Bosnia and Herzegovina</td>
      <td>1800</td>
      <td>852k</td>
      <td>757</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Belarus</td>
      <td>1800</td>
      <td>2.36M</td>
      <td>688</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Belize</td>
      <td>1800</td>
      <td>25.5k</td>
      <td>655</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Bolivia</td>
      <td>1800</td>
      <td>887k</td>
      <td>967</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Brazil</td>
      <td>1800</td>
      <td>2.5M</td>
      <td>1010</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Barbados</td>
      <td>1800</td>
      <td>81.7k</td>
      <td>1030</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Brunei</td>
      <td>1800</td>
      <td>2260</td>
      <td>1710</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Bhutan</td>
      <td>1800</td>
      <td>392k</td>
      <td>712</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Botswana</td>
      <td>1800</td>
      <td>121k</td>
      <td>449</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Central African Republic</td>
      <td>1800</td>
      <td>479k</td>
      <td>480</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Canada</td>
      <td>1800</td>
      <td>500k</td>
      <td>1490</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>48915</th>
      <td>Eswatini</td>
      <td>2050</td>
      <td>1.7M</td>
      <td>14.4k</td>
    </tr>
    <tr>
      <th>48916</th>
      <td>Seychelles</td>
      <td>2050</td>
      <td>105k</td>
      <td>58.4k</td>
    </tr>
    <tr>
      <th>48917</th>
      <td>Syria</td>
      <td>2050</td>
      <td>33.1M</td>
      <td>7110</td>
    </tr>
    <tr>
      <th>48918</th>
      <td>Chad</td>
      <td>2050</td>
      <td>34M</td>
      <td>2310</td>
    </tr>
    <tr>
      <th>48919</th>
      <td>Togo</td>
      <td>2050</td>
      <td>15.4M</td>
      <td>4690</td>
    </tr>
    <tr>
      <th>48920</th>
      <td>Thailand</td>
      <td>2050</td>
      <td>65.9M</td>
      <td>36.1k</td>
    </tr>
    <tr>
      <th>48921</th>
      <td>Tajikistan</td>
      <td>2050</td>
      <td>16.2M</td>
      <td>7240</td>
    </tr>
    <tr>
      <th>48922</th>
      <td>Turkmenistan</td>
      <td>2050</td>
      <td>7.95M</td>
      <td>24.5k</td>
    </tr>
    <tr>
      <th>48923</th>
      <td>Timor-Leste</td>
      <td>2050</td>
      <td>2.02M</td>
      <td>4600</td>
    </tr>
    <tr>
      <th>48924</th>
      <td>Tonga</td>
      <td>2050</td>
      <td>134k</td>
      <td>11.5k</td>
    </tr>
    <tr>
      <th>48925</th>
      <td>Trinidad and Tobago</td>
      <td>2050</td>
      <td>1.34M</td>
      <td>40.6k</td>
    </tr>
    <tr>
      <th>48926</th>
      <td>Tunisia</td>
      <td>2050</td>
      <td>13.8M</td>
      <td>16.4k</td>
    </tr>
    <tr>
      <th>48927</th>
      <td>Turkey</td>
      <td>2050</td>
      <td>97.1M</td>
      <td>58.1k</td>
    </tr>
    <tr>
      <th>48928</th>
      <td>Tuvalu</td>
      <td>2050</td>
      <td>16k</td>
      <td>8960</td>
    </tr>
    <tr>
      <th>48929</th>
      <td>Taiwan</td>
      <td>2050</td>
      <td>22.4M</td>
      <td>112k</td>
    </tr>
    <tr>
      <th>48930</th>
      <td>Tanzania</td>
      <td>2050</td>
      <td>129M</td>
      <td>5390</td>
    </tr>
    <tr>
      <th>48931</th>
      <td>Uganda</td>
      <td>2050</td>
      <td>89.4M</td>
      <td>4150</td>
    </tr>
    <tr>
      <th>48932</th>
      <td>Ukraine</td>
      <td>2050</td>
      <td>35.2M</td>
      <td>28.1k</td>
    </tr>
    <tr>
      <th>48933</th>
      <td>Uruguay</td>
      <td>2050</td>
      <td>3.64M</td>
      <td>41.8k</td>
    </tr>
    <tr>
      <th>48934</th>
      <td>United States</td>
      <td>2050</td>
      <td>379M</td>
      <td>110k</td>
    </tr>
    <tr>
      <th>48935</th>
      <td>Uzbekistan</td>
      <td>2050</td>
      <td>42.9M</td>
      <td>15.7k</td>
    </tr>
    <tr>
      <th>48936</th>
      <td>St. Vincent and the Grenadines</td>
      <td>2050</td>
      <td>109k</td>
      <td>24.2k</td>
    </tr>
    <tr>
      <th>48937</th>
      <td>Venezuela</td>
      <td>2050</td>
      <td>37M</td>
      <td>2070</td>
    </tr>
    <tr>
      <th>48938</th>
      <td>Vietnam</td>
      <td>2050</td>
      <td>110M</td>
      <td>22.1k</td>
    </tr>
    <tr>
      <th>48939</th>
      <td>Vanuatu</td>
      <td>2050</td>
      <td>557k</td>
      <td>4040</td>
    </tr>
    <tr>
      <th>48940</th>
      <td>Samoa</td>
      <td>2050</td>
      <td>267k</td>
      <td>10.7k</td>
    </tr>
    <tr>
      <th>48941</th>
      <td>Yemen</td>
      <td>2050</td>
      <td>48.1M</td>
      <td>4540</td>
    </tr>
    <tr>
      <th>48942</th>
      <td>South Africa</td>
      <td>2050</td>
      <td>75.5M</td>
      <td>19.7k</td>
    </tr>
    <tr>
      <th>48943</th>
      <td>Zambia</td>
      <td>2050</td>
      <td>39.1M</td>
      <td>5680</td>
    </tr>
    <tr>
      <th>48944</th>
      <td>Zimbabwe</td>
      <td>2050</td>
      <td>23.9M</td>
      <td>5920</td>
    </tr>
  </tbody>
</table>
<p>48945 rows Ã— 4 columns</p>
</div>




```python
# merge the fertility data into the dataframa we prviously created, and show the dataframe after merge
df = pd.merge(df, df_fert, on = ['country', 'year'])
df
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>income</th>
      <th>child_per_woman</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1800</td>
      <td>3.28M</td>
      <td>683</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>1800</td>
      <td>1.57M</td>
      <td>700</td>
      <td>6.93</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>1800</td>
      <td>400k</td>
      <td>755</td>
      <td>4.60</td>
    </tr>
    <tr>
      <th>3</th>
      <td>United Arab Emirates</td>
      <td>1800</td>
      <td>40.2k</td>
      <td>1130</td>
      <td>6.94</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Argentina</td>
      <td>1800</td>
      <td>534k</td>
      <td>1730</td>
      <td>6.80</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Armenia</td>
      <td>1800</td>
      <td>413k</td>
      <td>582</td>
      <td>7.80</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Antigua and Barbuda</td>
      <td>1800</td>
      <td>37k</td>
      <td>857</td>
      <td>5.00</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Australia</td>
      <td>1800</td>
      <td>200k</td>
      <td>925</td>
      <td>6.50</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Austria</td>
      <td>1800</td>
      <td>3M</td>
      <td>2090</td>
      <td>5.10</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Azerbaijan</td>
      <td>1800</td>
      <td>880k</td>
      <td>877</td>
      <td>8.10</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Burundi</td>
      <td>1800</td>
      <td>899k</td>
      <td>473</td>
      <td>6.80</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Belgium</td>
      <td>1800</td>
      <td>3.25M</td>
      <td>2700</td>
      <td>4.85</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Benin</td>
      <td>1800</td>
      <td>637k</td>
      <td>676</td>
      <td>5.55</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Burkina Faso</td>
      <td>1800</td>
      <td>1.67M</td>
      <td>543</td>
      <td>6.03</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Bangladesh</td>
      <td>1800</td>
      <td>19.2M</td>
      <td>992</td>
      <td>6.70</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Bulgaria</td>
      <td>1800</td>
      <td>2.25M</td>
      <td>1230</td>
      <td>5.16</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Bahrain</td>
      <td>1800</td>
      <td>64.5k</td>
      <td>1400</td>
      <td>7.03</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Bahamas</td>
      <td>1800</td>
      <td>27.4k</td>
      <td>1640</td>
      <td>5.90</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Bosnia and Herzegovina</td>
      <td>1800</td>
      <td>852k</td>
      <td>757</td>
      <td>5.91</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Belarus</td>
      <td>1800</td>
      <td>2.36M</td>
      <td>688</td>
      <td>7.00</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Belize</td>
      <td>1800</td>
      <td>25.5k</td>
      <td>655</td>
      <td>6.69</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Bolivia</td>
      <td>1800</td>
      <td>887k</td>
      <td>967</td>
      <td>6.48</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Brazil</td>
      <td>1800</td>
      <td>2.5M</td>
      <td>1010</td>
      <td>6.26</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Barbados</td>
      <td>1800</td>
      <td>81.7k</td>
      <td>1030</td>
      <td>4.96</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Brunei</td>
      <td>1800</td>
      <td>2260</td>
      <td>1710</td>
      <td>7.06</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Bhutan</td>
      <td>1800</td>
      <td>392k</td>
      <td>712</td>
      <td>6.67</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Botswana</td>
      <td>1800</td>
      <td>121k</td>
      <td>449</td>
      <td>6.47</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Central African Republic</td>
      <td>1800</td>
      <td>479k</td>
      <td>480</td>
      <td>6.51</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Canada</td>
      <td>1800</td>
      <td>500k</td>
      <td>1490</td>
      <td>5.72</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Switzerland</td>
      <td>1800</td>
      <td>1.75M</td>
      <td>2770</td>
      <td>4.14</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>46656</th>
      <td>Sweden</td>
      <td>2050</td>
      <td>11.4M</td>
      <td>90.2k</td>
      <td>1.93</td>
    </tr>
    <tr>
      <th>46657</th>
      <td>Eswatini</td>
      <td>2050</td>
      <td>1.7M</td>
      <td>14.4k</td>
      <td>2.07</td>
    </tr>
    <tr>
      <th>46658</th>
      <td>Seychelles</td>
      <td>2050</td>
      <td>105k</td>
      <td>58.4k</td>
      <td>1.87</td>
    </tr>
    <tr>
      <th>46659</th>
      <td>Syria</td>
      <td>2050</td>
      <td>33.1M</td>
      <td>7110</td>
      <td>1.93</td>
    </tr>
    <tr>
      <th>46660</th>
      <td>Chad</td>
      <td>2050</td>
      <td>34M</td>
      <td>2310</td>
      <td>3.37</td>
    </tr>
    <tr>
      <th>46661</th>
      <td>Togo</td>
      <td>2050</td>
      <td>15.4M</td>
      <td>4690</td>
      <td>2.95</td>
    </tr>
    <tr>
      <th>46662</th>
      <td>Thailand</td>
      <td>2050</td>
      <td>65.9M</td>
      <td>36.1k</td>
      <td>1.61</td>
    </tr>
    <tr>
      <th>46663</th>
      <td>Tajikistan</td>
      <td>2050</td>
      <td>16.2M</td>
      <td>7240</td>
      <td>2.40</td>
    </tr>
    <tr>
      <th>46664</th>
      <td>Turkmenistan</td>
      <td>2050</td>
      <td>7.95M</td>
      <td>24.5k</td>
      <td>2.06</td>
    </tr>
    <tr>
      <th>46665</th>
      <td>Timor-Leste</td>
      <td>2050</td>
      <td>2.02M</td>
      <td>4600</td>
      <td>2.94</td>
    </tr>
    <tr>
      <th>46666</th>
      <td>Tonga</td>
      <td>2050</td>
      <td>134k</td>
      <td>11.5k</td>
      <td>2.67</td>
    </tr>
    <tr>
      <th>46667</th>
      <td>Trinidad and Tobago</td>
      <td>2050</td>
      <td>1.34M</td>
      <td>40.6k</td>
      <td>1.71</td>
    </tr>
    <tr>
      <th>46668</th>
      <td>Tunisia</td>
      <td>2050</td>
      <td>13.8M</td>
      <td>16.4k</td>
      <td>1.86</td>
    </tr>
    <tr>
      <th>46669</th>
      <td>Turkey</td>
      <td>2050</td>
      <td>97.1M</td>
      <td>58.1k</td>
      <td>1.75</td>
    </tr>
    <tr>
      <th>46670</th>
      <td>Taiwan</td>
      <td>2050</td>
      <td>22.4M</td>
      <td>112k</td>
      <td>1.57</td>
    </tr>
    <tr>
      <th>46671</th>
      <td>Tanzania</td>
      <td>2050</td>
      <td>129M</td>
      <td>5390</td>
      <td>3.35</td>
    </tr>
    <tr>
      <th>46672</th>
      <td>Uganda</td>
      <td>2050</td>
      <td>89.4M</td>
      <td>4150</td>
      <td>3.24</td>
    </tr>
    <tr>
      <th>46673</th>
      <td>Ukraine</td>
      <td>2050</td>
      <td>35.2M</td>
      <td>28.1k</td>
      <td>1.76</td>
    </tr>
    <tr>
      <th>46674</th>
      <td>Uruguay</td>
      <td>2050</td>
      <td>3.64M</td>
      <td>41.8k</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>46675</th>
      <td>United States</td>
      <td>2050</td>
      <td>379M</td>
      <td>110k</td>
      <td>1.91</td>
    </tr>
    <tr>
      <th>46676</th>
      <td>Uzbekistan</td>
      <td>2050</td>
      <td>42.9M</td>
      <td>15.7k</td>
      <td>1.81</td>
    </tr>
    <tr>
      <th>46677</th>
      <td>St. Vincent and the Grenadines</td>
      <td>2050</td>
      <td>109k</td>
      <td>24.2k</td>
      <td>1.69</td>
    </tr>
    <tr>
      <th>46678</th>
      <td>Venezuela</td>
      <td>2050</td>
      <td>37M</td>
      <td>2070</td>
      <td>1.83</td>
    </tr>
    <tr>
      <th>46679</th>
      <td>Vietnam</td>
      <td>2050</td>
      <td>110M</td>
      <td>22.1k</td>
      <td>1.90</td>
    </tr>
    <tr>
      <th>46680</th>
      <td>Vanuatu</td>
      <td>2050</td>
      <td>557k</td>
      <td>4040</td>
      <td>2.42</td>
    </tr>
    <tr>
      <th>46681</th>
      <td>Samoa</td>
      <td>2050</td>
      <td>267k</td>
      <td>10.7k</td>
      <td>2.81</td>
    </tr>
    <tr>
      <th>46682</th>
      <td>Yemen</td>
      <td>2050</td>
      <td>48.1M</td>
      <td>4540</td>
      <td>2.11</td>
    </tr>
    <tr>
      <th>46683</th>
      <td>South Africa</td>
      <td>2050</td>
      <td>75.5M</td>
      <td>19.7k</td>
      <td>1.91</td>
    </tr>
    <tr>
      <th>46684</th>
      <td>Zambia</td>
      <td>2050</td>
      <td>39.1M</td>
      <td>5680</td>
      <td>3.48</td>
    </tr>
    <tr>
      <th>46685</th>
      <td>Zimbabwe</td>
      <td>2050</td>
      <td>23.9M</td>
      <td>5920</td>
      <td>2.35</td>
    </tr>
  </tbody>
</table>
<p>46686 rows Ã— 5 columns</p>
</div>




```python
# merge the life expectancy data into the dataframa we prviously created, and show the dataframe after merge
df = pd.merge(df, df_life, on = ['country', 'year'])
df
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>income</th>
      <th>child_per_woman</th>
      <th>life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>Afghanistan</td>
      <td>1800</td>
      <td>3.28M</td>
      <td>683</td>
      <td>7.00</td>
      <td>28.2</td>
    </tr>
    <tr>
      <th>1</th>
      <td>Angola</td>
      <td>1800</td>
      <td>1.57M</td>
      <td>700</td>
      <td>6.93</td>
      <td>27.0</td>
    </tr>
    <tr>
      <th>2</th>
      <td>Albania</td>
      <td>1800</td>
      <td>400k</td>
      <td>755</td>
      <td>4.60</td>
      <td>35.4</td>
    </tr>
    <tr>
      <th>3</th>
      <td>United Arab Emirates</td>
      <td>1800</td>
      <td>40.2k</td>
      <td>1130</td>
      <td>6.94</td>
      <td>30.7</td>
    </tr>
    <tr>
      <th>4</th>
      <td>Argentina</td>
      <td>1800</td>
      <td>534k</td>
      <td>1730</td>
      <td>6.80</td>
      <td>33.2</td>
    </tr>
    <tr>
      <th>5</th>
      <td>Armenia</td>
      <td>1800</td>
      <td>413k</td>
      <td>582</td>
      <td>7.80</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>6</th>
      <td>Antigua and Barbuda</td>
      <td>1800</td>
      <td>37k</td>
      <td>857</td>
      <td>5.00</td>
      <td>33.5</td>
    </tr>
    <tr>
      <th>7</th>
      <td>Australia</td>
      <td>1800</td>
      <td>200k</td>
      <td>925</td>
      <td>6.50</td>
      <td>34.0</td>
    </tr>
    <tr>
      <th>8</th>
      <td>Austria</td>
      <td>1800</td>
      <td>3M</td>
      <td>2090</td>
      <td>5.10</td>
      <td>34.4</td>
    </tr>
    <tr>
      <th>9</th>
      <td>Azerbaijan</td>
      <td>1800</td>
      <td>880k</td>
      <td>877</td>
      <td>8.10</td>
      <td>29.2</td>
    </tr>
    <tr>
      <th>10</th>
      <td>Burundi</td>
      <td>1800</td>
      <td>899k</td>
      <td>473</td>
      <td>6.80</td>
      <td>31.5</td>
    </tr>
    <tr>
      <th>11</th>
      <td>Belgium</td>
      <td>1800</td>
      <td>3.25M</td>
      <td>2700</td>
      <td>4.85</td>
      <td>40.0</td>
    </tr>
    <tr>
      <th>12</th>
      <td>Benin</td>
      <td>1800</td>
      <td>637k</td>
      <td>676</td>
      <td>5.55</td>
      <td>31.0</td>
    </tr>
    <tr>
      <th>13</th>
      <td>Burkina Faso</td>
      <td>1800</td>
      <td>1.67M</td>
      <td>543</td>
      <td>6.03</td>
      <td>29.2</td>
    </tr>
    <tr>
      <th>14</th>
      <td>Bangladesh</td>
      <td>1800</td>
      <td>19.2M</td>
      <td>992</td>
      <td>6.70</td>
      <td>25.5</td>
    </tr>
    <tr>
      <th>15</th>
      <td>Bulgaria</td>
      <td>1800</td>
      <td>2.25M</td>
      <td>1230</td>
      <td>5.16</td>
      <td>35.8</td>
    </tr>
    <tr>
      <th>16</th>
      <td>Bahrain</td>
      <td>1800</td>
      <td>64.5k</td>
      <td>1400</td>
      <td>7.03</td>
      <td>30.3</td>
    </tr>
    <tr>
      <th>17</th>
      <td>Bahamas</td>
      <td>1800</td>
      <td>27.4k</td>
      <td>1640</td>
      <td>5.90</td>
      <td>35.2</td>
    </tr>
    <tr>
      <th>18</th>
      <td>Bosnia and Herzegovina</td>
      <td>1800</td>
      <td>852k</td>
      <td>757</td>
      <td>5.91</td>
      <td>35.1</td>
    </tr>
    <tr>
      <th>19</th>
      <td>Belarus</td>
      <td>1800</td>
      <td>2.36M</td>
      <td>688</td>
      <td>7.00</td>
      <td>36.2</td>
    </tr>
    <tr>
      <th>20</th>
      <td>Belize</td>
      <td>1800</td>
      <td>25.5k</td>
      <td>655</td>
      <td>6.69</td>
      <td>26.5</td>
    </tr>
    <tr>
      <th>21</th>
      <td>Bolivia</td>
      <td>1800</td>
      <td>887k</td>
      <td>967</td>
      <td>6.48</td>
      <td>33.0</td>
    </tr>
    <tr>
      <th>22</th>
      <td>Brazil</td>
      <td>1800</td>
      <td>2.5M</td>
      <td>1010</td>
      <td>6.26</td>
      <td>32.0</td>
    </tr>
    <tr>
      <th>23</th>
      <td>Barbados</td>
      <td>1800</td>
      <td>81.7k</td>
      <td>1030</td>
      <td>4.96</td>
      <td>32.1</td>
    </tr>
    <tr>
      <th>24</th>
      <td>Brunei</td>
      <td>1800</td>
      <td>2260</td>
      <td>1710</td>
      <td>7.06</td>
      <td>29.2</td>
    </tr>
    <tr>
      <th>25</th>
      <td>Bhutan</td>
      <td>1800</td>
      <td>392k</td>
      <td>712</td>
      <td>6.67</td>
      <td>28.8</td>
    </tr>
    <tr>
      <th>26</th>
      <td>Botswana</td>
      <td>1800</td>
      <td>121k</td>
      <td>449</td>
      <td>6.47</td>
      <td>33.6</td>
    </tr>
    <tr>
      <th>27</th>
      <td>Central African Republic</td>
      <td>1800</td>
      <td>479k</td>
      <td>480</td>
      <td>6.51</td>
      <td>30.0</td>
    </tr>
    <tr>
      <th>28</th>
      <td>Canada</td>
      <td>1800</td>
      <td>500k</td>
      <td>1490</td>
      <td>5.72</td>
      <td>39.0</td>
    </tr>
    <tr>
      <th>29</th>
      <td>Switzerland</td>
      <td>1800</td>
      <td>1.75M</td>
      <td>2770</td>
      <td>4.14</td>
      <td>38.0</td>
    </tr>
    <tr>
      <th>...</th>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
      <td>...</td>
    </tr>
    <tr>
      <th>46656</th>
      <td>Sweden</td>
      <td>2050</td>
      <td>11.4M</td>
      <td>90.2k</td>
      <td>1.93</td>
      <td>86.7</td>
    </tr>
    <tr>
      <th>46657</th>
      <td>Eswatini</td>
      <td>2050</td>
      <td>1.7M</td>
      <td>14.4k</td>
      <td>2.07</td>
      <td>65.5</td>
    </tr>
    <tr>
      <th>46658</th>
      <td>Seychelles</td>
      <td>2050</td>
      <td>105k</td>
      <td>58.4k</td>
      <td>1.87</td>
      <td>77.9</td>
    </tr>
    <tr>
      <th>46659</th>
      <td>Syria</td>
      <td>2050</td>
      <td>33.1M</td>
      <td>7110</td>
      <td>1.93</td>
      <td>82.3</td>
    </tr>
    <tr>
      <th>46660</th>
      <td>Chad</td>
      <td>2050</td>
      <td>34M</td>
      <td>2310</td>
      <td>3.37</td>
      <td>69.0</td>
    </tr>
    <tr>
      <th>46661</th>
      <td>Togo</td>
      <td>2050</td>
      <td>15.4M</td>
      <td>4690</td>
      <td>2.95</td>
      <td>72.2</td>
    </tr>
    <tr>
      <th>46662</th>
      <td>Thailand</td>
      <td>2050</td>
      <td>65.9M</td>
      <td>36.1k</td>
      <td>1.61</td>
      <td>83.8</td>
    </tr>
    <tr>
      <th>46663</th>
      <td>Tajikistan</td>
      <td>2050</td>
      <td>16.2M</td>
      <td>7240</td>
      <td>2.40</td>
      <td>74.6</td>
    </tr>
    <tr>
      <th>46664</th>
      <td>Turkmenistan</td>
      <td>2050</td>
      <td>7.95M</td>
      <td>24.5k</td>
      <td>2.06</td>
      <td>74.6</td>
    </tr>
    <tr>
      <th>46665</th>
      <td>Timor-Leste</td>
      <td>2050</td>
      <td>2.02M</td>
      <td>4600</td>
      <td>2.94</td>
      <td>75.6</td>
    </tr>
    <tr>
      <th>46666</th>
      <td>Tonga</td>
      <td>2050</td>
      <td>134k</td>
      <td>11.5k</td>
      <td>2.67</td>
      <td>76.5</td>
    </tr>
    <tr>
      <th>46667</th>
      <td>Trinidad and Tobago</td>
      <td>2050</td>
      <td>1.34M</td>
      <td>40.6k</td>
      <td>1.71</td>
      <td>78.8</td>
    </tr>
    <tr>
      <th>46668</th>
      <td>Tunisia</td>
      <td>2050</td>
      <td>13.8M</td>
      <td>16.4k</td>
      <td>1.86</td>
      <td>83.0</td>
    </tr>
    <tr>
      <th>46669</th>
      <td>Turkey</td>
      <td>2050</td>
      <td>97.1M</td>
      <td>58.1k</td>
      <td>1.75</td>
      <td>84.5</td>
    </tr>
    <tr>
      <th>46670</th>
      <td>Taiwan</td>
      <td>2050</td>
      <td>22.4M</td>
      <td>112k</td>
      <td>1.57</td>
      <td>84.9</td>
    </tr>
    <tr>
      <th>46671</th>
      <td>Tanzania</td>
      <td>2050</td>
      <td>129M</td>
      <td>5390</td>
      <td>3.35</td>
      <td>74.3</td>
    </tr>
    <tr>
      <th>46672</th>
      <td>Uganda</td>
      <td>2050</td>
      <td>89.4M</td>
      <td>4150</td>
      <td>3.24</td>
      <td>74.0</td>
    </tr>
    <tr>
      <th>46673</th>
      <td>Ukraine</td>
      <td>2050</td>
      <td>35.2M</td>
      <td>28.1k</td>
      <td>1.76</td>
      <td>78.1</td>
    </tr>
    <tr>
      <th>46674</th>
      <td>Uruguay</td>
      <td>2050</td>
      <td>3.64M</td>
      <td>41.8k</td>
      <td>1.81</td>
      <td>82.1</td>
    </tr>
    <tr>
      <th>46675</th>
      <td>United States</td>
      <td>2050</td>
      <td>379M</td>
      <td>110k</td>
      <td>1.91</td>
      <td>83.5</td>
    </tr>
    <tr>
      <th>46676</th>
      <td>Uzbekistan</td>
      <td>2050</td>
      <td>42.9M</td>
      <td>15.7k</td>
      <td>1.81</td>
      <td>71.5</td>
    </tr>
    <tr>
      <th>46677</th>
      <td>St. Vincent and the Grenadines</td>
      <td>2050</td>
      <td>109k</td>
      <td>24.2k</td>
      <td>1.69</td>
      <td>76.9</td>
    </tr>
    <tr>
      <th>46678</th>
      <td>Venezuela</td>
      <td>2050</td>
      <td>37M</td>
      <td>2070</td>
      <td>1.83</td>
      <td>80.1</td>
    </tr>
    <tr>
      <th>46679</th>
      <td>Vietnam</td>
      <td>2050</td>
      <td>110M</td>
      <td>22.1k</td>
      <td>1.90</td>
      <td>78.8</td>
    </tr>
    <tr>
      <th>46680</th>
      <td>Vanuatu</td>
      <td>2050</td>
      <td>557k</td>
      <td>4040</td>
      <td>2.42</td>
      <td>69.2</td>
    </tr>
    <tr>
      <th>46681</th>
      <td>Samoa</td>
      <td>2050</td>
      <td>267k</td>
      <td>10.7k</td>
      <td>2.81</td>
      <td>74.3</td>
    </tr>
    <tr>
      <th>46682</th>
      <td>Yemen</td>
      <td>2050</td>
      <td>48.1M</td>
      <td>4540</td>
      <td>2.11</td>
      <td>72.2</td>
    </tr>
    <tr>
      <th>46683</th>
      <td>South Africa</td>
      <td>2050</td>
      <td>75.5M</td>
      <td>19.7k</td>
      <td>1.91</td>
      <td>70.9</td>
    </tr>
    <tr>
      <th>46684</th>
      <td>Zambia</td>
      <td>2050</td>
      <td>39.1M</td>
      <td>5680</td>
      <td>3.48</td>
      <td>69.8</td>
    </tr>
    <tr>
      <th>46685</th>
      <td>Zimbabwe</td>
      <td>2050</td>
      <td>23.9M</td>
      <td>5920</td>
      <td>2.35</td>
      <td>67.6</td>
    </tr>
  </tbody>
</table>
<p>46686 rows Ã— 6 columns</p>
</div>




```python
# find number of rows and columns
df.shape
```




    (46686, 6)




```python
# check if there are null values
df.info()
```

    <class 'pandas.core.frame.DataFrame'>
    Int64Index: 46686 entries, 0 to 46685
    Data columns (total 6 columns):
    country            46686 non-null object
    year               46686 non-null object
    population         46686 non-null object
    income             46686 non-null object
    child_per_woman    46686 non-null float64
    life_expectancy    46686 non-null float64
    dtypes: float64(2), object(4)
    memory usage: 2.5+ MB
    


```python
# show number of null values in each column
df.isnull().sum()
```




    country            0
    year               0
    population         0
    income             0
    child_per_woman    0
    life_expectancy    0
    dtype: int64




```python
# check data types
df.dtypes
```




    country             object
    year                object
    population          object
    income              object
    child_per_woman    float64
    life_expectancy    float64
    dtype: object




```python
# check for duplicates
sum(df.duplicated())
```




    0




### Data Cleaning
> **Tip**: Make sure that you keep your reader informed on the steps that you are taking in your investigation. Follow every code cell, or every set of related code cells, with a markdown cell to describe to the reader what was found in the preceding cell(s). Try to make it so that the reader can then understand what they will be seeing in the following cell(s).
 


```python
# change the data type of year column into int.
df.year = df.year.astype(int)
```


```python
# check changing the data type of year column
df.dtypes
```




    country             object
    year                 int64
    population          object
    income              object
    child_per_woman    float64
    life_expectancy    float64
    dtype: object



Now, we have changed the year column data type into int


```python
# trim the dataset to include years from 1980 till 2022 which is the period under investigation
df = df.query('year >= 1980 and year < 2022')
```


```python
# check the year column for changes made on it
df.year
```




    33480    1980
    33481    1980
    33482    1980
    33483    1980
    33484    1980
             ... 
    41287    2021
    41288    2021
    41289    2021
    41290    2021
    41291    2021
    Name: year, Length: 7812, dtype: int64



Thus, we successfully trimmed the dataset to include the years from 1980 till 2022!


```python
# check the number of rows after trimming
df.shape
```




    (7812, 6)




```python
# replace k, K, M, and B in population column with 1000, 1000000, 1000000000, and convert its type into float
df.population = df.population.replace(r'[kKMB]+$', '', regex=True).astype(float) * df.population.str.extract(r'[\d\.]+([KkMB]+)', expand=False).fillna(1).replace(['K', 'k', 'M', 'B'], [10**3,10**3, 10**6, 10**9]).astype(int)
```

    /opt/conda/lib/python3.6/site-packages/pandas/core/generic.py:5209: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self[name] = value
    


```python
# check that changes have took place
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>income</th>
      <th>child_per_woman</th>
      <th>life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33480</th>
      <td>Afghanistan</td>
      <td>1980</td>
      <td>13400000.0</td>
      <td>1190</td>
      <td>7.45</td>
      <td>43.7</td>
    </tr>
    <tr>
      <th>33481</th>
      <td>Angola</td>
      <td>1980</td>
      <td>8340000.0</td>
      <td>1780</td>
      <td>7.50</td>
      <td>48.1</td>
    </tr>
    <tr>
      <th>33482</th>
      <td>Albania</td>
      <td>1980</td>
      <td>2680000.0</td>
      <td>4470</td>
      <td>3.62</td>
      <td>71.3</td>
    </tr>
    <tr>
      <th>33483</th>
      <td>United Arab Emirates</td>
      <td>1980</td>
      <td>1020000.0</td>
      <td>93.8k</td>
      <td>5.51</td>
      <td>67.6</td>
    </tr>
    <tr>
      <th>33484</th>
      <td>Argentina</td>
      <td>1980</td>
      <td>27900000.0</td>
      <td>17.1k</td>
      <td>3.33</td>
      <td>70.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
df.dtypes
```




    country             object
    year                 int64
    population         float64
    income              object
    child_per_woman    float64
    life_expectancy    float64
    dtype: object



We successfully replaced the letters K, M, and B into the corresponding numbers and converted the column type into foat


```python
# for the income column If the value is a string, then remove k, K, M, or B with the corresponding value 1000, 1000000, or 1000000000 and convert its type into float
df.income = df.income.replace(r'[kKMB]+$', '', regex=True).astype(float) * df.income.str.extract(r'[\d\.]+([KkMB]+)', expand=False).fillna(1).replace(['K', 'k', 'M', 'B'], [10**3,10**3, 10**6, 10**9]).astype(int)
```

    /opt/conda/lib/python3.6/site-packages/pandas/core/generic.py:5209: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      self[name] = value
    


```python
# check that changes have took place
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>income</th>
      <th>child_per_woman</th>
      <th>life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33480</th>
      <td>Afghanistan</td>
      <td>1980</td>
      <td>13400000.0</td>
      <td>1190.0</td>
      <td>7.45</td>
      <td>43.7</td>
    </tr>
    <tr>
      <th>33481</th>
      <td>Angola</td>
      <td>1980</td>
      <td>8340000.0</td>
      <td>1780.0</td>
      <td>7.50</td>
      <td>48.1</td>
    </tr>
    <tr>
      <th>33482</th>
      <td>Albania</td>
      <td>1980</td>
      <td>2680000.0</td>
      <td>4470.0</td>
      <td>3.62</td>
      <td>71.3</td>
    </tr>
    <tr>
      <th>33483</th>
      <td>United Arab Emirates</td>
      <td>1980</td>
      <td>1020000.0</td>
      <td>93800.0</td>
      <td>5.51</td>
      <td>67.6</td>
    </tr>
    <tr>
      <th>33484</th>
      <td>Argentina</td>
      <td>1980</td>
      <td>27900000.0</td>
      <td>17100.0</td>
      <td>3.33</td>
      <td>70.2</td>
    </tr>
  </tbody>
</table>
</div>




```python
# check change of data type
df.dtypes
```




    country             object
    year                 int64
    population         float64
    income             float64
    child_per_woman    float64
    life_expectancy    float64
    dtype: object



We successfully replaced the letters K, M, and B into the corresponding numbers and converted the column type into foat


```python
# install of Python package pycountry to be able to get continent names from list of countries
!pip install pycountry_convert
```

    Requirement already satisfied: pycountry_convert in /opt/conda/lib/python3.6/site-packages (0.7.2)
    Requirement already satisfied: repoze.lru>=0.7 in /opt/conda/lib/python3.6/site-packages (from pycountry_convert) (0.7)
    Requirement already satisfied: pycountry>=16.11.27.1 in /opt/conda/lib/python3.6/site-packages (from pycountry_convert) (22.3.5)
    Requirement already satisfied: pytest-mock>=1.6.3 in /opt/conda/lib/python3.6/site-packages (from pycountry_convert) (3.6.1)
    Requirement already satisfied: pytest>=3.4.0 in /opt/conda/lib/python3.6/site-packages (from pycountry_convert) (4.5.0)
    Requirement already satisfied: pprintpp>=0.3.0 in /opt/conda/lib/python3.6/site-packages (from pycountry_convert) (0.4.0)
    Requirement already satisfied: wheel>=0.30.0 in /opt/conda/lib/python3.6/site-packages (from pycountry_convert) (0.30.0)
    Requirement already satisfied: pytest-cov>=2.5.1 in /opt/conda/lib/python3.6/site-packages (from pycountry_convert) (4.0.0)
    Requirement already satisfied: setuptools in /opt/conda/lib/python3.6/site-packages (from pycountry>=16.11.27.1->pycountry_convert) (38.4.0)
    Requirement already satisfied: more-itertools>=4.0.0; python_version > "2.7" in /opt/conda/lib/python3.6/site-packages (from pytest>=3.4.0->pycountry_convert) (7.0.0)
    Requirement already satisfied: attrs>=17.4.0 in /opt/conda/lib/python3.6/site-packages (from pytest>=3.4.0->pycountry_convert) (19.1.0)
    Requirement already satisfied: six>=1.10.0 in /opt/conda/lib/python3.6/site-packages (from pytest>=3.4.0->pycountry_convert) (1.11.0)
    Requirement already satisfied: pluggy!=0.10,<1.0,>=0.9 in /opt/conda/lib/python3.6/site-packages (from pytest>=3.4.0->pycountry_convert) (0.11.0)
    Requirement already satisfied: wcwidth in /opt/conda/lib/python3.6/site-packages (from pytest>=3.4.0->pycountry_convert) (0.1.7)
    Requirement already satisfied: atomicwrites>=1.0 in /opt/conda/lib/python3.6/site-packages (from pytest>=3.4.0->pycountry_convert) (1.3.0)
    Requirement already satisfied: py>=1.5.0 in /opt/conda/lib/python3.6/site-packages (from pytest>=3.4.0->pycountry_convert) (1.8.0)
    Requirement already satisfied: coverage[toml]>=5.2.1 in /opt/conda/lib/python3.6/site-packages (from pytest-cov>=2.5.1->pycountry_convert) (6.2)
    Requirement already satisfied: tomli; extra == "toml" in /opt/conda/lib/python3.6/site-packages (from coverage[toml]>=5.2.1->pytest-cov>=2.5.1->pycountry_convert) (1.2.3)
    


```python
# load the pycountry_convert package
import pycountry_convert as pc
```


```python
# create a new column named continent that contains the corresponding continent for each country
def country_to_continent(country_name):
    '''
    to get the continent name corresponding to the country in the row
    input = Spain
    Output = Europe
    '''
    try:
        country_alpha2 = pc.country_name_to_country_alpha2(country_name)
        country_continent_code = pc.country_alpha2_to_continent_code(country_alpha2)
        country_continent_name = pc.convert_continent_code_to_continent_name(country_continent_code)
        return country_continent_name
    except:
        return "None"

df['continent'] = df['country'].apply(country_to_continent)
```

    /opt/conda/lib/python3.6/site-packages/ipykernel_launcher.py:16: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame.
    Try using .loc[row_indexer,col_indexer] = value instead
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      app.launch_new_instance()
    


```python
# check the dataset with the new column 'continent'
df.head(50)
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>income</th>
      <th>child_per_woman</th>
      <th>life_expectancy</th>
      <th>continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33480</th>
      <td>Afghanistan</td>
      <td>1980</td>
      <td>1.340000e+07</td>
      <td>1190.0</td>
      <td>7.45</td>
      <td>43.7</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33481</th>
      <td>Angola</td>
      <td>1980</td>
      <td>8.340000e+06</td>
      <td>1780.0</td>
      <td>7.50</td>
      <td>48.1</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33482</th>
      <td>Albania</td>
      <td>1980</td>
      <td>2.680000e+06</td>
      <td>4470.0</td>
      <td>3.62</td>
      <td>71.3</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33483</th>
      <td>United Arab Emirates</td>
      <td>1980</td>
      <td>1.020000e+06</td>
      <td>93800.0</td>
      <td>5.51</td>
      <td>67.6</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33484</th>
      <td>Argentina</td>
      <td>1980</td>
      <td>2.790000e+07</td>
      <td>17100.0</td>
      <td>3.33</td>
      <td>70.2</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33485</th>
      <td>Armenia</td>
      <td>1980</td>
      <td>3.100000e+06</td>
      <td>6920.0</td>
      <td>2.39</td>
      <td>70.2</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33486</th>
      <td>Antigua and Barbuda</td>
      <td>1980</td>
      <td>6.190000e+04</td>
      <td>7910.0</td>
      <td>2.12</td>
      <td>72.1</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33487</th>
      <td>Australia</td>
      <td>1980</td>
      <td>1.460000e+07</td>
      <td>26300.0</td>
      <td>1.90</td>
      <td>74.5</td>
      <td>Oceania</td>
    </tr>
    <tr>
      <th>33488</th>
      <td>Austria</td>
      <td>1980</td>
      <td>7.610000e+06</td>
      <td>28900.0</td>
      <td>1.65</td>
      <td>72.8</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33489</th>
      <td>Azerbaijan</td>
      <td>1980</td>
      <td>6.150000e+06</td>
      <td>7700.0</td>
      <td>3.50</td>
      <td>66.2</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33490</th>
      <td>Burundi</td>
      <td>1980</td>
      <td>4.160000e+06</td>
      <td>1040.0</td>
      <td>7.42</td>
      <td>48.5</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33491</th>
      <td>Belgium</td>
      <td>1980</td>
      <td>9.870000e+06</td>
      <td>28800.0</td>
      <td>1.63</td>
      <td>73.3</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33492</th>
      <td>Benin</td>
      <td>1980</td>
      <td>3.720000e+06</td>
      <td>2010.0</td>
      <td>7.03</td>
      <td>52.7</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33493</th>
      <td>Burkina Faso</td>
      <td>1980</td>
      <td>6.820000e+06</td>
      <td>921.0</td>
      <td>7.13</td>
      <td>48.6</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33494</th>
      <td>Bangladesh</td>
      <td>1980</td>
      <td>7.960000e+07</td>
      <td>1220.0</td>
      <td>6.36</td>
      <td>53.2</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33495</th>
      <td>Bulgaria</td>
      <td>1980</td>
      <td>8.880000e+06</td>
      <td>12700.0</td>
      <td>2.11</td>
      <td>71.2</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33496</th>
      <td>Bahrain</td>
      <td>1980</td>
      <td>3.600000e+05</td>
      <td>42800.0</td>
      <td>4.92</td>
      <td>68.4</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33497</th>
      <td>Bahamas</td>
      <td>1980</td>
      <td>2.110000e+05</td>
      <td>32600.0</td>
      <td>2.99</td>
      <td>68.6</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33498</th>
      <td>Bosnia and Herzegovina</td>
      <td>1980</td>
      <td>4.180000e+06</td>
      <td>5500.0</td>
      <td>2.12</td>
      <td>69.7</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33499</th>
      <td>Belarus</td>
      <td>1980</td>
      <td>9.570000e+06</td>
      <td>8580.0</td>
      <td>2.08</td>
      <td>71.0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33500</th>
      <td>Belize</td>
      <td>1980</td>
      <td>1.440000e+05</td>
      <td>3860.0</td>
      <td>5.85</td>
      <td>70.9</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33501</th>
      <td>Bolivia</td>
      <td>1980</td>
      <td>5.580000e+06</td>
      <td>5170.0</td>
      <td>5.52</td>
      <td>56.8</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33502</th>
      <td>Brazil</td>
      <td>1980</td>
      <td>1.210000e+08</td>
      <td>10600.0</td>
      <td>4.07</td>
      <td>62.7</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33503</th>
      <td>Barbados</td>
      <td>1980</td>
      <td>2.520000e+05</td>
      <td>13600.0</td>
      <td>2.00</td>
      <td>73.0</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33504</th>
      <td>Brunei</td>
      <td>1980</td>
      <td>1.940000e+05</td>
      <td>128000.0</td>
      <td>4.25</td>
      <td>67.5</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33505</th>
      <td>Bhutan</td>
      <td>1980</td>
      <td>4.070000e+05</td>
      <td>1410.0</td>
      <td>6.55</td>
      <td>52.8</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33506</th>
      <td>Botswana</td>
      <td>1980</td>
      <td>8.980000e+05</td>
      <td>3870.0</td>
      <td>6.21</td>
      <td>61.0</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33507</th>
      <td>Central African Republic</td>
      <td>1980</td>
      <td>2.200000e+06</td>
      <td>1450.0</td>
      <td>5.95</td>
      <td>49.2</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33508</th>
      <td>Canada</td>
      <td>1980</td>
      <td>2.440000e+07</td>
      <td>29800.0</td>
      <td>1.67</td>
      <td>75.2</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33509</th>
      <td>Switzerland</td>
      <td>1980</td>
      <td>6.280000e+06</td>
      <td>49100.0</td>
      <td>1.51</td>
      <td>76.0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33510</th>
      <td>Chile</td>
      <td>1980</td>
      <td>1.140000e+07</td>
      <td>9300.0</td>
      <td>2.78</td>
      <td>69.4</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33511</th>
      <td>China</td>
      <td>1980</td>
      <td>1.000000e+09</td>
      <td>1360.0</td>
      <td>2.32</td>
      <td>64.4</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33512</th>
      <td>Cote d'Ivoire</td>
      <td>1980</td>
      <td>8.030000e+06</td>
      <td>3780.0</td>
      <td>7.60</td>
      <td>56.7</td>
      <td>None</td>
    </tr>
    <tr>
      <th>33513</th>
      <td>Cameroon</td>
      <td>1980</td>
      <td>8.620000e+06</td>
      <td>4130.0</td>
      <td>6.63</td>
      <td>55.4</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33514</th>
      <td>Congo, Dem. Rep.</td>
      <td>1980</td>
      <td>2.640000e+07</td>
      <td>2150.0</td>
      <td>6.59</td>
      <td>52.1</td>
      <td>None</td>
    </tr>
    <tr>
      <th>33515</th>
      <td>Congo, Rep.</td>
      <td>1980</td>
      <td>1.780000e+06</td>
      <td>3930.0</td>
      <td>6.21</td>
      <td>52.8</td>
      <td>None</td>
    </tr>
    <tr>
      <th>33516</th>
      <td>Colombia</td>
      <td>1980</td>
      <td>2.690000e+07</td>
      <td>7520.0</td>
      <td>3.97</td>
      <td>68.9</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33517</th>
      <td>Comoros</td>
      <td>1980</td>
      <td>3.080000e+05</td>
      <td>2420.0</td>
      <td>7.13</td>
      <td>54.5</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33518</th>
      <td>Cape Verde</td>
      <td>1980</td>
      <td>2.840000e+05</td>
      <td>1330.0</td>
      <td>6.38</td>
      <td>66.8</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33519</th>
      <td>Costa Rica</td>
      <td>1980</td>
      <td>2.390000e+06</td>
      <td>9880.0</td>
      <td>3.59</td>
      <td>74.7</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33520</th>
      <td>Cuba</td>
      <td>1980</td>
      <td>9.850000e+06</td>
      <td>4770.0</td>
      <td>1.89</td>
      <td>73.6</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33521</th>
      <td>Cyprus</td>
      <td>1980</td>
      <td>6.850000e+05</td>
      <td>13900.0</td>
      <td>2.35</td>
      <td>71.3</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33522</th>
      <td>Czech Republic</td>
      <td>1980</td>
      <td>1.030000e+07</td>
      <td>18500.0</td>
      <td>2.18</td>
      <td>70.5</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33523</th>
      <td>Germany</td>
      <td>1980</td>
      <td>7.830000e+07</td>
      <td>30400.0</td>
      <td>1.47</td>
      <td>73.3</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33524</th>
      <td>Djibouti</td>
      <td>1980</td>
      <td>3.590000e+05</td>
      <td>3680.0</td>
      <td>6.44</td>
      <td>60.8</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33525</th>
      <td>Denmark</td>
      <td>1980</td>
      <td>5.120000e+06</td>
      <td>30900.0</td>
      <td>1.55</td>
      <td>74.4</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33526</th>
      <td>Dominican Republic</td>
      <td>1980</td>
      <td>5.800000e+06</td>
      <td>5440.0</td>
      <td>4.42</td>
      <td>69.3</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33527</th>
      <td>Algeria</td>
      <td>1980</td>
      <td>1.920000e+07</td>
      <td>8840.0</td>
      <td>6.79</td>
      <td>58.7</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33528</th>
      <td>Ecuador</td>
      <td>1980</td>
      <td>7.990000e+06</td>
      <td>8400.0</td>
      <td>4.73</td>
      <td>67.0</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33529</th>
      <td>Egypt</td>
      <td>1980</td>
      <td>4.330000e+07</td>
      <td>4610.0</td>
      <td>5.60</td>
      <td>58.5</td>
      <td>Africa</td>
    </tr>
  </tbody>
</table>
</div>



We successfully created a column containing the continent name of each country!


```python
# check unique values and their counts in the continent column
df.continent.value_counts()
```




    Africa           2142
    Asia             1974
    Europe           1638
    North America     840
    South America     504
    Oceania           378
    None              336
    Name: continent, dtype: int64




```python
# drop rows containing a continent column value of None
df.drop(df.index[df['continent'] == 'None'], inplace=True)
```

    /opt/conda/lib/python3.6/site-packages/pandas/core/frame.py:4097: SettingWithCopyWarning: 
    A value is trying to be set on a copy of a slice from a DataFrame
    
    See the caveats in the documentation: http://pandas.pydata.org/pandas-docs/stable/user_guide/indexing.html#returning-a-view-versus-a-copy
      errors=errors,
    


```python
# check removal of rows with none values in continent column
df.head(50)
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
      <th>country</th>
      <th>year</th>
      <th>population</th>
      <th>income</th>
      <th>child_per_woman</th>
      <th>life_expectancy</th>
      <th>continent</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>33480</th>
      <td>Afghanistan</td>
      <td>1980</td>
      <td>1.340000e+07</td>
      <td>1190.0</td>
      <td>7.45</td>
      <td>43.7</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33481</th>
      <td>Angola</td>
      <td>1980</td>
      <td>8.340000e+06</td>
      <td>1780.0</td>
      <td>7.50</td>
      <td>48.1</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33482</th>
      <td>Albania</td>
      <td>1980</td>
      <td>2.680000e+06</td>
      <td>4470.0</td>
      <td>3.62</td>
      <td>71.3</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33483</th>
      <td>United Arab Emirates</td>
      <td>1980</td>
      <td>1.020000e+06</td>
      <td>93800.0</td>
      <td>5.51</td>
      <td>67.6</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33484</th>
      <td>Argentina</td>
      <td>1980</td>
      <td>2.790000e+07</td>
      <td>17100.0</td>
      <td>3.33</td>
      <td>70.2</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33485</th>
      <td>Armenia</td>
      <td>1980</td>
      <td>3.100000e+06</td>
      <td>6920.0</td>
      <td>2.39</td>
      <td>70.2</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33486</th>
      <td>Antigua and Barbuda</td>
      <td>1980</td>
      <td>6.190000e+04</td>
      <td>7910.0</td>
      <td>2.12</td>
      <td>72.1</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33487</th>
      <td>Australia</td>
      <td>1980</td>
      <td>1.460000e+07</td>
      <td>26300.0</td>
      <td>1.90</td>
      <td>74.5</td>
      <td>Oceania</td>
    </tr>
    <tr>
      <th>33488</th>
      <td>Austria</td>
      <td>1980</td>
      <td>7.610000e+06</td>
      <td>28900.0</td>
      <td>1.65</td>
      <td>72.8</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33489</th>
      <td>Azerbaijan</td>
      <td>1980</td>
      <td>6.150000e+06</td>
      <td>7700.0</td>
      <td>3.50</td>
      <td>66.2</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33490</th>
      <td>Burundi</td>
      <td>1980</td>
      <td>4.160000e+06</td>
      <td>1040.0</td>
      <td>7.42</td>
      <td>48.5</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33491</th>
      <td>Belgium</td>
      <td>1980</td>
      <td>9.870000e+06</td>
      <td>28800.0</td>
      <td>1.63</td>
      <td>73.3</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33492</th>
      <td>Benin</td>
      <td>1980</td>
      <td>3.720000e+06</td>
      <td>2010.0</td>
      <td>7.03</td>
      <td>52.7</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33493</th>
      <td>Burkina Faso</td>
      <td>1980</td>
      <td>6.820000e+06</td>
      <td>921.0</td>
      <td>7.13</td>
      <td>48.6</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33494</th>
      <td>Bangladesh</td>
      <td>1980</td>
      <td>7.960000e+07</td>
      <td>1220.0</td>
      <td>6.36</td>
      <td>53.2</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33495</th>
      <td>Bulgaria</td>
      <td>1980</td>
      <td>8.880000e+06</td>
      <td>12700.0</td>
      <td>2.11</td>
      <td>71.2</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33496</th>
      <td>Bahrain</td>
      <td>1980</td>
      <td>3.600000e+05</td>
      <td>42800.0</td>
      <td>4.92</td>
      <td>68.4</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33497</th>
      <td>Bahamas</td>
      <td>1980</td>
      <td>2.110000e+05</td>
      <td>32600.0</td>
      <td>2.99</td>
      <td>68.6</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33498</th>
      <td>Bosnia and Herzegovina</td>
      <td>1980</td>
      <td>4.180000e+06</td>
      <td>5500.0</td>
      <td>2.12</td>
      <td>69.7</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33499</th>
      <td>Belarus</td>
      <td>1980</td>
      <td>9.570000e+06</td>
      <td>8580.0</td>
      <td>2.08</td>
      <td>71.0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33500</th>
      <td>Belize</td>
      <td>1980</td>
      <td>1.440000e+05</td>
      <td>3860.0</td>
      <td>5.85</td>
      <td>70.9</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33501</th>
      <td>Bolivia</td>
      <td>1980</td>
      <td>5.580000e+06</td>
      <td>5170.0</td>
      <td>5.52</td>
      <td>56.8</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33502</th>
      <td>Brazil</td>
      <td>1980</td>
      <td>1.210000e+08</td>
      <td>10600.0</td>
      <td>4.07</td>
      <td>62.7</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33503</th>
      <td>Barbados</td>
      <td>1980</td>
      <td>2.520000e+05</td>
      <td>13600.0</td>
      <td>2.00</td>
      <td>73.0</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33504</th>
      <td>Brunei</td>
      <td>1980</td>
      <td>1.940000e+05</td>
      <td>128000.0</td>
      <td>4.25</td>
      <td>67.5</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33505</th>
      <td>Bhutan</td>
      <td>1980</td>
      <td>4.070000e+05</td>
      <td>1410.0</td>
      <td>6.55</td>
      <td>52.8</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33506</th>
      <td>Botswana</td>
      <td>1980</td>
      <td>8.980000e+05</td>
      <td>3870.0</td>
      <td>6.21</td>
      <td>61.0</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33507</th>
      <td>Central African Republic</td>
      <td>1980</td>
      <td>2.200000e+06</td>
      <td>1450.0</td>
      <td>5.95</td>
      <td>49.2</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33508</th>
      <td>Canada</td>
      <td>1980</td>
      <td>2.440000e+07</td>
      <td>29800.0</td>
      <td>1.67</td>
      <td>75.2</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33509</th>
      <td>Switzerland</td>
      <td>1980</td>
      <td>6.280000e+06</td>
      <td>49100.0</td>
      <td>1.51</td>
      <td>76.0</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33510</th>
      <td>Chile</td>
      <td>1980</td>
      <td>1.140000e+07</td>
      <td>9300.0</td>
      <td>2.78</td>
      <td>69.4</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33511</th>
      <td>China</td>
      <td>1980</td>
      <td>1.000000e+09</td>
      <td>1360.0</td>
      <td>2.32</td>
      <td>64.4</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33513</th>
      <td>Cameroon</td>
      <td>1980</td>
      <td>8.620000e+06</td>
      <td>4130.0</td>
      <td>6.63</td>
      <td>55.4</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33516</th>
      <td>Colombia</td>
      <td>1980</td>
      <td>2.690000e+07</td>
      <td>7520.0</td>
      <td>3.97</td>
      <td>68.9</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33517</th>
      <td>Comoros</td>
      <td>1980</td>
      <td>3.080000e+05</td>
      <td>2420.0</td>
      <td>7.13</td>
      <td>54.5</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33518</th>
      <td>Cape Verde</td>
      <td>1980</td>
      <td>2.840000e+05</td>
      <td>1330.0</td>
      <td>6.38</td>
      <td>66.8</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33519</th>
      <td>Costa Rica</td>
      <td>1980</td>
      <td>2.390000e+06</td>
      <td>9880.0</td>
      <td>3.59</td>
      <td>74.7</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33520</th>
      <td>Cuba</td>
      <td>1980</td>
      <td>9.850000e+06</td>
      <td>4770.0</td>
      <td>1.89</td>
      <td>73.6</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33521</th>
      <td>Cyprus</td>
      <td>1980</td>
      <td>6.850000e+05</td>
      <td>13900.0</td>
      <td>2.35</td>
      <td>71.3</td>
      <td>Asia</td>
    </tr>
    <tr>
      <th>33522</th>
      <td>Czech Republic</td>
      <td>1980</td>
      <td>1.030000e+07</td>
      <td>18500.0</td>
      <td>2.18</td>
      <td>70.5</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33523</th>
      <td>Germany</td>
      <td>1980</td>
      <td>7.830000e+07</td>
      <td>30400.0</td>
      <td>1.47</td>
      <td>73.3</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33524</th>
      <td>Djibouti</td>
      <td>1980</td>
      <td>3.590000e+05</td>
      <td>3680.0</td>
      <td>6.44</td>
      <td>60.8</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33525</th>
      <td>Denmark</td>
      <td>1980</td>
      <td>5.120000e+06</td>
      <td>30900.0</td>
      <td>1.55</td>
      <td>74.4</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33526</th>
      <td>Dominican Republic</td>
      <td>1980</td>
      <td>5.800000e+06</td>
      <td>5440.0</td>
      <td>4.42</td>
      <td>69.3</td>
      <td>North America</td>
    </tr>
    <tr>
      <th>33527</th>
      <td>Algeria</td>
      <td>1980</td>
      <td>1.920000e+07</td>
      <td>8840.0</td>
      <td>6.79</td>
      <td>58.7</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33528</th>
      <td>Ecuador</td>
      <td>1980</td>
      <td>7.990000e+06</td>
      <td>8400.0</td>
      <td>4.73</td>
      <td>67.0</td>
      <td>South America</td>
    </tr>
    <tr>
      <th>33529</th>
      <td>Egypt</td>
      <td>1980</td>
      <td>4.330000e+07</td>
      <td>4610.0</td>
      <td>5.60</td>
      <td>58.5</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33530</th>
      <td>Eritrea</td>
      <td>1980</td>
      <td>1.730000e+06</td>
      <td>1420.0</td>
      <td>6.68</td>
      <td>42.7</td>
      <td>Africa</td>
    </tr>
    <tr>
      <th>33531</th>
      <td>Spain</td>
      <td>1980</td>
      <td>3.770000e+07</td>
      <td>18800.0</td>
      <td>2.22</td>
      <td>75.5</td>
      <td>Europe</td>
    </tr>
    <tr>
      <th>33532</th>
      <td>Estonia</td>
      <td>1980</td>
      <td>1.470000e+06</td>
      <td>13500.0</td>
      <td>2.06</td>
      <td>69.7</td>
      <td>Europe</td>
    </tr>
  </tbody>
</table>
</div>




```python
# check unique values and their counts in the continent column after removal of none values
df.continent.value_counts()
```




    Africa           2142
    Asia             1974
    Europe           1638
    North America     840
    South America     504
    Oceania           378
    Name: continent, dtype: int64



We have successfully deleted the rows with none values in the continent column


```python
# confirm data types of each column in the dataset
df.dtypes
```




    country             object
    year                 int64
    population         float64
    income             float64
    child_per_woman    float64
    life_expectancy    float64
    continent           object
    dtype: object




```python
# save the dataframe in a csv file named gapminder_dataset1.csv
df.to_csv('gapminder_dataset1.csv', index=False)
```

We have successfully saved our new clean dataset in the csv file named: 'gapminder_dataset1.csv'

<a id='eda'></a>
## Exploratory Data Analysis


In this stage we will go in the depth of our dataset, to get very important measures, for example we will study how population levels are related to the levels of income per person. Also another question we will answer is Which continent have the highest average af income per person along the previous 42 years!

Moreover, we will study the relationship between fertility and life from one side and population levels from the other side .... Let's Go!  





### Research Question 1 ( Are population levels of countries and income per person in those countries related?


```python
# explore the dataset
df.describe()
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
      <th>year</th>
      <th>population</th>
      <th>income</th>
      <th>child_per_woman</th>
      <th>life_expectancy</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>7476.000000</td>
      <td>7.476000e+03</td>
      <td>7476.000000</td>
      <td>7476.000000</td>
      <td>7476.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2000.500000</td>
      <td>3.418407e+07</td>
      <td>15535.339486</td>
      <td>3.427781</td>
      <td>68.368967</td>
    </tr>
    <tr>
      <th>std</th>
      <td>12.121729</td>
      <td>1.284499e+08</td>
      <td>17740.017174</td>
      <td>1.814881</td>
      <td>9.013872</td>
    </tr>
    <tr>
      <th>min</th>
      <td>1980.000000</td>
      <td>5.930000e+04</td>
      <td>385.000000</td>
      <td>0.900000</td>
      <td>9.500000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>1990.000000</td>
      <td>2.200000e+06</td>
      <td>3120.000000</td>
      <td>1.880000</td>
      <td>62.400000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2000.500000</td>
      <td>7.500000e+06</td>
      <td>9000.000000</td>
      <td>2.820000</td>
      <td>70.300000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2011.000000</td>
      <td>2.180000e+07</td>
      <td>20300.000000</td>
      <td>4.840000</td>
      <td>75.100000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2021.000000</td>
      <td>1.440000e+09</td>
      <td>128000.000000</td>
      <td>8.870000</td>
      <td>85.100000</td>
    </tr>
  </tbody>
</table>
</div>



Now, we have the different statistics for our dataset 


```python
# draw a scatter plot to show the relationship betweeen country's population and income per person
df.plot(x="population", y="income", kind="scatter")
plt.title('Relationship Between Population and Income Per Person'.title(),
               fontsize = 14, weight = "bold")
plt.xlabel('Population'.title(),
               fontsize = 10, weight = "bold")
plt.ylabel('Income Per Person'.title(),
               fontsize = 10, weight = "bold");
```


    
![png](output_55_0.png)
    


We used a scatter plot to show us how data are scattered across the two variables.
Here, we can observe that there is an inverse (negative) relationship between population and income per person.

### Research Question 2  (Which continent has the highest in average income per person across the last 42 years? And which continents come in the second and third places?)

To answer this question, we have to group our data by continent and to get the mean incomes for each of them, after that we can graph our data (the best chart will be the bar chart to see the results more clear)


```python
# get the mean income for each continent, and show the dataframe
cont = df.groupby('continent').income.mean()
cont
```




    continent
    Africa            4523.142390
    Asia             17616.796859
    Europe           29635.628816
    North America    15102.678571
    Oceania          11331.164021
    South America    12233.095238
    Name: income, dtype: float64




```python
# draw a bar chart to show the continents with highest income per person
plt.subplots(figsize=(8, 5))
plt.bar(cont.index, cont)
plt.title('Average Income Per Person Over Last 42 Years Across Continents'.title(),
               fontsize = 14, weight = "bold")
plt.xlabel('Continent'.title(),
               fontsize = 10, weight = "bold")
plt.ylabel('Average Income Per Person'.title(),
               fontsize = 10, weight = "bold");
```


    
![png](output_59_0.png)
    


From the bar chart above we can see that Europe is the highest continent in the average income per person across the last 42 years, followed by Asia and North America continents.

### Research Question 3  (Is there a relationship between population levels and child per woman (fertility)?)

A scatter plot will best describe this relationship, here we go!


```python
# draw a scatter plot to show the relationship between population levels and child per woman (fertility)
df.plot(x="population", y="child_per_woman", kind="scatter")
plt.title('Relationship Between Population and Fertility'.title(),
               fontsize = 14, weight = "bold")
plt.xlabel('Population'.title(),
               fontsize = 10, weight = "bold")
plt.ylabel('Child Per Woman (Fertility)'.title(),
               fontsize = 10, weight = "bold");
```


    
![png](output_62_0.png)
    


Obviously there is a negative relationship between fertility ( number of child per woman) and population levels

### Research Question 4 (Can we say that population and life expectancy are related to each other?)

Another scatter will make this relation very obvious as we will see next!


```python
## draw a scatter plot to show the relationship between population levels and life expectancy
df.plot(x="population", y="life_expectancy", kind="scatter")
plt.title('Relationship Between Population and Life Expectancy'.title(),
               fontsize = 14, weight = "bold")
plt.xlabel('Population'.title(),
               fontsize = 10, weight = "bold")
plt.ylabel('Life Expectancy'.title(),
               fontsize = 10, weight = "bold");
```


    
![png](output_65_0.png)
    


Here, we get that there is a positive relationship exists between population levels and life expectancy

<a id='conclusions'></a>
## Conclusions

> **1**: From the above analysis we can conclude that there is an inverse (negative) relationship between population and income per person, which means that high levels of income per person are in countries with low population and vice versa.

> **2**: Europe is the highest continent in the average income per person across 42 years, followed by Asia and North America continents with slight difference between the last two continents.

> **3**: We can observe from our analysis that there is a negative relationship between fertility ( number of child per woman) and population levels, and futher investigation is needed here to know reasons stand behind this relationship.

> **4**: On the other hand it is obvious that a positive relationship exists between population levels and life expectancy (average number years a new born child would live), as when population is hight the number of years of life expectancy increases and vice versa. 

> **Limitation**: More data needed to investigate the negative relationship between fertility ( number of child per woman) and population levels and the reasons stand behind this relationship.


## Submitting your Project 




```python
from subprocess import call
call(['python', '-m', 'nbconvert', 'Investigate_a_Dataset-Copy2.ipynb'])
```




    0




```python

```
