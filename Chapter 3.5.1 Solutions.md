# 3.5.1 Exercises

**Problem 1: What happens if you facet on a continuous variable**

There is only one variable in the *mpg* dataset that is continuous, which is the displ category.  if we try to facet cut on that variable, R will create bins for the variable to make it act like a discrete variable.  Trying the code below we see that the bin size is around 0.2 and creates quite a few facets to the point that the facets just blur together to look like a standard x ~ y plot

> ggplot(data = mpg) + 
>     geom_point(mapping = aes(x = drv, y = hwy)) + 
>     facet_grid(~ displ)


![image](/images/Exercise3.5.1.1.png)

**Problem 2: What do the empty cells in plot with facet_grid(drv ~ cyl) mean? How do they relate to this plot?**

To the first question, the empty cells in the facet grid plots means there are no data points for that facet.  So there are no 4-or 5-cylinder vehiles that are rear-wheel drive, nor are there any 5-cylinder vehicles with all-wheel drive (4-wheel drive)

>ggplot(data = mpg) + 
>  geom_point(mapping = aes(x = drv, y = cyl))

![image](/images/Exercise3.5.1.2.png)


the plot above shows the same thing, it just doesn't take into consideration the displ difference in the combination classes of *drv* and *cyl*, with the added exceptions of the y-scale including the possibility of 7-cylinder vehicles due to treating the *drv* variable as a discrete numerical value and not a categorical one. 

**Problem 3: What plots does the following code make? What does . do?**

>ggplot(data = mpg) + 
>  geom_point(mapping = aes(x = displ, y = hwy)) +
>  facet_grid(drv ~ .)

This will produce multiple plots comparing *displ* vs *hwy* grouped only by the type of *drv*.  The "." indicates to show all the grouped plots in a horizontal fashion.  swapping the location of the dot will have the facet cuts aligned vertically

![image](/images/Exercise3.5.1.3a.png)

>ggplot(data = mpg) + 
>  geom_point(mapping = aes(x = displ, y = hwy)) +
>  facet_grid(. ~ cyl)

Here we see the plots grouped by *cyl* and aligned vertically

![image](/images/Exercise3.5.1.3b.png)


**Take the first faceted plot in this section:**

>ggplot(data = mpg) + 
>  geom_point(mapping = aes(x = displ, y = hwy)) + 
>  facet_wrap(~ class, nrow = 2)

**What are the advantages to using faceting instrad of the colour asthetic?  What are the disadvantages? How might the balance change if you had a larger dataset?**

Here is the plot from the beginning of the section:

![image](/images/Exercise3.5.1.4a.png)


Here is a similar plot using the color aesthetic to represent class of vehicles:

>ggplot(data = mpg) + 
>  geom_point(mapping = aes(x = displ, y = hwy, color=class))  

![image](/images/Exercise3.5.1.4b.png)

The faceting allows each class of vehicle to have its own plot where as the color aesthetic is comparing them all on one plot combined. Faceting may help see a pattern in individual classes whereas the color aesthetic may reveal patterns among classes compared to each other.  

If the data set were larger and in particular had more features, then the number of facet grids would increase making it hard to spot a pattern across classes.  The color aesthetic may have too many colors or classes over-lapping to see where one class ends and the next begins.
