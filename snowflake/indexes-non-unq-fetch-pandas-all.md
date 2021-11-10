# Indexes in dataframes created from `fetch_pandas_all` are not unique 

When reading in data using `fetch_pandas_all` from the [snowflake connector](https://github.com/snowflakedb/snowflake-connector-python) my expectation was for the dataframe created to have a unique index, as is the case in `pd.read_csv` when `index_col` is set to `None`. 

The indexes in the dataframe were not unique, so the below fails
```
df = cur.execute("SELECT * FROM TABLE").fetch_pandas_all()

assert len(df) == df.index.nunique()
```
There is not an equal distribution of indexes, i.e. some appear more frequently than others. 

An easy fix for this is to reset the index and drop the column created with duplicate indexes, like:
```
df.reset_index()
df.drop(columns=['index'])
```

I think this behaviour could be confusing for other users, so have raised a GitHub ticket [here](https://github.com/snowflakedb/snowflake-connector-python/issues/956).
