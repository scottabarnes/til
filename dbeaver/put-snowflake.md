# Using dbeaver to upload Snowflake files using PUT 

Was using the PUT [command](https://docs.snowflake.com/en/sql-reference/sql/put.html) to upload a CSV from local drive to Snowflake. Ensured that certificate was added to keystore using keytool.  

Running a command like:
    PUT file://C:\tmp\new_file.csv @EXISTING_SCHEMA/LOCATION;  

Gives the error `SQL Error [2] [0A000]: Unsupported feature 'unsupported_requested_format:snowflake'.` when run from a script stored in a folder linked via a project, but runs successfully when the script is saved within `General -> Scripts`. Think this is due to dbeaver config - not entirely sure why this is the case though! 
