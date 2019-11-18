
#  Exercises for 3.8.1

## Exercise 1: What is the problem with this plot? How could you improve it?

```r
  ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
     geom_point()
```
![image](/images/Exercise3.8.1.1.png)

Depending on the audience, there could be a whole host of things wrong with the plot.  Should we make use of color to differentiate the 
`class` of vehicles?  Should we use shapes to denote the type of `drv` class of each vehicle? Do we look for overplottting as mentioned in the section?

Say we want to add colors for each `class`.  Since we want the `color` feature to react to the data itself, we will place the argument `color = class` inside the aesthetic:

```R
ggplot(data = mpg, mapping = aes(x = cty, y = hwy, color = class)) + 
  geom_point()
```
![image](/images/Exercise3.8.1.1a.png)

Denoting the `cyl` for each data point by assigning a shape, again, place inside the aesthetic since we want the shape to react to the data:

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy, shape = drv)) + 
  geom_point()
```

![image](/images/Exercise3.8.1.1b.png)

Not bad but a little hard to see the shapes.  Let us increase the size of the points.  Note: since we want to change the size of the points, we will add the `size=3` argument in the `geom_point()` function.  It does not need to go inside the aesthetic since we want all the points to be larger, regardless of what the data points' shape represents

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy, shape=drv)) + 
  geom_point(size=3)
```

![image](/images/Exercise3.8.1.1c.png)

To address the issue of overplotting, we can add noise to the data with `geom_jitter` instead of `geom_point`

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter()
```
![image](/images/Exercise3.8.1.1d.png)

looking at the `?geom_jitter` documentation you will see you can control how "jittery" you want your data to be.  You can specify how much noise in the vertical or horizontal direction.

Here is a recreation with very small values of "jitter" = 0.05.  notice the points are still overlapping quite a bit and it looks very similar to the graph in the exercise.

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(height = .05, width = .05)
```
![image](/images/Exercise3.8.1.1e.png)


Here is one with possibly too much "jitter" = 5

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(height = 5, width = 5)
```

![image](/images/Exercise3.8.1.1f.png)


It would appear the default values for the amount of jitter were adequate without needing to adjust the amount of noise for jittering.

Now combine all the above together...color, shapes, size, jitter:

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy, color = class, shape = drv)) + 
  geom_jitter(size = 3)
```

![image](/images/Exercise3.8.1.1g.png)

Did we improve this plot?  We hope so.  This is a debate for the field of visualization.  Right now we are just practicing ways to alter plots in the hopes of improving the showcasing of the data we want to display.




## Exercise 2: What parameters to `geom_jitter()` control the amount of jittering? 

We already addressed this partly in the previous exercise

pulling directly from `?geom_jitter` we find the following:

**width**	

>Amount of vertical and horizontal jitter. The jitter is added in both positive and negative directions, so the total spread is twice the value specified here.
>If omitted, defaults to 40% of the resolution of the data: this means the jitter values will occupy 80% of the implied bins. Categorical data is aligned on the integers, so a width or height of 0.5 will spread the data so it's not possible to see the distinction between the categories.

**height**

>Amount of vertical and horizontal jitter. The jitter is added in both positive and negative directions, so the total spread is twice the value specified here.
>If omitted, defaults to 40% of the resolution of the data: this means the jitter values will occupy 80% of the implied bins. Categorical data is aligned on the integers, so a width or height of 0.5 will spread the data so it's not possible to see the distinction between the categories.

You can choose to add noise in either direction: horizontally, vertically, or both.  You can even remove noise by setting the parameter to zero.

Using the plot from **Exercise 1**, try out a few values for the `width` parameter:  `0.1, 1, 5`   and we will turn off the vertical jittering by setting `height = 0`

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 0.1, height = 0)
```
![image](/images/Exercise3.8.1.2a.png)

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 1, height = 0)
```
![image](/images/Exercise3.8.1.2b.png)


```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 5, height = 0)
```

![image](/images/Exercise3.8.1.2c.png)

Now, we will lock down the horizontal jitter by setting `width = 0` and altering values for the `height` parameter: `0.1, 1, 10`

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 0, height = 0.1)
```
![image](/images/Exercise3.8.1.2d.png)

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 0, height = 1)
```
![image](/images/Exercise3.8.1.2e.png)

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 0, height = 10)
```

![image](/images/Exercise3.8.1.2g.png)

Lastly for fun, setting both `width` and `height` to a large value should truly scatter the scatterplot to be unrecognizable from the original overplotted data in **Exercise 1**

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 20, height = 20)
```

![image](/images/Exercise3.8.1.2h.png)


## Exercise 3: Compare and contrast `geom_jitter()` with `geom_count()`

Pictures are worth 1000 words right?  Let us use the plot from **Exercise 1** with the different geoms

The original with `geom_point`

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_point()
```
![image](/images/Exercise3.8.1.1.png)

Now revisit the plot with `geom_jitter`

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter()
```

![image](/images/Exercise3.8.1.1d.png)

Lastly, plot the data using `geom_count`

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_count()
```
![image](/images/Exercise3.8.1.3c.png)

The `geom_count` will adjust the size of the plotted points based on the number of points that are all overplotted to the same location.  This is another way to convey overplotting, but depending on the distribution of the data, the now larger points can hide other points nearby.

There are a few features to tweak with `geom_count` with the two internal calculated values `n = number of observations at position` and `prop = percent of points in the panal at that position`

*Recall:* to reference an internal calculated value put ".." around the values:   `..n..` and `..prop..` in this case

To demonstrate, lets change the color of the points to react to the proportion of data points at that location.  Since I want the parameter to react to the data (or a value calculated from the data in this case), I will place the argument `color = ..prop..`inside an aesthetic:

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_count(aes(color = ..prop..))
```
![image](/images/Exercise3.8.1.4a.png)

## Exercise 4: What’s the default position adjustment for `geom_boxplot()`? Create a visualisation of the mpg dataset that demonstrates it.

As per usual, utilize `?geom_boxplot` to access the documentation to find defaults for geoms:

```geom_boxplot(mapping = NULL, data = NULL, stat = "boxplot",
  **position = "dodge2"**, ..., outlier.colour = NULL,
  outlier.color = NULL, outlier.fill = NULL, outlier.shape = 19,
  outlier.size = 1.5, outlier.stroke = 0.5, outlier.alpha = NULL,
  notch = FALSE, notchwidth = 0.5, varwidth = FALSE, na.rm = FALSE,
  show.legend = NA, inherit.aes = TRUE)
```

the `position` parameter is set to `dodge2` which is a special setting just for boxplots.

Since boxplots are useful for categorical comparisons.  Let's create a boxplot for each `class` of vehicle and plot the `hwy` mileage for that `class`

```r
ggplot(data = mpg, mapping = aes(x = class, y = hwy)) + 
  geom_boxplot()
```

![image](/images/Exercise3.8.1.4b.png)

Now lets split each boxplot into categories of the type of `drv` by assigning each `dyv` type to a color:

```r
ggplot(data = mpg, mapping = aes(x = class, y = hwy, color = drv)) + 
  geom_boxplot()
```

![image](/images/Exercise3.8.1.4c.png)

Now just play with the `position` parameter to see what changes.  Note: some choices will not be valid like `position="fill"` or `position="stack"`

```r
ggplot(data = mpg, mapping = aes(x = class, y = hwy, color = drv)) + 
  geom_boxplot(position = "identity")
```
Here we see each `drv`-boxplot is placed vertically above the `class` categories, but they overlap each other.

![image](/images/Exercise3.8.1.4d.png)

```r
ggplot(data = mpg, mapping = aes(x = class, y = hwy, color = drv)) + 
  geom_boxplot(position = "jitter")
```
Adds some randomness to how each boxplot is drawn.  Notice where some of the whiskers are in relation to the boxes.

![image](/images/Exercise3.8.1.4e.png)

```r
ggplot(data = mpg, mapping = aes(x = class, y = hwy, color = drv)) + 
  geom_boxplot(position = "dodge")
```

I cannot detect any difference between `"dodge"` and `"dodge2"` for all the feaures in this plot, but we can see every `drv`-boxplot is spaced out so as to avoid or 'dodge' any other `drv`-boxplots nearby

![image](/images/Exercise3.8.1.4f.png)
