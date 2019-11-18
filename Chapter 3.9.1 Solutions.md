# Exercises for 3.9.1

## Exercise 1: Turn a stacked bar chart into a pie chart using `coord_polar()`

There is reference to a stacked bar chart in section **3.8**:

```r
ggplot(data = diamonds) + 
  geom_bar(mapping = aes(x = cut, fill = clarity))
```
 
  ![image](/images/Exercise3.9.1.1a.png)
  
  Let's see what happens when we apply the `coord_polar()` coordinate system
  
  ```r
  ggplot(data = diamonds) + 
    geom_bar(mapping = aes(x = cut, fill = clarity)) +
    coord_polar()
  ```
  
   ![image](/images/Exercise3.9.1.1b.png)

Not quite a pie chart.

Exploring `?coord_polar()` will provide some guidance in the examples section:

```r
# A pie chart = stacked bar chart + polar coordinates
pie <- ggplot(mtcars, aes(x = factor(1), fill = factor(cyl))) +
 geom_bar(width = 1)
pie + coord_polar(theta = "y")
```

The book really hasn't mentioned how to create a stacked bar chart for one category.  It referenced in section **3.8** that stacked bars are automatically created when setting x equal to a category and fill to different category.  yet throwing that into a `coord_polar` doesn't give us a pie chart.

To accomplish this we can set `x = 1` inside of `geom_bar()`  and this will render one bar (at x = 1 location) with a height of 234 (the number of rows in `mpg`)

```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1))
```
  ![image](/images/Exercise3.9.1.1c.png)
  
if we change the `position` parameter to `"fill"` we get a similar plot but now notice the y-axis goes from 0.00 to 1.00, since it is measuring proportions in the data.

```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1), position = "fill")
```
  ![image](/images/Exercise3.9.1.1d.png)
  
Not terribly exciting plots so far, I know.  Now let's fill that bar with some categorical data, `class` or `drv` should give something more appealing:

`drv`
```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1, fill = drv))
```
  ![image](/images/Exercise3.9.1.1e.png)

`class`
```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1, fill = class))
```
  ![image](/images/Exercise3.9.1.1f.png)
  
Adding the `position = "fill"` won't change the overall appearance of the plot, but `position="dodge"` should give us some more experience with how changing the `position` parameter impacts the plots. This is not needed for this exercise, but is a nice addon from the previous section.  We see each part of the "stack" now dodging each other by being placed next to one another


`drv`with `"dodge"`
```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1, fill = drv), position = "dodge")
```
  ![image](/images/Exercise3.9.1.1g.png)


`class`with `"dodge"`
```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1, fill = class), position = "dodge")
```
  ![image](/images/Exercise3.9.1.1h.png)

removing the "dodge" parameter, now just add-on `+ coord_polar()` and see what happens

```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1, fill=drv)) +
  coord_polar()
```
  ![image](/images/Exercise3.9.1.1i.png)

It looks more like a pie, but not cut right.  This is referred to as a *bullseye* chart.  The number of data items in each category is captured by how thick the radial (or donut) sections are.  

Digging back through the documentation in `?coord_polar` there is a parameter `theta` that will use either the x data or y data to determine where to cut the pie.  It defaults to "x" so try "y" to see what happens.  This is akin assigning data to *r* or *θ* for calculations like *S = rθ* for those that recall things about sectors and polor coordinate system

```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1, fill = drv)) +
  coord_polar(theta = "y")
```
  ![image](/images/Exercise3.9.1.1j.png)

Now we have a pie chart.  I am sure there are more features we can add to clean it up, but I am trying to just create things from the text or documentation within R as best as I can stumble upon.  Just trying things out and playing around with settings seems to be a major theme to this text.

Not to neglect our `class` data:

```r
ggplot(data = mpg) +
  geom_bar(mapping = aes(x = 1, fill = class)) +
  coord_polar(theta = "y")
```
  ![image](/images/Exercise3.9.1.1k.png)
