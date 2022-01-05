# Get DDL function

When creating a table (or other object) which has the same (or similar) schema to an existing table, the `get_ddl` function in Snowflake returns a DDL statement that can be used to recreate the specified object. Schema is as below:

    SELECT GET_DDL('table', 'DATABASE.SCHEMA.TABLE');