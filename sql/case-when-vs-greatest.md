# Case when vs. greatest

Not all SQL flavours permit the `GREATEST()` function. In these cases, a `CASE WHEN` statement can be used instead, as suggested in this [post](https://dba.stackexchange.com/a/215134).

E.g.

    CASE WHEN a > b then a else b end


Although - in Netezza SQL it appears `MAX()` can be used in place of `GREATEST()` as outlined [here](https://stackoverflow.com/questions/18576891/greatest-function-in-netezza) and [here](https://stackoverflow.com/questions/30748437/greatest-least-or-max-min-calculation-in-sql).