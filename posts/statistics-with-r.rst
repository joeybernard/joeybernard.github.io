.. title: Statistics with R
.. slug: statistics-with-r
.. date: 2020-07-29 20:32:14 UTC-03:00
.. tags: 
.. category: 
.. link: 
.. description: 
.. type: text

R is actually a full programming language, designed around the tasks you tend to need to do when you are doing statistics. It was 
developed at Bell Labs. It is very similar to another statistical programming language, S. Since R and S are programming languages, 
any actual programs are actually implementations of this language. There are commercial implementations available, like S-Plus. 
We'll be looking at the open source implementation by the R Project. References to R from here on in will refer to this open source 
implementation.

R is broken up into a core engine and a full complement of libraries and functions which provides all of its capabilities. Because 
of this, different downloads contain different pre-packaged functions. However, there is an entire repository of extra functionality 
available at CRAN (Comprehensive R Archive Network). There is a strong community of people willing to share the work they've done 
through CRAN. Because of this, there is usually a function, or several, to handle almost any task you can imagine. And if not, you 
have the freedom to develop your own. Because R is broken down into a core engine and functions, this means that any graphical 
interface is simply bolted on top of the core. There are several graphical interfaces available, such as RComander or Rgui. 

.. image::/images/R/gui1.png

There are also graphical interfaces available for Windows and Mac OSX. We'll be looking at actual commands 
in R, so we'll be using the text interface. To start it, you simply have to type in "R" and hit enter. 

.. image::/images/R/text1.png

To quit R, you 
simply have to type "q();" and hit enter. In R, commands can end with either a semi-colon or a newline.

R has very extensive help files available for all of the commands and functions. Accessing these help pages can be done two ways:

.. sourcecode::

   > help(command)
   or
   > ?command

These help pages are in the form of man pages. 

.. image::/images/R/text2.png

You can run a whole series of commands by using the source command

.. sourcecode::

   > source("commands.R")

where the file "commands.R" contains all of the commands that you want to run as a single block. Think of this as if it were a shell 
script. You can send your output to a file with the sink command

.. sourcecode::

   > sink("output.txt")

Once you are done writing the output, you can reset the output back to the console with

.. sourcecode::

   > sink()

R can handle basic statistics out of the box. The available functions can do all of the single variable statistics that you are 
familiar doing. The first step is to load data. Data is stored in lists. These lists can be arranged as arrays and matrices. The 
easiest way to create data arrays is to use the concatenation function "c". This works well when you only have a little bit of data 
to work with.

.. sourcecode::

   > data1 = c(2,3,4,2,0,1,2)

This creates a single list, and dumps these values into the variable data1. Then you can use this variable in other functions. For 
example, if you wanted to find the average of these values, you would use

.. sourcecode::

   > mean(data1)
   [1] 2

The second line above is the output from the function "mean". Output is labeled with a numeric label "[1]". The output from the first 
command in a session has the label "[1]", the output from the second command is labeled "[2]", and so on. If you have a larger amount 
of data that you need to work with, you can use the read command to read in a file. If that data is in a table format, you can read 
that table in as a whole by using

.. sourcecode::

   > DataToUse = read.table("research.data")

You can access individual data elements by using the "[]" characters. So printing the second item is as simple as

.. sourcecode::

   > data1[2]
   [1] 3

If you wanted to set a value in a vector, you can use

.. sourcecode::

   > data1[2] = 5

So, let's say that you were making some measurements on whales. You would start by saving the data into a variable.

.. sourcecode::

   > whale = c(74,122,235,111,292,111,211,133,156,79)

The first thing you would want to do is to run some basic statistical functions to find the mean, variance and standard deviation

.. sourcecode::

   > mean(whale)
   [1] 152.4
   > var(whale)
   [2] 5113.378
   >std(whale)
   Error: couldn't find function "std"

It looks like there is no standard deviation function. But, since R is a full programming language, you can write your own.

.. sourcecode::

   > std = function(x) sqrt(var(x))
   > std(whale)
   [3] 71.50789

This shows one of the shortcomings of R. Since it is such a large system, it does tend to have a relatively steep learning curve. 
More research would have shown that there is a builtin standard deviation function, it's just that it was called "sd" instead of "std"

.. sourcecode::

   > sd(whale)
   [4] 71.50789

Sometimes it's worth taking the extra time to do some research before storming forward and writing all of the code yourself.

R has very extensive graphing capabilities, as well. It generates very high quality plots and graphs that you can use in publications. 
The commands can be very simple, if you just want a quick display so that you can visually inspect your data. If you want very 
specific output, with lots of markup and customizations, then R gives you full control over all of the details of your graphs. The 
most basic plot command is simply plot. Let's say that you have a series of two dimensional data

.. sourcecode::

   > x = c(1,2,3,4)
   > y = c(2,3,4,5)
   > plot(x,y)

This gives us the following plot. [gui2.png] This looks like a straight line, so you probably want to do a linear regression on it.

.. sourcecode::

   > abline(lm(y~x))

This command does the linear regression of a straight line and plots it on the same plot. [gui3.png] This seems like a pretty close 
fit, so we should probably look at the coefficients of the linear model

.. sourcecode::

   > lm(y~x)
   Call:
   lm(formula = y ~ x)
   Coefficients:
   (Intercept)           x
             1           1

So we end up with a straight line with a slope of 1 and an intercept of 1.

Once you've done all of your analysis, you'll probably want to generate some nice plots for your publication. By default, when you 
call one of the plotting functions, the output is the graphical display. But you can change this to an output file of a particular 
format. Let's say you want to generate some PNG's.

.. sourcecode::

   > png("filename.png")
   > plot(x,y)

This will save your plot to the file "filename.png". You can also save to several other file formats (jpeg, pdf, postscript, etc). 
There are also lots of other options available, so check out the help page.

This short crash course should give you an idea and starting point to exploring R. A good place to look for more information is the 
main page for the R project [http://www.r-project.org]. Remember to check out the CRAN repository [http://cran.r-project.org] before 
you put too much work into it. Also, if there are any scientific packages or computational science technique covered, please let me know.
