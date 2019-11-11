# Chapter 3.6.1 Exercise Solutions #


## Exercise 1: What geom would you use to draw a line chart? A boxplot? A histogram? An area chart?

Cheatsheets are a good place to start:  here is an updated link (Nov 2019) to one for Geoms:  [Data Visualiztion with ggplot2 Cheat Sheet.pdf](https://rstudio.com/wp-content/uploads/2015/03/ggplot2-cheatsheet.pdf)

A line chart?  geom_line, geom_smooth or geom_step would be good starts.  there are others depending on the data type you are working with

A boxplot?  geom_boxplot or some variants like geom_dotplot or geom_violin

A histogram?  geom_histogram, or a variant like geom_dotplot or geom_bar (if you aren't splitting hairs on histogram vs bar chart)

An area chart?  lots to choose from here depending on your data.  geom_area, geom_polygon, geom_map

## Exercise 2: Run this code in your head and predict what the output will look like. Then, run the code in R and check your predictions. 

```ggplot(data = mpg, mapping = aes(x = displ, y = hwy, color = drv)) + 
  geom_point() + 
  geom_smooth(se = FALSE)```
