
#  Exercises for 3.8.1

## Exercise 1: What is the problem with this plot? How could you improve it?

```r
  ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
     geom_point()
```

Depending on the audience, there could be a whole host of things wrong with the plot.  Could we use color to differentiate the 
'class' of vehicles?  Should we use shapes to denote the type of 'drv' class of each vehicle? Do we look at overplottting as mentioned in the section?

Adding colors for each class.  Since we want the 'color' feature to react to the data itself, we will place the argument inside the aesthetic:

```R
ggplot(data = mpg, mapping = aes(x = cty, y = hwy, color = class)) + 
  geom_point()
```
![image](/images/Exercise3.8.1.1a.png)

Denoting the 'cyl' for each data point by assigning a shape, again, place inside the aesthetic:

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy, shape = drv)) + 
  geom_point()
```

![image](/images/Exercise3.8.1.1b.png)

Not bad but a little hard to see the shapes.  Let us increase the size of the points.  Note: since we want to change the size of the points, we will add the 'size=3' argument in the 'geom_point()' function

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy, shape=drv)) + 
  geom_point(size=3)
```

![image](/images/Exercise3.8.1.1c.png)

To address the issue of overplotting, we can add noise to the data with 'geom_jitter' instead of 'geom_point'

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter()
```
![image](/images/Exercise3.8.1.1d.png)

looking at the '?geom_jitter' documentation you will see you can control how "jittery" you want your data to be.  You can specify how much noise in the vertical or horizontal direction.

Here is a recreation with very small values of "jitter" = 0.05.  notice the points are still overlapping quite a bit.

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(height=.05,width=.05)
```
![image](/images/Exercise3.8.1.1e.png)


Here is one with possibly too much "jitter" = 5

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy)) + 
  geom_jitter(height=5,width=5)
```

![image](/images/Exercise3.8.1.1f.png)


It would appear the default values for the amount of jitter were adequate.

Now we could combine all the above together...color, shapes, size, jitter:

```r
ggplot(data = mpg, mapping = aes(x = cty, y = hwy, color = class, shape = drv)) + 
  geom_jitter(size = 3)
```

![image](/images/Exercise3.8.1.1g.png)






