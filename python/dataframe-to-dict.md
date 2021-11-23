# Converting a dataframe to a dictionary

I was trying to simulate a JSON payload from a dataframes with multiple rows. 

First thought was to use `to_dict`, e.g.

    d = {'col1': [1, 2], 'col2': [3, 4]}
    df = pd.DataFrame(data=d)
    df.to_dict('records')

However this returns a list of dictionaries, e.g. `[{'col1': 1, 'col2': 3}, {'col1': 2, 'col2': 4}]`.

By transposing the records before converting to dict, and setting `orient` to dict, the output is a dictionary where the keys are the row indexes, e.g.
    
    df.transpose().to_dict('dict')

Which returns `{0: {'col1': 1, 'col2': 3}, 1: {'col1': 2, 'col2': 4}}` which is much closer to the JSON payload structure intended. 