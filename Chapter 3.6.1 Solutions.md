# Chapter 3.6.1 Exercise Solutions #


### Exercise 1: What geom would you use to draw a line chart? A boxplot? A histogram? An area chart?

Cheatsheets are a good place to start:  here is an updated link (Nov 2019) to one for Geoms:  [Data Visualiztion with ggplot2 Cheat Sheet.pdf](https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)

A line chart?  geom_line, geom_smooth or geom_step would be good starts.  there are others depending on the data type you are working with

A boxplot?  geom_boxplot or some variants like geom_dotplot or geom_violin

A histogram?  geom_histogram, or a variant like geom_dotplot or geom_bar (if you aren't splitting hairs on histogram vs bar chart)

An area chart?  lots to choose from here depending on your data.  geom_area, geom_polygon, geom_map

### Exercise 2: Run this code in your head and predict what the output will look like. Then, run the code in R and check your predictions. 
```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)```
```
We should get a scatterplot of *displ* vs *hwy* where the dots will be colored according to the *drv* levels, we should also get an overlay of lines that best fit the data for the *drv* levels, with the confidence boundaries around the lines turned off.  Hopefully the color of the lines matches the color of the points.

and here is the graphic rendered in R

![image](/images/Exercise3.6.1.1.png)

### Exercise 3: What does `R show.legend = FALSE` do? What happens if you remove it? Why do you think I used it earlier in the chapter?

The option of `show.legend = FALSE` will tell the geom to not show the legend next to the plot.  If you remove the line (or set it to `TRUE`) then it will show the legend so that the viewer can see which line and color correspondes to which *drv* type

I assume the author wanted to remove the legend so the three example code and their graphs could appear as similar as possible.

here is the graph with the line removed and we see the legend to the right of the plot:

```R
ggplot(data = mpg) +
  geom_smooth(mapping = aes(x = displ, y = hwy, color = drv) )
```

![image](/images/Exercise3.6.1.3a.png)

### Exercise 4: What does the `se` argument to `geom_smooth()` do?

This will add the shaded region around the line that represents the 'standard error (se)' for the line.  You may also know this as the confidence interval based on a level of confidence (default is 95%) from your statistics studies.  

Here is an example from this section with the `se` feature set to `FALSE` and `TRUE`
```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = class)) + 
  geom_smooth(data = filter(mpg, class == "subcompact"), se = FALSE)
```
#### `se` value set to `FALSE`
![image](/images/Exercise3.6.1.4a.png)

```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point(mapping = aes(color = class)) + 
  geom_smooth(data = filter(mpg, class == "subcompact"), se = TRUE)
```
#### `se` value set to `TRUE`
![image](/images/Exercise3.6.1.4b.png)

