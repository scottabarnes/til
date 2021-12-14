# When to use max vs. greatest - and what to do if you can't use greatest

On first I assumed that the max() and greatest() functions in SQL performed the same operation. As detailed in this [blog](https://database.guide/max-vs-greatest-in-mysql-whats-the-difference/) this is not the case!

`MAX()` is used to return the maximum value in a column in a database, e.g.

    SELECT MAX(Population) as 'Result'
    FROM City;

