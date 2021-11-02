# Using base64 encoding to remove special characters from a string

I was trying to run a sql query through the [snowflake python connector](https://docs.snowflake.com/en/user-guide/python-connector-example.html) but was unable to read in the the data as one of the fields contained the '£' special character.  

At first I tried to remove the special character using regular expressions, e.g.:


    SELECT regexp_replace(messy_string, '[^0-9A-Za-z] ', '')) 
    as cleaned_string
    FROM TABLE;    

However this did not remove the special character from the source data so did not work. 

The hack I ended up using was to convert the string to base64 encoding when reading in the data, e.g.:


    SELECT base64_encode(regexp_replace(messy_string, '[^0-9A-Za-z] ', ''))) 
    as cleaned_string
    FROM TABLE;    

Once the data was imported, I created a function to convert the field back to a string, and replacing the special character when doing so: 

    def base64_to_str(string):
        ' Function to convert string from base64 back to string, removing £ sign
        decodedBytes = base64.urlsafe_b64decode(string)
        # Replace \\xa3 hex code character with pounds
        decodedStr = str(decodedBytes).replace("\\xa3",'pounds ')
        return decodedStr 

This was a bit hacky, but meant all the data could be used. 