# Applying a function to many columns using lambda 

Typically if I wanted to apply a function to many columns in a dataframe, I'd do something like


    def append_to_col(col):
        return col + '_append'

    fields_to_apply = ['field1','field2','field3']

    for field in fields_to_apply:
        df[field] = df[field].apply(append_to_col)

`lambda` can be used to do this in a cleaner way, e.g. 


    def append_to_col(col):
        return col + '_append'

    df = df.apply(lambda row: append_to_col(row['field1'],row['field2'],row['field3']))
