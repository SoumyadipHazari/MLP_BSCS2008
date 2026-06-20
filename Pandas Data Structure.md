
# Series

[[series.ipynb]]

> A series is a one -dimensional array-like object containing a sequence of values (similar to **NumPy** types) of the same type and an associated array of data labels called its *index*.

```python 
obj = pd.Series([3,5,6,27,-45.234,65])

obj

#gives output 
"""
0     3.000
1     5.000
2     6.000
3    27.000
4   -45.234
5    65.000
dtype: float64
"""

obj.index

#gives
# RangeIndex(start=0, stop=6, step=1)

obj.array

#gives
"""
<NumpyExtensionArray>
[3.0, 5.0, 6.0, 27.0, -45.234, 65.0]
Length: 6, dtype: float64
"""

# 

```

The string representation of a Series displayed shows the index in the left side and the values to the right. 

>Since we didn't have specify any index for the values, it taken the default one where the indexing starts from 0 to N-1 (where N is the length of the series) is created.

We can also specify the indexing of a Series 

```python

obj2 = pd.Series([4,-9,6,-2,66,21], index =["a","g","s","e","t","b"])

obj2

#gives
"""
a     4
g    -9
s     6
e    -2
t    66
b    21
dtype: int64
"""

obj2.index

#gives 

#Index(['a', 'g', 's', 'e', 't', 'b'], dtype='str')

obj2["g"]

#gives
#np.int64(-9)

obj2[["s","e","a"]]
#Here ["s","e","a"] is interpreted as a list of indices, even though it contains strings instead of integers.

#gives

"""
s    6
e   -2
a    4
dtype: int64
"""

```

We can work with dictionaries and meanwhile can you can create series from them by passing the dictionary 

```python

tdata = {"ohio": 35000, "texas": 600000, "delhi": 50000, "mumbai": 8000 }

obj3 = pd.Series(tdata)

obj3 

#gives 

"""
ohio       35000
texas     600000
delhi      50000
mumbai      8000
dtype: int64
"""

```

>you can convert a series into dictionary by using `to_dict()` method

```python

obj2.to_dict()

#gives you

#{'a': 4, 'g': -9, 's': 6, 'e': -2, 't': 66, 'b': 21}

```

>if you convert a dictionary into series the indexing will be according to the order of the keys but can be override this by passing an index with the dictionary keys in any order 

```python

# from the previous dictionary and data

states = ["Kolkata", "mumbai", "texas","kota", "ohio"]

obj4 = pd.Series(tdata, index = states)

obj4

#gives 
"""
Kolkata         NaN
mumbai       8000.0
texas      600000.0
kota            NaN
ohio        35000.0
dtype: float64
"""

# where NaN means Not a number

```

>`isna` and `notna`

```python

pd.isna(obj4) # or obj4.isna()

#gives

"""Kolkata     True
mumbai     False
texas      False
kota        True
ohio       False
dtype: bool"""

pd.notna(obj4) #or obj4.notna()

#gives

"""
Kolkata    False
mumbai      True
texas       True
kota       False
ohio        True
dtype: bool
"""
```

```python

obj3 + obj4

#gives

"""Kolkata          NaN
delhi            NaN
kota             NaN
mumbai       16000.0
ohio         70000.0
texas      1200000.0
dtype: float64"""

```

```python

obj.index = ["Bob", "steve", "billo", "billi", "meow", "lulu"]

obj 

#gives

"""
Bob       3.000
steve     5.000
billo     6.000
billi    27.000
meow    -45.234
lulu     65.000
dtype: float64
"""

```


# DataFrame

[[dataframe.ipynb]]

A **DataFrame** represents a rectangular table of data and contains an ordered, named collection of columns each of which can be a different value type (numeric, string, Boolean etc)

This has both a row and column index which can be thought of as a dictionary of **Series** of all sharing the same index.


```python
# first run the import pandas as pd
data = {"State": ["Ohio", "Ohio", "Ohio", "Texas", "Texas", "Texas", "kolkata", "kolkata", "kolkata"], "Year": [2000,2001,2002,2001,2002,2003,2001,2002,2003], "PoP": [1.5,1.6,3.6,2.4,2.9,3.2,2.6,2.8,3.4]}

frame = pd.DataFrame(data)

frame

#gives

"""
|State|Year|PoP|
|---|---|---|
|0|Ohio|2000|1.5|
|1|Ohio|2001|1.6|
|2|Ohio|2002|3.6|
|3|Texas|2001|2.4|
|4|Texas|2002|2.9|
|5|Texas|2003|3.2|
|6|kolkata|2001|2.6|
|7|kolkata|2002|2.8|
|8|kolkata|2003|3.4|
"""
```

>Head Method -- it gives the first 5 rows of the table
>Tail method -- it gives the last 5 rows of the table

```python

frame.head()

#gives
"""
|State|Year|PoP|
|---|---|---|
|0|Ohio|2000|1.5|
|1|Ohio|2001|1.6|
|2|Ohio|2002|3.6|
|3|Texas|2001|2.4|
|4|Texas|2002|2.9|
"""

frame.tail()

#gives
"""
|State|Year|PoP|
|---|---|---|
|4|Texas|2002|2.9|
|5|Texas|2003|3.2|
|6|kolkata|2001|2.6|
|7|kolkata|2002|2.8|
|8|kolkata|2003|3.4|
"""

```

> if we want then we change the sequence of the dataframe columns 

```python

pd.DataFrame(data, columns = ["Year", "State", "PoP"])

|Year|State|PoP|
|---|---|---|
|0|2000|Ohio|1.5|
|1|2001|Ohio|1.6|
|2|2002|Ohio|3.6|
|3|2001|Texas|2.4|
|4|2002|Texas|2.9|
|5|2003|Texas|3.2|
|6|2001|kolkata|2.6|
|7|2002|kolkata|2.8|
|8|2003|kolkata|3.4|

```

>if we pass a column with empty values in the dictionary then it will give NaN (not a number) 

```python

frame2 = pd.DataFrame(data, columns = ["Year", "State", "PoP", "debt"])

frame2

#gives

"""
|Year|State|PoP|debt|
|---|---|---|---|
|0|2000|Ohio|1.5|NaN|
|1|2001|Ohio|1.6|NaN|
|2|2002|Ohio|3.6|NaN|
|3|2001|Texas|2.4|NaN|
|4|2002|Texas|2.9|NaN|
|5|2003|Texas|3.2|NaN|
|6|2001|kolkata|2.6|NaN|
|7|2002|kolkata|2.8|NaN|
|8|2003|kolkata|3.4|NaN|
"""

frame2.columns

#gives

#Index(['Year', 'State', 'PoP', 'debt'], dtype='str')

frame2.State #or frame2["State"]

#gives
""""
0       Ohio
1       Ohio
2       Ohio
3      Texas
4      Texas
5      Texas
6    kolkata
7    kolkata
8    kolkata
Name: State, dtype: str
"""

```

> We can retrive any columns by using `.column_name` or `["column_name"]` 

> we can access  a row detailed by using `iloc` and `loc` attributes

```python

frame2.loc[1]

#gives

"""
Year     2001
State    Ohio
PoP       1.6
debt      NaN
Name: 1, dtype: object
"""

#we can access an specific rows specific column value 

frame2.iloc[2,1]

#gives 'Ohio' 

```

>The empty debt column could be assigned a scalar value or array of values

```python

frame2["debt"] = "13M"

frame2

#gives 

"""
|Year|State|PoP|debt|
|---|---|---|---|
|0|2000|Ohio|1.5|13M|
|1|2001|Ohio|1.6|13M|
|2|2002|Ohio|3.6|13M|
|3|2001|Texas|2.4|13M|
|4|2002|Texas|2.9|13M|
|5|2003|Texas|3.2|13M|
|6|2001|kolkata|2.6|13M|
|7|2002|kolkata|2.8|13M|
|8|2003|kolkata|3.4|13M|
"""
#or

frame2["debt"] = [45,2,3,4,51,45,2,1,53]

frame2

#gives

"""
|Year|State|PoP|debt|
|---|---|---|---|
|0|2000|Ohio|1.5|45|
|1|2001|Ohio|1.6|2|
|2|2002|Ohio|3.6|3|
|3|2001|Texas|2.4|4|
|4|2002|Texas|2.9|51|
|5|2003|Texas|3.2|45|
|6|2001|kolkata|2.6|2|
|7|2002|kolkata|2.8|1|
|8|2003|kolkata|3.4|53|
"""

```

> if you don't give the correct index array then this error happens `frame2["debt"] = [45,2,3,4,51,45,2,1]` gives you `ValueError: Length of values (8) does not match length of index (9)`

>if you assign a series where the indexing itself is different from the target DataFrame then that will not work as and the DataFrame will be same as before

```python

 val = pd.Series([-1.2, -1.5, -1.7], index=["two", "four", "five"])
frame2["debt"] = val

frame2

#gives
"""
|Year|State|PoP|debt|
|---|---|---|---|
|0|2000|Ohio|1.5|NaN|
|1|2001|Ohio|1.6|NaN|
|2|2002|Ohio|3.6|NaN|
|3|2001|Texas|2.4|NaN|
|4|2002|Texas|2.9|NaN|
|5|2003|Texas|3.2|NaN|
|6|2001|kolkata|2.6|NaN|
|7|2002|kolkata|2.8|NaN|
|8|2003|kolkata|3.4|NaN|
""" 
#but

val = pd.Series([-1.2, -1.5, -1.7], index=[2,4,5])
frame2["debt"] = val
frame2

"""
|Year|State|PoP|debt|
|---|---|---|---|
|0|2000|Ohio|1.5|NaN|
|1|2001|Ohio|1.6|NaN|
|2|2002|Ohio|3.6|-1.2|
|3|2001|Texas|2.4|NaN|
|4|2002|Texas|2.9|-1.5|
|5|2003|Texas|3.2|-1.7|
|6|2001|kolkata|2.6|NaN|
|7|2002|kolkata|2.8|NaN|
|8|2003|kolkata|3.4|NaN|
"""

```

```python

frame2["eastern"] = frame2["State"] == "Ohio"
frame2

"""
|Year|State|PoP|debt|eastern|
|---|---|---|---|---|
|0|2000|Ohio|1.5|NaN|True|
|1|2001|Ohio|1.6|NaN|True|
|2|2002|Ohio|3.6|-1.2|True|
|3|2001|Texas|2.4|NaN|False|
|4|2002|Texas|2.9|-1.5|False|
|5|2003|Texas|3.2|-1.7|False|
|6|2001|kolkata|2.6|NaN|False|
|7|2002|kolkata|2.8|NaN|False|
|8|2003|kolkata|3.4|NaN|False|
"""

```

>`del` method is used to remove columns 

```python

del frame2["eastern"]

frame2.columns

# Index(['Year', 'State', 'PoP', 'debt'], dtype='str')
```

> let there is a nested dictionary is passed to the DataFrame, pandas will interpret the
outer dictionary keys as the columns, and the inner keys as the row indices :

so when we pass a nested dictionary like 

```python

{
    "Ohio": {
        2000: 1.2,
        2001: 1.3,
        2002: 3.6
    },
    "Kolkata": {
        2001: 2.4,
        2002: 2.9
    }
}

```

then 
- Outer keys --> Columns
- Inner keys --> Row indices
- Inner  Values --> Cell Values

```python

population = {"ohio": {2000:1.2, 2001:1.3, 2002: 3.6},
             "Texas": {2001: 2.4, 2002: 2.9}}

frmae3 = pd.DataFrame(population)
frame3

"""
|ohio|Texas|
|---|---|
|2000|1.2|NaN|
|2001|1.3|2.4|
|2002|3.6|2.9|
"""

```

> we can shift the position of the row and column

```python

frame3.T

"""
|2000|2001|2002|
|---|---|---|
|ohio|1.2|1.3|3.6|
|Texas|NaN|2.4|2.9|
"""

```


| Type                                  | Notes                                                                                                                                                               |
| ------------------------------------- | ------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
| 2D ndarray                            | A matrix of data, passing optional row and column labels                                                                                                            |
| Dictionary of array, lists, or tuples | Each sequence becomes a column in the DataFrame; all sequences must be the same length                                                                              |
| NumPy structured /record array        | Treated as the "dictionary of array" case                                                                                                                           |
| Dictionary of dictionaries            | Each inner dictionary becomes a column; keys are unioned to form the row index as in the "dictionary of Series" case                                                |
| Dictionary of Series                  | Each value becomes a column; indexes from each Series are unioned<br>Dictionary of Series<br>together to form the result’s row index if no explicit index is passed |
| List of dictionaries or Series        | Each item becomes a row in the DataFrame; unions of dictionary keys or Series indexes become the DataFrame's column labels                                          |
| List of list or tuples                | Treated as the "2D ndarray" case                                                                                                                                    |
| Another DataFrame                     | The DataFrame’s indexes are used unless different ones are passed                                                                                                   |
| NumPy MaskedArray                     | Like the “2D ndarray” case except masked values are missing in the DataFrame result                                                                                 |
>Unlike Series, DataFrame does not have a name attribute. DataFrame's `to_numpy` method returns the data contained in the DataFrame as a two-dimensional ndarray:

```python

frame3.to_numpy()
"""
array([[1.2, nan],
       [1.3, 2.4],
       [3.6, 2.9]])
"""
# if the datatypes of the DataFrame's columns are different data types, the data type of the returned array will be chosen to accommodate all of the columns

frame2.to_numpy()
"""
array([[2000, 'Ohio', 1.5, nan],
       [2001, 'Ohio', 1.6, nan],
       [2002, 'Ohio', 3.6, -1.2],
       [2001, 'Texas', 2.4, nan],
       [2002, 'Texas', 2.9, -1.5],
       [2003, 'Texas', 3.2, -1.7],
       [2001, 'kolkata', 2.6, nan],
       [2002, 'kolkata', 2.8, nan],
       [2003, 'kolkata', 3.4, nan]], dtype=object)
"""
```


# Index Objects

[[index_objects.ipynb]]

Panda's Index objects are responsible for holding the axis labels (including a DataFrame's) and other metadata.

Any array or other sequence of labels you use when constructing a Series of DataFrame is internally converted to an index.

```python

obj = pd.Series(np.arange(3), index=["a","b","c"])
index = obj.index

index

#Index(['b', 'a', 'c'], dtype='str') 


```

>Index objects are immutable in nature (can't be modified by the user) so it makes safer to share Index objects among data structures:

```

index[1] = "d"

#TypeError: Index does not support mutable operations

```

```python

labels = pd.Index(np.arange(4))

labels

#Index([0, 1, 2, 3], dtype='int64')

obj2 = pd.Series([-1.3,4.5,-9.8], index = labels)

#gives you this -- ValueError: Length of values (3) does not match length of index (4)
obj2 = pd.Series([-1.3,4.5,-9.8,2.1], index = labels)
obj2


"""
1    1.2
3    3.4
5   -5.6
7    2.1
dtype: float64
"""

```

> Unlike Python sets, a pandas Index can contain duplicate labels:

```python

pd.Index(["foo","foo","faa","faa"])

#gives Index(['foo', 'foo', 'faa', 'faa'], dtype='str')
```

| Method         | Description                                                                               |
| -------------- | ----------------------------------------------------------------------------------------- |
| append()       | concatenate with additional index objects, producing a new index                          |
| difference()   | Compute set difference as an index                                                        |
| intersection() | compute set intersection                                                                  |
| union()        | compute set union                                                                         |
| isin()         | compute boolean array indicating whether each value is contained in the passed collection |
| delete()       | Compute new Index with element at Index i deleted                                         |
| drop()         | Compute new Index by deleting passed values                                               |
| insert()       | Compute new Index by inserting element at Index i                                         |
| is_monotonic   | Returns True if each element is greater than or equal to the previous element             |
| is_unique      | Returns True if the Index has no duplicate values                                         |
| unique()       | Compute the array of unique values in the Index                                           |
