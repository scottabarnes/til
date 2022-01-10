# Using interval when adding to timestamps 

Was adding a series of day intervals to a timestamp field. E.g.:


  Days_to_add   
  ---------|
  1 |
  2 |
  3 |

Adding these to a timestamp field without using INTERVAL to the nearest n-days, e.g. for timestamp `10-01-2022 16:35`

`select timestamp + days_to_add as timestamp_add;`

Gives something like:

 timestamp_add   
  ---------|
  10-02-2022 00:00 |
  10-03-2022 00:00 |
  10-04-2022 00:00 |

Interval needs to be used to add a full 24 hour period per day, e.g.

` select timestamp + days_to_add || ' days' as timestamp_add`;

This gives the expected output of: 

 timestamp_add   
  ---------|
  10-02-2022 16:35 |
  10-03-2022 16:35 |
  10-04-2022 16:35 |
