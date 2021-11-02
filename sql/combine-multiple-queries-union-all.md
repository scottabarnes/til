# Using union all to combine results from multiple queries

I wanted to execute multiple SQL statements and add the results to a table for viewing in one place. If I was doing this in Python I would iterate through the SQL statements and append the result to a list, but that's not possible in SQL. I found an easy way to do this was to use UNION all.

If we had a `monday_orders` table like:
| LOCATION | NUMBER_ORDERS | 
|--------------|-----------|
| UK | 21      |
| FRANCE | 21  |

And a  `tuesday_orders` table like:
| LOCATION | NUMBER_ORDERS | 
|--------------|-----------|
| UK | 19      |
| FRANCE | 19  |

I used something like the following SQL script:


    SELECT 'MONDAY' AS DAY, sum(number_orders) as total_orders from monday_orders
    UNION ALL
    SELECT 'TUESDAY' AS DAY, sum(number_orders) as total_orders from tuesday_orders;

To produce a table that looked like:

| DAY | total_orders | 
|--------------|-----------|
| MONDAY | 42      |
| TUESDAY | 38  |

Of course this method only works if the column names from each query are the same. 