---
title: "Pandas: Best Practicees Guide"
sub_title: "A useful function for electricity markets time series data that combines two dataframe columns into one index"
categories:
  - Python
tags:
  - Time Series
  - Data
  - Pandas
image: 
---


### Some Pointers for Handling Large Datasets in Python
	1. Use Categorical DataTypes

	Selectively assign a category datatype. This saves memory when working with Pandas Series and DataFrames.

	```python
	data = 'col1,col2,col3\na,b,1\na,b,2\nc,d,3'
	df = pd.read_csv(pd.compat.StringIO(data), dtype={'col1':'category'})
	print (df.dtypes)
	df.memory_usage(index=False, deep=True)
	```

	2. Use the "chunksize" parameters in Pandas when reading csv files.

	```python
	chunks_df = pd.read_csv(datasource, chunksize=1000000)
	chunk_list = []  # append each chunk df here 

	#Each chunk is in df format
	for chunk in chunks_df:  
	   
		#Once the data filtering is done, append the chunk to list
		chunk_list.append(chunk)
		
	#concat the list into dataframe 
	df_concat = pd.concat(chunk_list)
	```

	3. Filter-out columns

	Remove all unnecessary columns when preparing a dataframe for processing.

	```python
	df = df['a','b']
	```
	
	4. Free-up some memory by changing column types (i.e. int64 to int32)
	
	Use .astype() to convert your column types

	```python
	#Change the dtypes (int64 -> int32)
	df[['a','b']] = df[[['a','b']].astype('int32')

	#Change the dtypes (float64 -> float32)
	df[[['a','b']]] = df[[['a','b']]].astype('float32')
	```

### Sources:
1. [Why and How to Use Pandas with Large Data](https://towardsdatascience.com/why-and-how-to-use-pandas-with-large-data-9594dda2ea4c)
2. [Categorical DataTypes](https://pandas.pydata.org/pandas-docs/stable/user_guide/categorical.html)
3. [Pandas Tips and Tricks](https://realpython.com/python-pandas-tricks/)