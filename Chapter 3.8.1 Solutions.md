
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

>*Amount of vertical and horizontal jitter. The jitter is added in both positive and negative directions, so the total spread is twice the value specified here.

>If omitted, defaults to 40% of the resolution of the data: this means the jitter values will occupy 80% of the implied bins. Categorical data is aligned on the integers, so a width or height of 0.5 will spread the data so it's not possible to see the distinction between the categories.*

**height**

>*Amount of vertical and horizontal jitter. The jitter is added in both positive and negative directions, so the total spread is twice the value specified here.

>If omitted, defaults to 40% of the resolution of the data: this means the jitter values will occupy 80% of the implied bins. Categorical data is aligned on the integers, so a width or height of 0.5 will spread the data so it's not possible to see the distinction between the categories.*

You can choose to add noise in either direction: horizontally, vertically, or both.  You can even remove noise by setting the parameter to zero.

Using the plot from ***Exercise 1***, try out a few values for the `width` parameter:  `0.1, 1, 5`   and we will turn off the vertical jittering by setting `height = 0`

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

Lastly for fun, setting both `width` and `height` to a large value should truly scatter the scatterplot to be unrecognizable from the original overplotted data in ***Exercise 1***

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(width = 20, height = 20)
```

![image](/images/Exercise3.8.1.2h.png)
