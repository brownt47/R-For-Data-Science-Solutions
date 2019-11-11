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
```{R message=False}
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
 
 If we alter the tribble by adding another "Fair" row, we should see a change in the `geom_bar` plot now that there are two "Fair" entries.
 
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
  
The following tables lists the pairs of geoms and stats that are almost always used in concert.

### Exercise 3.7.1.3

<div class="question">

Most geoms and stats come in pairs that are almost always used in concert.
Read through the documentation and make a list of all the pairs.
What do they have in common?

</div>

<div class="answer">

The following tables lists the pairs of geoms and stats that are almost always used in concert.

| geom                | stat                |
|---------------------|---------------------|
| `geom_bar()`        | `stat_count()`      |
| `geom_bin2d()`      | `stat_bin_2d()`     |
| `geom_boxplot()`    | `stat_boxplot()`    |
| `geom_contour()`    | `stat_contour()`    |
| `geom_count()`      | `stat_sum()`        |
| `geom_density()`    | `stat_density()`    |
| `geom_density_2d()` | `stat_density_2d()` |
| `geom_hex()`        | `stat_hex()`        |
| `geom_freqpoly()`   | `stat_bin()`        |
| `geom_histogram()`  | `stat_bin()`        |
| `geom_qq_line()`    | `stat_qq_line()`    |
| `geom_qq()`         | `stat_qq()`         |
| `geom_quantile()`   | `stat_quantile()`   |
| `geom_smooth()`     | `stat_smooth()`     |
| `geom_violin()`     | `stat_violin()`     |
| `geom_sf()`         | `stat_sf()`         |

Table: Complementary geoms and stats

They tend to have their names in common, `stat_smooth()` and `geom_smooth()`.
However, this is not always the case, with `geom_bar()` and `stat_count()` and `geom_histogram()` and `geom_bin()` as notable counter-examples.
Also, the pairs of geoms and stats that are used in concert almost always have each other as the default stat (for a geom) or geom (for a stat).

The following tables contain the geoms and stats in [ggplot2](https://ggplot2.tidyverse.org/reference/).

| geom                | default stat        | shared docs |
|:--------------------|:--------------------|-------------|
| `geom_abline()`     |                     |             |
| `geom_hline()`      |                     |             |
| `geom_vline()`      |                     |             |
| `geom_bar()`        | `stat_count()`      | x           |
| `geom_col()`        |                     |             |
| `geom_bin2d()`      | `stat_bin_2d()`     | x           |
| `geom_blank()`      |                     |             |
| `geom_boxplot()`    | `stat_boxplot()`    | x           |
| `geom_countour()`   | `stat_countour()`   | x           |
| `geom_count()`      | `stat_sum()`        | x           |
| `geom_density()`    | `stat_density()`    | x           |
| `geom_density_2d()` | `stat_density_2d()` | x           |
| `geom_dotplot()`    |                     |             |
| `geom_errorbarh()`  |                     |             |
| `geom_hex()`        | `stat_hex()`        | x           |
| `geom_freqpoly()`   | `stat_bin()`        | x           |
| `geom_histogram()`  | `stat_bin()`        | x           |
| `geom_crossbar()`   |                     |             |
| `geom_errorbar()`   |                     |             |
| `geom_linerange()`  |                     |             |
| `geom_pointrange()` |                     |             |
| `geom_map()`        |                     |             |
| `geom_point()`      |                     |             |
| `geom_map()`        |                     |             |
| `geom_path()`       |                     |             |
| `geom_line()`       |                     |             |
| `geom_step()`       |                     |             |
| `geom_point()`      |                     |             |
| `geom_polygon()`    |                     |             |
| `geom_qq_line()`    | `stat_qq_line()`    | x           |
| `geom_qq()`         | `stat_qq()`         | x           |
| `geom_quantile()`   | `stat_quantile()`   | x           |
| `geom_ribbon()`     |                     |             |
| `geom_area()`       |                     |             |
| `geom_rug()`        |                     |             |
| `geom_smooth()`     | `stat_smooth()`     | x           |
| `geom_spoke()`      |                     |             |
| `geom_label()`      |                     |             |
| `geom_text()`       |                     |             |
| `geom_raster()`     |                     |             |
| `geom_rect()`       |                     |             |
| `geom_tile()`       |                     |             |
| `geom_violin()`     | `stat_ydensity()`   | x           |
| `geom_sf()`         | `stat_sf()`         | x           |

Table: ggplot2 geom layers and their default stats.

| stat                 | default geom        | shared docs |
|:---------------------|:--------------------|-------------|
| `stat_ecdf()`        | `geom_step()`       |             |
| `stat_ellipse()`     | `geom_path()`       |             |
| `stat_function()`    | `geom_path()`       |             |
| `stat_identity()`    | `geom_point()`      |             |
| `stat_summary_2d()`  | `geom_tile()`       |             |
| `stat_summary_hex()` | `geom_hex()`        |             |
| `stat_summary_bin()` | `geom_pointrange()` |             |
| `stat_summary()`     | `geom_pointrange()` |             |
| `stat_unique()`      | `geom_point()`      |             |
| `stat_count()`       | `geom_bar()`        | x           |
| `stat_bin_2d()`      | `geom_tile()`       | x           |
| `stat_boxplot()`     | `geom_boxplot()`    | x           |
| `stat_countour()`    | `geom_contour()`    | x           |
| `stat_sum()`         | `geom_point()`      | x           |
| `stat_density()`     | `geom_area()`       | x           |
| `stat_density_2d()`  | `geom_density_2d()` | x           |
| `stat_bin_hex()`     | `geom_hex()`        | x           |
| `stat_bin()`         | `geom_bar()`        | x           |
| `stat_qq_line()`     | `geom_path()`       | x           |
| `stat_qq()`          | `geom_point()`      | x           |
| `stat_quantile()`    | `geom_quantile()`   | x           |
| `stat_smooth()`      | `geom_smooth()`     | x           |
| `stat_ydensity()`    | `geom_violin()`     | x           |
| `stat_sf()`          | `geom_rect()`       | x           |

Table: ggplot2 stat layers and their default geoms.
shamelessly stolen from Jrnold
</div>
