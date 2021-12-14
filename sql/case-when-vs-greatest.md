# Case when vs. greatest

Not all SQL flavours permit the `GREATEST()` function. In these cases, a `CASE WHEN` statement can be used instead, as suggested in this [post](https://dba.stackexchange.com/a/215134).

E.g.

    CASE WHEN a > b then a else b end

