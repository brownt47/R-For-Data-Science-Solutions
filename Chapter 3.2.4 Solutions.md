## Solutions for 3.2.4 

**Problem 1: Run ggplot(data = mpg). What do you see?**

After running this command, we see an empty graph, much like the text mentioned
     
![image](/images/Exercise3.2.4.1.png)
  
&nbsp;   
&nbsp;   
&nbsp;   
   
**Problem 2: How many rows are in mpg? How many columns?**

Simply typing *"mpg"* into the command line will display some basic information about the data frame:
     
We see then *mpg* is a tibble data frame with 234 rows and 11 columns.  

*I always used the mnemonic divice of RC-Cola for remembering rows x columns is how a matrix's dimensions are listed.*
 
![image](/images/Exercise3.2.4.2.png)
  
&nbsp;   
&nbsp;   
&nbsp;   
  
   
     
  
**Problem 3: What does the *drv* variable describe? Read the help for *?mpg* to find out.**

Entering *?mpg* into the command line will open a description of the data frame in your help window in R-Studio.  
This provides a description of the data set and each of the variables/categories within it.

scrolling down the list of variables we see that *drv* stands for the drive train type a vehicle utilizes:
             
             f = front-wheel drive, r = rear wheel drive, 4 = 4wd
             
![image](/images/Exercise3.2.4.3.png)
     
     
&nbsp;   
&nbsp;   
&nbsp;   
 
     
             
**Problem 4: Make a scatterplot of hwy vs cyl**

the *geom_point()* will create scatterplots.  Here are two with swapping the choices of the x and y variables. 

Which looks better? Presentation is also a part of creating graphs.
```
     ggplot(data = mpg)+geom_point(mapping = aes (x= cyl, y=hwy))
```
![image](/images/Exercise3.2.4.4a.png)

```
     ggplot(data = mpg)+geom_point(mapping = aes (x= hwy, y=cyl))
```
![image](/images/Exercise3.2.4.4b.png)


&nbsp;   
&nbsp;   
&nbsp;   



**Problem 5: What happens if you make a scatterplot of *class* vs *drv*? Why is the plot not useful?**

Run the following code:  
```
     ggplot(data = mpg)+geom_point(mapping = aes (x= class, y=cyl))
```
Upon initial viewing of the graph we see that there is a compact vehicle that has a 4-cylinder engine and a minivan that has a 4-cylinder engine.
   
   
![image](/images/Exercise3.2.4.5a.png)
   
   What the graph is not showing is *how many* compact vehicles and minivans have 4-cylinder engines.  
   if you try using a "jitter" scatterplot, it will better reveal how many vehicles have particular engine types:
   
   Try:
   ```
       ggplot(data = mpg)+geom_jitter(mapping = aes (x= class, y=cyl))   `
   ```
   the jitter geom will add some noise to the data so all the points do not just stack on top of each other.  
   Now we can see there is only one 4-cylinder minivan and dozens of 4-cylinder compact vehicles.
   
   
![image](/images/Exercise3.2.4.5b.png)
&nbsp;   
&nbsp;   
&nbsp;   
