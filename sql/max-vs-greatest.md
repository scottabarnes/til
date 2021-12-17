# When to use max vs. greatest - and what to do if you can't use greatest

On first I assumed that the `max()` and `greatest()` functions in SQL performed the same operation. As detailed in this [blog](https://database.guide/max-vs-greatest-in-mysql-whats-the-difference/) this is not the case!

`MAX()` is used to return the maximum value in a column in a database, e.g.

    SELECT MAX(Population) as 'Result'
    FROM City;

`Greatest()` returns the maximum value from a list of arguments passed to it, e.g.

    SELECT GREATEST(1,5,9) as 'Result';

Which returns 9. 

From the blog post, it looks like `MAX()` should through an error when multiple arguments are passed to it on MySQL, but this doesn't seem to be the case on all SQL flavours. 

