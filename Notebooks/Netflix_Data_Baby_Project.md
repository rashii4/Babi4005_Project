## Netflix Movies and TV Shows – Exploratory Data Analysis

This notebook explores a dataset of movies and TV shows available on Netflix.
The goal is to understand content trends, genres, release patterns,
and limitations of the dataset using exploratory data analysis.


```python
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import seaborn as sns
```

## Setup and Data Loading

The following section imports the required Python libraries and loads the Netflix dataset locally. The dataset file is excluded from GitHub
using `.gitignore`.


```python
df = pd.read_csv("NetFlix.csv")
```


```python
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
      <th>show_id</th>
      <th>type</th>
      <th>title</th>
      <th>director</th>
      <th>cast</th>
      <th>country</th>
      <th>date_added</th>
      <th>release_year</th>
      <th>rating</th>
      <th>duration</th>
      <th>genres</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>s1</td>
      <td>TV Show</td>
      <td>3%</td>
      <td>NaN</td>
      <td>João Miguel, Bianca Comparato, Michel Gomes, R...</td>
      <td>Brazil</td>
      <td>14-Aug-20</td>
      <td>2020</td>
      <td>TV-MA</td>
      <td>4</td>
      <td>International TV Shows, TV Dramas, TV Sci-Fi &amp;...</td>
      <td>In a future where the elite inhabit an island ...</td>
    </tr>
    <tr>
      <th>1</th>
      <td>s10</td>
      <td>Movie</td>
      <td>1920</td>
      <td>Vikram Bhatt</td>
      <td>Rajneesh Duggal, Adah Sharma, Indraneil Sengup...</td>
      <td>India</td>
      <td>15-Dec-17</td>
      <td>2008</td>
      <td>TV-MA</td>
      <td>143</td>
      <td>Horror Movies, International Movies, Thrillers</td>
      <td>An architect and his wife move into a castle t...</td>
    </tr>
    <tr>
      <th>2</th>
      <td>s100</td>
      <td>Movie</td>
      <td>3 Heroines</td>
      <td>Iman Brotoseno</td>
      <td>Reza Rahadian, Bunga Citra Lestari, Tara Basro...</td>
      <td>Indonesia</td>
      <td>5-Jan-19</td>
      <td>2016</td>
      <td>TV-PG</td>
      <td>124</td>
      <td>Dramas, International Movies, Sports Movies</td>
      <td>Three Indonesian women break records by becomi...</td>
    </tr>
    <tr>
      <th>3</th>
      <td>s1000</td>
      <td>Movie</td>
      <td>Blue Mountain State: The Rise of Thadland</td>
      <td>Lev L. Spiro</td>
      <td>Alan Ritchson, Darin Brooks, James Cade, Rob R...</td>
      <td>United States</td>
      <td>1-Mar-16</td>
      <td>2016</td>
      <td>R</td>
      <td>90</td>
      <td>Comedies</td>
      <td>New NFL star Thad buys his old teammates' belo...</td>
    </tr>
    <tr>
      <th>4</th>
      <td>s1001</td>
      <td>TV Show</td>
      <td>Blue Planet II</td>
      <td>NaN</td>
      <td>David Attenborough</td>
      <td>United Kingdom</td>
      <td>3-Dec-18</td>
      <td>2017</td>
      <td>TV-G</td>
      <td>1</td>
      <td>British TV Shows, Docuseries, Science &amp; Nature TV</td>
      <td>This sequel to the award-winning nature series...</td>
    </tr>
  </tbody>
</table>
</div>



### Dataset Overview

The dataset contains information on Netflix movies and TV shows,
including content type, release year, duration, genre, country,
cast, and director.

It includes thousands of titles spanning multiple decades and
a mix of categorical and numeric variables, making it suitable
for descriptive and exploratory data analysis.



```python
df.info
```




    <bound method DataFrame.info of      show_id     type                                      title  \
    0         s1  TV Show                                         3%   
    1        s10    Movie                                       1920   
    2       s100    Movie                                 3 Heroines   
    3      s1000    Movie  Blue Mountain State: The Rise of Thadland   
    4      s1001  TV Show                             Blue Planet II   
    ...      ...      ...                                        ...   
    7782    s995  TV Show                                 Blown Away   
    7783    s996  TV Show                              Blue Exorcist   
    7784    s997    Movie                  Blue Is the Warmest Color   
    7785    s998    Movie                               Blue Jasmine   
    7786    s999    Movie                                   Blue Jay   
    
                     director                                               cast  \
    0                     NaN  João Miguel, Bianca Comparato, Michel Gomes, R...   
    1            Vikram Bhatt  Rajneesh Duggal, Adah Sharma, Indraneil Sengup...   
    2          Iman Brotoseno  Reza Rahadian, Bunga Citra Lestari, Tara Basro...   
    3            Lev L. Spiro  Alan Ritchson, Darin Brooks, James Cade, Rob R...   
    4                     NaN                                 David Attenborough   
    ...                   ...                                                ...   
    7782                  NaN                                                NaN   
    7783                  NaN  Nobuhiko Okamoto, Jun Fukuyama, Kana Hanazawa,...   
    7784  Abdellatif Kechiche  Léa Seydoux, Adèle Exarchopoulos, Salim Kechio...   
    7785          Woody Allen  Cate Blanchett, Sally Hawkins, Alec Baldwin, L...   
    7786         Alex Lehmann           Sarah Paulson, Mark Duplass, Clu Gulager   
    
                         country date_added  release_year rating  duration  \
    0                     Brazil  14-Aug-20          2020  TV-MA         4   
    1                      India  15-Dec-17          2008  TV-MA       143   
    2                  Indonesia   5-Jan-19          2016  TV-PG       124   
    3              United States   1-Mar-16          2016      R        90   
    4             United Kingdom   3-Dec-18          2017   TV-G         1   
    ...                      ...        ...           ...    ...       ...   
    7782                  Canada  12-Jul-19          2019  TV-14         1   
    7783                   Japan   1-Sep-20          2017  TV-MA         2   
    7784  France, Belgium, Spain  26-Aug-16          2013  NC-17       180   
    7785           United States   8-Mar-19          2013  PG-13        98   
    7786           United States   6-Dec-16          2016  TV-MA        81   
    
                                                     genres  \
    0     International TV Shows, TV Dramas, TV Sci-Fi &...   
    1        Horror Movies, International Movies, Thrillers   
    2           Dramas, International Movies, Sports Movies   
    3                                              Comedies   
    4     British TV Shows, Docuseries, Science & Nature TV   
    ...                                                 ...   
    7782                 International TV Shows, Reality TV   
    7783               Anime Series, International TV Shows   
    7784   Dramas, Independent Movies, International Movies   
    7785               Comedies, Dramas, Independent Movies   
    7786        Dramas, Independent Movies, Romantic Movies   
    
                                                description  
    0     In a future where the elite inhabit an island ...  
    1     An architect and his wife move into a castle t...  
    2     Three Indonesian women break records by becomi...  
    3     New NFL star Thad buys his old teammates' belo...  
    4     This sequel to the award-winning nature series...  
    ...                                                 ...  
    7782  Ten master artists turn up the heat in glassbl...  
    7783  Determined to throw off the curse of being Sat...  
    7784  Determined to fall in love, 15-year-old Adele ...  
    7785  The high life leads to high anxiety for a fash...  
    7786  Two former high school sweethearts unexpectedl...  
    
    [7787 rows x 12 columns]>



## Missing Values


```python
df.isna().sum()
```




    show_id            0
    type               0
    title              0
    director        2389
    cast             718
    country          507
    date_added        10
    release_year       0
    rating             7
    duration           0
    genres             0
    description        0
    dtype: int64



Several columns contain missing values, particularly director, cast, and country. This is fairly common in real-world media datasets. While these gaps limit some detailed analysis, they do not prevent us from exploring overall trends and patterns.

## Summary Statistics

Summary statistics provide an overview of the distribution and range
of values in the dataset


```python
df.describe(include = "all")
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
      <th>show_id</th>
      <th>type</th>
      <th>title</th>
      <th>director</th>
      <th>cast</th>
      <th>country</th>
      <th>date_added</th>
      <th>release_year</th>
      <th>rating</th>
      <th>duration</th>
      <th>genres</th>
      <th>description</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>7787</td>
      <td>7787</td>
      <td>7787</td>
      <td>5398</td>
      <td>7069</td>
      <td>7280</td>
      <td>7777</td>
      <td>7787.000000</td>
      <td>7780</td>
      <td>7787.000000</td>
      <td>7787</td>
      <td>7787</td>
    </tr>
    <tr>
      <th>unique</th>
      <td>7787</td>
      <td>2</td>
      <td>7787</td>
      <td>4049</td>
      <td>6831</td>
      <td>681</td>
      <td>1565</td>
      <td>NaN</td>
      <td>14</td>
      <td>NaN</td>
      <td>492</td>
      <td>7769</td>
    </tr>
    <tr>
      <th>top</th>
      <td>s1</td>
      <td>Movie</td>
      <td>3%</td>
      <td>Raúl Campos, Jan Suter</td>
      <td>David Attenborough</td>
      <td>United States</td>
      <td>1-Jan-20</td>
      <td>NaN</td>
      <td>TV-MA</td>
      <td>NaN</td>
      <td>Documentaries</td>
      <td>Multiple women report their husbands as missin...</td>
    </tr>
    <tr>
      <th>freq</th>
      <td>1</td>
      <td>5377</td>
      <td>1</td>
      <td>18</td>
      <td>18</td>
      <td>2555</td>
      <td>118</td>
      <td>NaN</td>
      <td>2863</td>
      <td>NaN</td>
      <td>334</td>
      <td>3</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2013.932580</td>
      <td>NaN</td>
      <td>69.122769</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>std</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>8.757395</td>
      <td>NaN</td>
      <td>50.950743</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>min</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>1925.000000</td>
      <td>NaN</td>
      <td>1.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2013.000000</td>
      <td>NaN</td>
      <td>2.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2017.000000</td>
      <td>NaN</td>
      <td>88.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2018.000000</td>
      <td>NaN</td>
      <td>106.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
    <tr>
      <th>max</th>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>NaN</td>
      <td>2021.000000</td>
      <td>NaN</td>
      <td>312.000000</td>
      <td>NaN</td>
      <td>NaN</td>
    </tr>
  </tbody>
</table>
</div>



Most titles in the dataset were released in recent years, showing that
Netflix’s catalog is heavily focused on newer content. The wide range
of duration values reflects the mix of movies and TV shows, which makes
average duration less meaningful on its own.

## Graph 1: Movies vs TV Shows

This section compares the number of movies and TV shows available
in the Netflix dataset.


```python
df['type'].value_counts().plot(kind='bar')
plt.title("Movies vs TV Shows on Netflix")
plt.xlabel("Content Type")
plt.ylabel("Number of Titles")
plt.show()
```


    
![png](output_15_0.png)
    


Movies make up a larger portion of Netflix’s catalog compared to TV shows.
This suggests that while Netflix has expanded its original series,
movies still play a major role in its content library.

## Graph 2: Content Released Over Time


```python
df['release_year'].value_counts().sort_index().plot(kind='line')
plt.title("Number of Netflix Titles by Release Year")
plt.xlabel("Release Year")
plt.ylabel("Number of Titles")
plt.show()
```


    
![png](output_18_0.png)
    


There is a clear increase in the number of titles released after 2010.
This reflects Netflix’s rapid growth and its focus on expanding
its catalog with more recent content.

## Graph 3: Top 10 Genres



```python
df['genres'].value_counts().head(10).plot(kind='bar')
plt.title("Top 10 Genres on Netflix")
plt.xlabel("Genre")
plt.ylabel("Number of Titles")
plt.show()
```


    
![png](output_21_0.png)
    


Documentaries appear as the most common genre in the dataset.


```python

```
