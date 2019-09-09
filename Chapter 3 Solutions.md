##Solutions for 3.2.4
**Problem 1: Run ggplot(data = mpg). What do you see?**
     After running this command, we see an empty graph, much like the text mentioned
     
**Problem 2: How many rows are in mpg? How many columns?**
     Simply typing "mpg" into the command line will display some basic information about the data frame:
     
     > mpg
     # A tibble: 234 x 11   
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
   >ggplot(data = mpg)+geom_jitter(mapping = aes (x= class, y=cyl))   the jitter geom will add some noise to the data so all the points do not just stack on top of each other.
   
   

   



