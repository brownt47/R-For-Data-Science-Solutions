# 3.3.1 Exercises
&nbsp;
&nbsp;
&nbsp;

**Problem 1: What’s gone wrong with this code? Why are the points not blue?**
```Rstudio
  ggplot(data = mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))
```
What happened here is due to "color" being set inside the aesthetic then it is going to look in the data set for a variable called "blue" then use the properties (range, data type. etc.) to paint the colors with.  Since there is no variable labelled "blue" in the data set, the aes layer just defaults to red.  If we place it outside the aes() then this will instruct the plot to now set the color of all the dots to be painted blue.  Hadley discusses this here in more detail: https://nceas.github.io/oss-lessons/dataviz-and-interactive-tools/module-1-ggplot2.html

![image](/images/Exercise3.3.1.1a.png)

inside the aes() call will use the actual data to select colors, sizes, shapes appropriately.  outside the aes() will set the colors, sizes and shapes to whatever you declare.  Here we put the color statement outside of the aes()
```
  ggplot(data = mpg) + geom_point(mapping = aes(x = displ, y = hwy), color = "blue")
```
![image](/images/Exercise3.3.1.1b.png)

**Problem 2: Which variables in mpg are categorical? Which variables are continuous? (Hint: type ?mpg to read the documentation for the dataset). How can you see this information when you run mpg?**

if you run ?mpg you can read the description of each variable and may be able to identify categorical variables from the context.  if you run mpg then at the top of each column it will tell you the data type the variable stores its data values as.  If you are familar with some basic programming, these should look like your primitve data types:  int = integers (discrete), dbl = double (continuous) chr = character (categorical)


![image](/images/Exercise3.3.1.2.png)
&nbsp;
&nbsp;
&nbsp;

**Problem 3: Map a continuous variable to color, size, and shape. How do these aesthetics behave differently for categorical vs. continuous variables?**

using knowledge gained from the previous problem we can see that the variable displ is continuous (displ = engine displacement.  it involves how much fuel an engine is using to generate power if you were curious.  In essence a volume measurement)

keeping the same x and y, try the following to see how continuous vs categorical acts on aesthetics.  And since we want the color, shape and size to react to the data, we place those statements inside the aes() function

Use *displ* for the continuous and *class* for categorical
```
  ggplot(data = mpg) + 
      geom_point(mapping = aes(x = displ, y = hwy, color = displ))
```
&nbsp;
![image](/images/Exercise3.3.1.3a.png)

vs
```
  ggplot(data = mpg) + 
    geom_point(mapping = aes(x = displ, y = hwy, color = class))
```

![image](/images/Exercise3.3.1.3b.png)

as you repeat the above for shape and size, you will get some warning messages and some will not plot at all.

![image](/images/Exercise3.3.1.3c.png)

![image](/images/Exercise3.3.1.3d.png)

![image](/images/Exercise3.3.1.3e.png)
```
  ggplot(data = mpg) + 
  +         geom_point(mapping = aes(x = displ, y = hwy, size = displ))
```

![image](/images/Exercise3.3.1.3f.png)
```
  ggplot(data = mpg) + 
  +         geom_point(mapping = aes(x = displ, y = hwy, shape = displ))
```

![image](/images/Exercise3.3.1.3h.png)

&nbsp;
&nbsp;
&nbsp;

**Problem 4: What happens if you map the same variable to multiple aesthetics?**

this will simply have all the aesthetics reacting to the same variable.  This could be a nice way to add extra emphasis to the variables importance in the data.  This would be more of a presentation strategy to have the color and size of the points change as the value of a variable also changes.  draw more attention to patterns in the data (and maybe help out anyone in the audience who may be colorblind)

example:
```
  ggplot(data = mpg) + 
      geom_point(mapping = aes(x = displ, y = hwy, size = class,color = class))
```

this will create a scatterplot that gives each class it's own color and shape (up to five shapes due to limit on number of categories shape is set to as default)


![image](/images/Exercise3.3.1.4a.png)





```
  ggplot(data = mpg) + 
      geom_point(mapping = aes(x = displ, y = hwy, shape = class,color = class))
```

![image](/images/Exercise3.3.1.4b.png)
&nbsp;
&nbsp;
&nbsp;

**Problem 5: What does the stroke aesthetic do? What shapes does it work with? (Hint: use ?geom_point)**

stroke correspondes to the width of lines when drawing shapes. Solid shapes like 15-20 will no be impacted by stroke.  the hollow shapes and those with a border will.

running the example below you will see the star shapes become almost circles as you move left to right whereas the triangles do not change size

```
  ggplot(data = mpg) + 
      geom_point(mapping = aes(x = displ, y = hwy, shape=class, stroke=displ, color=class))
```

![image](/images/Exercise3.3.1.5a.png)

&nbsp;
&nbsp;
&nbsp;

**Problem 6: What happens if you map an aesthetic to something other than a variable name, like aes(colour = displ < 5)? Note, you’ll also need to specify x and y. **

keeping with the same x = displ, y = hwy and adding color = displ < 5 inside the aes() function, the legend will give us a clue as to what is happening
```
  ggplot(data = mpg) + 
      geom_point(mapping = aes(x = displ, y = hwy, color=displ<5))
```
we see the points are plotted using two colors and the legend tells us which vehicles have a displ less than 5 and which have displ of 5 or greater.  the statement displ < 5 is a logical statement with two outcomes TRUE and FALSE.  Not limiting the color palette to those vehicles with a displ less than 5, which one may have initially anticipated.

# End of Section 3.3.1
