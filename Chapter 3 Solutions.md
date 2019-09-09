## Solutions for 3.2.4 

**Problem 1: Run ggplot(data = mpg). What do you see?**

     After running this command, we see an empty graph, much like the text mentioned
     
**Problem 2: How many rows are in mpg? How many columns?**

     Simply typing "mpg" into the command line will display some basic information about the data frame:
     
     > mpg
     A tibble: 234 x 11   
   manufacturer model      displ  year   cyl trans      drv     cty   hwy fl    class  
   <chr>        <chr>      <dbl> <int> <int> <chr>      <chr> <int> <int> <chr> <chr>  
 1 audi         a4           1.8  1999     4 auto(l5)   f        18    29 p     compact
 2 audi         a4           1.8  1999     4 manual(m5) f        21    29 p     compact
 3 audi         a4           2    2008     4 manual(m6) f        20    31 p     compact
 4 audi         a4           2    2008     4 auto(av)   f        21    30 p     compact
 
 
 We see then mpg is a tibble data frame with 234 rows and 11 columns.  
 I always used the mnemonic divice of RC-Cola for remembering rows x columns is how a matrix's dimensions are listed.
 
 
** Problem 3: What does the drv variable describe? Read the help for ?mpg to find out.**

Entering ?mpg into the command line will open a description of the data frame in your help window in R-Studio.  
This provides a description of the data set and each of the variables/categories within it.

scrolling down the list of variables we see that drv stands for the drive train type a vehicle utilizes:
             f = front-wheel drive, r = rear wheel drive, 4 = 4wd
             
**Problem 4: Make a scatterplot of hwy vs cyl**

the geom_point() will create scatterplots.

>ggplot(data = mpg)+geom_point(mapping = aes (x= hwy, y=cyl))


**Problem 5: What happens if you make a scatterplot of class vs drv? Why is the plot not useful?**

Run the following code:  >ggplot(data = mpg)+geom_point(mapping = aes (x= hwy, y=cyl))
   Upon initial viewing of the graph we see that there is a compact vehicle that has a four cylinder engine and one that has a six-cylinder engine.
   
   What the graph is not showing is how many compact vehicles have 4 and 6-cylinder engines.  
   if you try using a "jitter" scatterplot, it will better reveal how many vehicles have particular engine types:
   
   Try:
   >ggplot(data = mpg)+geom_jitter(mapping = aes (x= class, y=cyl))   
   
   the jitter geom will add some noise to the data so all the points do not just stack on top of each other.
   
   
# 3.3.1 Exercises

**Problem 1: What’s gone wrong with this code? Why are the points not blue?

>ggplot(data = mpg) + 
>  geom_point(mapping = aes(x = displ, y = hwy, color = "blue"))

What happened here is due to "color" being set inside the aesthetic then it is going to look in the data set for a variable called "blue" then use the properties (range, data type. etc.) to paint the colors with.  Since there is no variable labelled "blue" in the data set, the aes layer just defaults to red.  If we place it outside the aes() then this will instruct the plot to now set the color of all the dots to be painted blue.  Hadley discusses this here in more detail: https://nceas.github.io/oss-lessons/dataviz-and-interactive-tools/module-1-ggplot2.html

inside the aes() call will use the actual data to select colors, sizes, shapes appropriately.  outside the aes() will set the colors, sizes and shapes to whatever you declare.

**Problem 2: Which variables in mpg are categorical? Which variables are continuous? (Hint: type ?mpg to read the documentation for the dataset). How can you see this information when you run mpg?**

if you run ?mpg you can read the description of each variable and may be able to identify categorical variables from the context.  if you run mpg then at the top of each column it will tell you the data type the variable stores its data values as.  If you are familar with some basic programming, these should look like your primitve data types:  int = integers (discrete), dbl = double (continuous) chr = character (categorical)

>mpg
>A tibble: 234 x 11
>   manufacturer model      displ  year   cyl trans      drv     cty   hwy fl    class  
>   <chr>     >   <chr>      <dbl> <int> <int> <chr>      <chr> <int> <int> <chr> <chr>  
> 1 audi         a4           1.8  1999     4 auto(l5)   f        18    29 p     compact
> 2 audi         a4           1.8  1999     4 manual(m5) f        21    29 p     compact
> 3 audi         a4           2    2008     4 manual(m6) f        20    31 p     compact
>   ...


**Problem 3: Map a continuous variable to color, size, and shape. How do these aesthetics behave differently for categorical vs. continuous variables?**

using knowledge gained from the previous problem we can see that the variable displ is continuous (displ = engine displacement.  it involves how much fuel an engine is using to generate power if you were curious.  In essence a volume measurement)

keeping the same x and y, try the following to see how cont vs categorical acts on aesthetics.  And since we want the color, shape and size to react to the data, we place those statements inside the aes() function

Use displ for the continuous and class for categorical

>ggplot(data = mpg) + 
>    geom_point(mapping = aes(x = displ, y = hwy, color = displ))
    
vs

>ggplot(data = mpg) + 
>    geom_point(mapping = aes(x = displ, y = hwy, color = class))

as you repeat the above for shape and size, you will get some warning messages and some will not plot at all.




