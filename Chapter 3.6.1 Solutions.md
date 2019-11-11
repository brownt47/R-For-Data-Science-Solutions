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

### Exercise 5: Will these two graphs look different? Why/why not?

These graphs should look the same.  They are all using the same data and mappings, just the first one is declaring it in the ggplt statement with the idea it will be passed to the following geoms, the latter is declaring the data and mappings within each geom separately.
```R
ggplot(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_point() + 
  geom_smooth()
```
![image](/images/Exercise3.6.1.5a.png)

```R
ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy)) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy))
```

![image](/images/Exercise3.6.1.5b.png)


### Exercise 6: Recreate the R code necessary to generate the following graphs.

**Upper Left** - we see all the points in the same color and one line passing thru the points.  doesn't seem to be any differentiation on any other features or variables.  The size of the line stroke seems to be a bit thick and looks to have `se` set to `FALSE`.  Also the dots seem to overlap, so increase the size in the points geom.  Lastly, notice the blue line is covering the dots it passes.  the line is sitting on top of the dots

```R
ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy), size = 5) + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy), se = FALSE, size = 3)
```
![image](/images/Exercise3.6.1.6a.png)

**Upper Right** - similar to the Upper Left plot, but there are now three trend lines.  They appear to be the same ones seen earlier in the section that are grouped according to *drv* type.  Notice the line is behind the dots here, so we will change the order of our geoms.

```R
ggplot() + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy, group = drv),  se = FALSE, size = 3) +
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy), size = 5) 
  ```
![image](/images/Exercise3.6.1.6b.png)

**Middle Left** - Now we see the lines and dots are color coded to the *drv* variable. Here we can drop the `group` option in exchange for `color` inside the aesthetics.  Hard to distinguise if the dots are on top of the lines or vice-verse.  Try both to see which is the best match.   it seems the dots are on top of the lines

```R
ggplot() + 
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy, color = drv),  se=FALSE, size = 3)+
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy, color = drv), size = 5) 
```

![image](/images/Exercise3.6.1.6c.png)

**Middle Right** - Here we are reverting back to one line for the whole data set and it appears to be set on top of the points/dots.

```
ggplot() + 
  geom_point(data = mpg, mapping = aes(x = displ, y = hwy, color = drv), size = 5) +
  geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy),  se = FALSE, size = 3)
```  

![image](/images/Exercise3.6.1.6d.png)


**Lower Left** - similar to the Middle Left, just adding a line stroke feature of solid and dashed lines, but all the lines are the same color.  So we will remove the `color=drv` and replace it with `linestyle=drv` inside the aesthetic of the smooth geom.  The lines appear to be on top of the points as well.

```R
ggplot() + 
    geom_point(data = mpg, mapping = aes(x = displ, y = hwy, color = drv ), size = 5) +
    geom_smooth(data = mpg, mapping = aes(x = displ, y = hwy, linetype = drv),  se = FALSE, size = 3)
 ```

![image](/images/Exercise3.6.1.6e.png)

**Lower Right** - no lines are present, so we will remove the smooth geom completely.  It seems the points have white halos around them. Use `?geom_point` to see what option will turn on that effect.  here is a hint from the documentation:

  > For shapes that have a border (like 21), you can colour the inside and
  > outside separately. Use the stroke aesthetic to modify the width of the
  > border
  > `ggplot(mtcars, aes(wt, mpg)) +
  >  geom_point(shape = 21, colour = "black", fill = "white", size = 5, stroke = 5)`

So adding the `shape=21`, then using *drv* to `fill` in the color, and adjusting `stroke` and `color` to address the "halo" part
```R
ggplot(data=mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy, fill = drv ), size = 5, color="white", stroke = 2, shape=21)
```
![image](/images/Exercise3.6.1.6f.png)


this is close but the stroke/halo's of the points seem to cover up other points.  Maybe two sets of points overlapped can make the graph appear similar to the text.  Notice on the first geom for the background large white points, I placed the `color="white"` outside of the `aes()` statement since I want all the points to be white.  Whereas for the geom plotting the foreground points, i want the color to react to the data in drv so I place the `color = drv` inside the `aes()` statement

```R
ggplot() + 
    geom_point(data = mpg, mapping = aes(x = displ, y = hwy ), color = "white",  size = 10) +
    geom_point(data = mpg, mapping = aes(x = displ, y = hwy, color = drv ), size = 5)
```

This seems like a better recreation of the plot in the text:

![image](/images/Exercise3.6.1.6g.png)

## End of Section 3.6.1
