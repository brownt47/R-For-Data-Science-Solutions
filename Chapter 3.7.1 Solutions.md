#  Exercises for 3.7.1

## Exercise 1: What is the default geom associated with stat_summary()? How could you rewrite the previous plot to use that geom function instead of the stat function?

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
  
When `stat_summary` is called, it will automatically calculate some summary statistics on the data that is passed to it and stores the calculated values in similarily named variables.  What we want to do is call the `stat_summary` function into the `geom_pointrange` so that we can reference min and max.  To do this we override the default stat in `geom_pointrange`from `stat="identity"` to `stat="summary"`  note: the call from stat="summary" can come after the values `min` and `max` are referenced.

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
