#  Exercises for 3.7.1

## Exercise 1: What is the default geom associated with stat_summary()? How could you rewrite the previous plot to use that geom function instead of the stat function?

Pull up the documentation for it with `?stat_summary()` and you will see in the Usage the `goem` it is associated with is `pointrange`

Part 2 of this is not obvious at all.  I wish the author had added a few examples showing how changing the "stat" option of a geom impacts the plot.
If you try to just swap out `stat_summary` with `geom_pointrange` you will get an error stating that ymin and ymax must be set in the aesthetic before the plot can be made.
There hasn't been a discussion on how to quickly get that information.
