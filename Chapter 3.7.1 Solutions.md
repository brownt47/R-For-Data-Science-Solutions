#  Exercises for 3.7.1

## Exercise 1: What is the default geom associated with `stat_summary()`? How could you rewrite the previous plot to use that geom function instead of the stat function?

Pull up the documentation for it with `?stat_summary()` and you will see in the "Usage section" the `geom` `stat_summary()` is associated with is `pointrange`.  Now pull up the documentaion with `?geom_pointrange` and you will see it's associated stat is `"identity"`.  That is your hint for the next part...

Part 2 of this is not obvious at all.  I wish the author had added a few examples showing how changing the "stat" option of a geom impacts the plot.
If you try to just swap out `stat_summary` with `geom_pointrange` you will get an error stating that ymin and ymax must be set in the aesthetic before the plot can be made.  There hasn't been a discussion on how to quickly get that information.

in the example to mimic we see there are required fields for the aesthetic, namely `fun.ymin` and `fun.ymax` and we see they are being assigned the values `min` and `max`, respectively.  There is no explaination for where `min` and `max` are coming from or where they are being calculated.  Similarily with `fun.y` and `median`

```R
ggplot(data = diamonds) + 
  stat_summary(
    mapping = aes(x = cut, y = depth),
    fun.ymin = min,
    fun.ymax = max,
    fun.y = median
  )
  ```
  
When `stat_summary` is called, it will automatically calculate some summary statistics on the data that is passed to it and stores the calculated values in similarily named variables.  What we want to do is call the `stat_summary` function into the `geom_pointrange` so that we can reference `min` and `max`.  To do this we override the default stat in `geom_pointrange`from `stat="identity"` to `stat="summary"`  note: the call from `stat="summary"` can come after the values `min` and `max` are referenced.

```R
ggplot(data = diamonds) +
  geom_pointrange(
    mapping = aes(x = cut, y = depth),
    fun.ymin = min,
    fun.ymax = max,
    fun.y = median,
    stat = "summary"
  )
  ```
  
  here we get the replicated plot:
  
  ![image](/images/Exercise3.7.1.1.png)


### Exercise 2: What does `geom_col()` do? How is it different to `geom_bar()`?

Once again, pull up the documentation for `?geom_col` using the `?`and it will reference Bar Charts in general and speak about the difference between `geom_col` and `geom_bar`. 

`geom_bar` will count up all the entries of a particular category and display the bar heights as a result of total counts.  `geom-col` will instead create bar hights that match the value of the data.

Let's use the tibble created in the section as an example to contrast the two geoms.
```R
demo <- tribble(
  ~cut,         ~freq,
  "Fair",       1610,
  "Good",       4906,
  "Very Good",  12082,
  "Premium",    13791,
  "Ideal",      21551
)
```

Looking at the tribble we see there is only one entry for "Fair" and the value associated with "Fair" is "1610".  Same thing for the other levels of cuts; there is only one row entry for each cut.

If we use the `geom_bar` on this tribble, we will get five bars all with a height of one.  This is because there is only one row for each of the labels: "Fair", "Good", etc.

 ![image](/images/Exercise3.7.1.2a.png)
 
 If we alter the tribble by adding another "Fair" row, we should see a change in the geom_bar plot now that there are two Fair entries.
 
 `geom_bar` is simply counting the number of rows that have "Fair", "Good", etc. in the `cut` column.
 
 ```R
 demo2 <- tribble(
  ~cut,         ~freq,
  "Fair",       1610,
  "Fair",       8500,
  "Good",       4906,
  "Very Good",  12082,
  "Premium",    13791,
  "Ideal",      21551
)

ggplot(data = demo2)+
  geom_bar( aes( x = cut ))
```
  
   ![image](/images/Exercise3.7.1.2b.png)
   
 Now let's compare what happens to the `demo` and `demo2` tribbles when the `geom_col` is applied.  Note we have to tell `geom_col` where to get the frequency data for our labels, hence `y=freq` is added to the aesthetic.
 
 #### Using the `demo` tribble that had one row entry for "Fair"
 
```R
 ggplot(data = demo)+
  geom_col(aes(x = cut, y = freq))
```
  ![image](/images/Exercise3.7.1.2c.png)

#### Using the `demo2` tribble that had two row entries for "Fair"  *Notice it automatically sums the "Fair" frequencies together*

```R
 ggplot(data = demo2)+
  geom_col(aes(x = cut, y = freq))
```

  ![image](/images/Exercise3.7.1.2d.png)
  
In short, if you have unsummarized data - `geom_bar` will automatically count the total entries for each category

if your data already has summarized data columns, `geom_col` will let you plot bar heights directly from your summarized data.
  
