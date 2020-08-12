---
layout:  post
title:   Analysing Data with Python
date:    2020-08-12
summary: Analysing and Plotting Data with Python Study Notes
categories: Python Data Analysis
---

# An introduction to Python

This tutorial aims to introduce Python and get familiar with the Jupyter notebook.

As you can see, a Jupyter's notebook is a combination of text and code (or _command_) cell. You can type and run any command in the code cell (or prompt) by double click onto it.


```python
# THIS IS A COMMAND CELL.
# YOU CAN WRITE YOUR CODE HERE.
# TO RUN YOUR CODE PRESS "SHIFT-ENTER" ON YOUR KEYBOARD
# OR PRESS THE "RUN BOTTOM" IN THE TOOLBAR
```


Jupyter interprets every word in a code cell as code unless the line starts with the symbol `#.` In python, the hashtag means _"ignore everything in this line"_ and therefore, it is used to add comments in the actual Python code.

An example is given below:


```python
# This is just a comment
x = 2 # this is another comment
```

In the example above the only command that Python executes is to set the variable _x_ to be equal to 2 (`x=2`) and it ignores every word after "#".

## Python as a Calculator

Let us introduce the primary command in Python by simply considering it as a calculator.


You can use a code cell to execute any numerical operation between numbers and print the result.
The syntax for numerical operations is straightforward: **+**, **-**, **\***, **/**. You can use round parenthesis for grouping as well.

**Run the command in the cell below for an example**
<a id='as_calculator'></a>


```python
# Example 1:
((4 + 5) - (14 / 7)) * 2
```




    14.0




```python
# Exercise:
# You can use this command cell for trying any operation you like
```

In the above example, the code does not "save" the result in any variable, but it just prints the value as output.

When you write code, you often need to do several calculations and use the value later. To do this, you need to assign the operation result into a variable.

Run the code in the cell below


```python
# Example 2:
# Let's save the result from ((4+5)-(14/7))*2 into the variable x and calculate the y=x*2
x = ((4 + 5) - (14 / 7)) * 2
y = x * 2
#...if you don't see any outputs, please do not panic just keep reading
```

As you have noticed, while the code in _Example 1_ produced an output ( `Out[]` ), the output is suppressed in the _Example 2_. If you want to display the value of any variables, you can type the variable in the command cell. For example


```python
x
```




    14.0



However, a better way is to use the command `print`, followed by the variable name in brackets. This command allows you to display several variables at the same time, if these are separating by a comma (`,`). For example, the code <center> `print(x,y) `</center> will display both **`x`** and **`y`**.


```python
# Example 2:
# Let's save the result from ((4+5)-(14/7))*2 into the variable x and calculate the y=x*2
x =((4 + 5) - (14 / 7)) * 2
y = x * 2
# Print both x and y
print(x, y)
```

    14.0 28.0


The command **`print()`** can also display sentence if they are contained in single brackets.


```python
print('The value of x is', x)
```

    The value of x is 14.0


In Python, you can create _non-numerical_ variable (named <b>string</b>) by enclosing letters in single quotes (`''`). For example, you can set a variable to contain letters, words or even sentences.

For example:


```python
# Set s as a string
s = 'This is a string'
print(s)
```

    This is a string


<div style="background-color:LAVENDER", text-align='justify'>
<h2> <center><FONT COLOR="Purple"> Hands On </FONT> </center></h2>
</div>
Copy the code used in the Example 2 cell and use `print()` to display the sentence "<b>The result is</b>" and the value of the variable <b>`y`</b>.
_Hints: Don't forget to enclose the words between single quotes `'The result is '` and the comma before the variable  `y`.

The output of your code should be: <b>The result is 28</b>.


```python
# Type your code here.
print('The result is', y)
```

    The result is 28.0


## Objects in Python
The real power of Python is that you can define different data structures, such as lists and data frame (more on this later). In Python, a *list* is a sequence of comma-separated values (or items) between square brackets. It can contain numbers, words or a bit of both.

For example:


```python
# a list of numbers
a = [18,25,3,4]
print('a contains', a)
# a list of strings
b = ['apple','orange','berry']
print('b contains', b)
# a mixed list
c = ['5','1244','green','berry', 'apple']
print('c contains', c)
```

    a contains [18, 25, 3, 4]
    b contains ['apple', 'orange', 'berry']
    c contains ['5', '1244', 'green', 'berry', 'apple']


Now, you can access the content of a list by using `your_list[i]`, where `i` is just a number that indicate the position of the i-th element. For example, `your_list[0]` will show the first element in `your_list`, `your_list[1]` the second one and so on.

**Important: Python starts to count from 0 and not from 1.**

If you create a list of 3 elements, like `your_list=[1,2,3]`, we said that `your_list` has length 3. In Python, you can always check the length of a list by typing `len(your_list)`. This is very useful when is you don't know how many elements a list has.



```python
your_list = [1,2,3]
print('The list contains', len(your_list), 'elements')
```

    The list contains 3 elements


Another important thing to keep in mind is that Python cannot access to elements that are not in your list. This means that if you try to print `your_list[4]`, asking for the fifth element, Python will print a `IndexError` pointing (see the arrow `---->`) to the line where the problem is.
But don't take this for granted and try yourself


```python
your_list = [1,2,3]
print(your_list[4])
```




    IndexErrorTraceback (most recent call last)

    <ipython-input-13-3597cb8707bb> in <module>
          1 your_list = [1,2,3]
    ----> 2 print(your_list[4])


    IndexError: list index out of range


Python can also access to the elements of a list *backwards*. This is done by using negative numbers for `i` (-1,-2, etc.). So, `your_list[-1]` is the last element, `your_list[-2]` is the second last and so on.


```python
print('first element of a is a[0] =', a[0]) # print the first element of a
print('last element of b is b[-1] =', b[-1]) # alternatively you can print b[2] Check your self!^_-
print('second last element of c is c[-2] =', c[-2])
```

    first element of a is a[0] = 18
    last element of b is b[-1] = berry
    second last element of c is c[-2] = berry


Python allows you to manipulate lists. For example, to add a new element `x` into your list, you can type `your_list.insert(i,x)`, where `i` is the index of the element before which to insert. To remove `x`, you can use `your_list.remove(x)`.

The code below shows a few examples on how to manipulate a list.



```python
# Manipulate a list
b = ['apple','orange','berry'];
# define a new list 'equal ' to b.
b_new = b

# insert an element into your_list:
# command 'your_list.insert(before this position,element to add)
# This will add the word 'apple' before the last element of b
b_new.insert(-1, 'apple')
print('b_new with an extra word apple', b_new)

# This will remove the word 'orange' that appear in the list
b_new.remove('orange')
print('b_new without the word orange', b_new)
```

    b_new with an extra word apple ['apple', 'orange', 'apple', 'berry']
    b_new without the word orange ['apple', 'apple', 'berry']


<div style="background-color:LAVENDER", text-align='justify'>
<h2> <center><FONT COLOR="Purple"> Hands On </FONT> </center></h2>
</div>

Follow the instructions in the cell below and complete the code.

**Important: before running it, you should first complete the code. Python cannot execute uncompleted code**.
Alternatively, you can add a new cell (by clicking on "+", second icon from the left in the toolbar) and copy and paste your completed code


```python
initial = [33,85,-5,8,24, 3,9] # initial list
print('initial list', initial)

my_list =  # create a new list equal to the initial one

x_sum =  # add the third element of my_list to the second last element.
print('x_sum = ', x_sum)

my_list.insert() # insert x_sum before the fourth element of my_list
print('my_list after adding x_sum is', my_list)

my_list.remove(3)#now remove the value 3 from my_list
print('At the end my_list looks like',my_list)
```


      File "<ipython-input-16-ea2fa8983d17>", line 4
        my_list =  # create a new list equal to the initial one
                                                               ^
    SyntaxError: invalid syntax




```python
initial = [33,85,-5,8,24, 3,9] # initial list
print('initial list', initial)

my_list = initial # create a new list equal to the initial one

x_sum = my_list[2] + my_list[-2] # add the third element of my_list to the second last element.
print('x_sum = ', x_sum)

my_list.insert(3, x_sum) # insert x_sum before the fourth element of my_list
print('my_list after adding x_sum is', my_list)

my_list.remove(3)# now remove the value 3 from my_list
print( 'At the end my_list looks like', my_list)
```

    initial list [33, 85, -5, 8, 24, 3, 9]
    x_sum =  -2
    my_list after adding x_sum is [33, 85, -5, -2, 8, 24, 3, 9]
    At the end my_list looks like [33, 85, -5, -2, 8, 24, 9]


**Check Your Results**

Let's proceed step by step and check your results.

The first instruction asks you to create a list equal to the one given. You need to manipulate the list, so it is good practice keep the original as a reference.

The next step is to sum two elements of the new list. If you are not sure how to do this Go back to [Python as Calculator](#as_calculator).
After running, the code prints `x_sum=` followed by your result.
If everything is correct, you should see

<center> <b>`x_sum= -2`</b>, </center>

as the instructions ask you to calculate the sum of the <b>third</b> and <b>second last</b> element.

On the other hand, if you see
<center> <b>`x_sum= 17`</b>  or  <b>`x_sum= 11`</b> or <b>`x_sum= 4`</b>, </center>

it means that your code is almost correct, but you've chosen the wrong elements for sum. Remember: Python <b>starts counting from 0</b> and that the index <b>-1</b> accesses to the <b>last</b> element.

<br>
Once you calculate `x_sum`, you need to insert it into `my_list`, at the position indicated in the text. The code should print
<center> <b>`my_list after adding x_sum is  [33, 85, -5, -2, 8, 24, 3, 9]`</b>.</center>
If your answer is different, check at which position the value of x_sum is printed. This will give you a hint on where the problem could be.
Remember that the `.insert()` module needs to know: the position before which you want insert the value and the actual value. If you want to insert the value "4" before the last element (index 3) you should type `my_list.insert(3,4)` (remember that Python starts counting from 0).
<br>
After removing the number 3 from `my_list`, your list is
<center> <b>`At the end my_list looks like [33, 85, -5, -2, 8, 24, 9]`</b>.</center>


# <center> MODULE 1: An Introduction to Pandas </center>

# Introduction

Data analysis, or data analytics, is the process of exploring, cleansing and transforming raw data to transform them into useful information. Data analysis is an increasingly important part of modern decision-making and strategic and policy analysis.
As an example, data analytics is used to track shopper preferences, both on-line and in brick and mortar stores. Another example is the adds that pop-up in your search engine or on your social media site, which are based on your own behaviour on the internet. Here is an example from google analytics, that runs powerful data analytics in the background.


![An example of data analysis: Google analytics](GoogleAnalytics.png)

Using Data analytics, all kinds of data are transformed into powerful information through graphing, slicing, statistics and discovery of relationships. Programs like Excel are designed to help users to do these analyses without worrying too much about the algorithms and coding. Instead these programs provide build-in tools.

However, these tailor-made programs have limitations and there are situations where the sheer size of the analysis you are looking for is such that the only alternative is to write your own code. This is often the case when the size of your dataset is larger than can be handled by more traditional software, or when you need to repeat the same long set of operations fpr different data sets. In those situations, knowing a programming language is crucial and it will help you to analyse your data in a very efficient and productive way.

Python is a very powerful and easy to learn a programming language and it is open source and free. In addition, there are several packages available out of charges for data analysis. In this tutorial, we will introduce the <b>pandas</b> package, a high-level building block for doing real-world data analysis.



# Learning Objectives
In this tutorial, you will:

• Learn how to import library in python

•	Learn how to read data files using <b>pandas</b>

•	Get familiar with data frame and data structures

•	Do data manipulation (e.g. perform operation on your data, creating subsample)

# Importing Pandas Library
The first step is to import Pandas into Python. Simply typing in your command cell <b>`import pandas`</b>. The <b>`import`</b> command tells python where all the tools are stored and that it needs to make them accessible to you. In the cell below, there is an example on how you can import this library. To run the command just click on command cell and press <b>Shift+ Enter</b> on your keyboard.



```python
import pandas
```

Once you have imported the library, you have access to all the tools stored in `pandas` and you can start working on your data. As case of study, we will analyse Australian population growth data, taken from the [Australia Bureau of Statistics website](http://www.abs.gov.au/AUSSTATS/abs@.nsf/DetailsPage/3101.0Jun%202016?OpenDocument). We downloaded the data into a file named `AustraliaDemographics.dat`.

## A case of study: Population growth in Australia

Pandas allows you to read data from a file and save its content into a data structure.
A file can be read using `pandas.read_table()` function, that takes as input parameter the file and folder path that you want to read and how the columns in the file are separated (`sep=`), for example by a white space or a comma .
If you want to know about read_table() you can type into a command cell help(pandas.read_table()) to access the help page.

So, for example to read the file `AustraliaDemographics.dat` (white space separated columns) you can type:


```python
import pandas
pop_data = pandas.read_table('AustraliaDemographics.dat', sep = ' ')
#Important: note the white space between single (after sep=)
```

<div style="background-color:HONEYDEW", text-align='justify'>
<h4> <center><FONT color="Green"> *Explanation* </FONT></center> </h4>
<br>

Let's analyse a bit what we just did.

For the `read_table()` command, we used single quotes twice, for the file name and for the `sep` argument. In Python, this means that we are defining a character variables (called `string`). A string can contain words, letters, numbers, space or symbols. In Python, the file names and their paths (folders) are <u><b>always</b></u> defined as string and therefore, enclosed into single quotes. If you don't include the single quotes, you will have a `NameError`. You can try yourself, by removing the single quotes from the code above.
Once we read the file, we saved all its content into a variable called <b>`pop_data`</b>.
</div>


The data describe the Australia demographic statistic between 2011 and 2015 for each state and territory.
The first column indicates the year of the census and the second one the state or territory where the data were taken.
The next five columns show the estimated States and territories resident population by sex (number of men, women and total) and the number of births and the death rates. The data also provide the net overseas migration (NOM) considering the number of overseas arrivals (NOM_A) and overseas departures (NOM_D). The last two columns are the population growth in each state and territories considering the natural growth and the net overseas growth, or rather, the contribution to the population growth by the overseas migrations. The data also provide information about the Australia as a nation for the 2011-2015 period.


#### But how can we explore the data? ####

Pandas offers several options for exploring a data frame. For example, you can type <b>`pop_data.head()`</b> to display the first five rows in the frame or <b>`pop_data.tail()`</b> to see the last five rows.

By typing <b>`pop_data`</b> in a command cell and run it, you can display on the screen the entire data frame.

Try them in the command cell below



```python
pop_data.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>State</th>
      <th>Male</th>
      <th>Female</th>
      <th>Total</th>
      <th>NofBirths</th>
      <th>N.OfDeaths</th>
      <th>NOM_A</th>
      <th>NOM_D</th>
      <th>NOM-Rate</th>
      <th>Natural-Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015</td>
      <td>NSW</td>
      <td>3805197</td>
      <td>3866402</td>
      <td>7671599</td>
      <td>96808</td>
      <td>53075</td>
      <td>168727</td>
      <td>100291</td>
      <td>0.90</td>
      <td>0.58</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>VIC</td>
      <td>2964694</td>
      <td>3033229</td>
      <td>5997923</td>
      <td>74097</td>
      <td>40944</td>
      <td>133990</td>
      <td>73374</td>
      <td>1.03</td>
      <td>0.56</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015</td>
      <td>QLD</td>
      <td>2390891</td>
      <td>2416995</td>
      <td>4807886</td>
      <td>61688</td>
      <td>29496</td>
      <td>81045</td>
      <td>61739</td>
      <td>0.41</td>
      <td>0.68</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015</td>
      <td>SA</td>
      <td>843150</td>
      <td>859536</td>
      <td>1702686</td>
      <td>19546</td>
      <td>13497</td>
      <td>22665</td>
      <td>12550</td>
      <td>0.60</td>
      <td>0.36</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>WA</td>
      <td>1313474</td>
      <td>1289899</td>
      <td>2603373</td>
      <td>35183</td>
      <td>14582</td>
      <td>53917</td>
      <td>39688</td>
      <td>0.55</td>
      <td>0.80</td>
    </tr>
  </tbody>
</table>
</div>



As you can see, after reading the file, **`pandas`** organised the data into a spreadsheet, very similar to what you could see in a program like Excel. This structure is called **_`DataFrame`_** and it can contain numerical data, letters, words.

If you want to know the value stored in a particular column, you can type **`your_dataframe['column name']`**. It is important that you enclose the column names into single quotes, as they are string variable (if you don't, you will receive a **`NameError`**>)

Let's consider you want to know how many people lived in each state from 2013 to 2015, regardless their gender. The data are stored in the column `Total` in our data frame **`pop_data`**. So, if we want see all the data in this column, we can type **`pop_data['Total']`** in the cell below and run it


```python
pop_data['Total']
```




    0      7671599
    1      5997923
    2      4807886
    3      1702686
    4      2603373
    5       517374
    6       243875
    7       393104
    8      7568179
    9      5891105
    10     4748062
    11     1691489
    12     2572856
    13      515350
    14      242939
    15      387866
    16     7459562
    17     5784777
    18     4685080
    19     1676671
    20     2536368
    21      513948
    22      242840
    23      383310
    24     7356850
    25     5680502
    26     4608886
    27     1662197
    28     2479506
    29      512475
    30      239294
    31      377927
    32     7261592
    33     5582670
    34     4518605
    35     1646951
    36     2391592
    37      511944
    38      232703
    39      371108
    40    23941062
    41    23621064
    42    23285739
    43    22920798
    44    22520298
    Name: Total, dtype: int64



The code's output consists of two columns: the first shows the position, or index, for each value and the second shows the values stored in the column.  For example, you read the output as: "the first element (index 0) of the column <b>`Total`</b> is 7671599; the second one (index 1) has value 5997923" and so on, until the end.
In general, you can always access to each value in your data set by indicating the column name and the index (or position) of the element you are interested in.

An important feature of all <b>`DataFrame`</b> objects is that there are several build-in functions (called *methods*) that allow you to access your data more easily, to create data subsample or to perform simple statistical analysis. For example, if you want to know the sum of all the data in the <b>`Male`</b> column, you can type <b>`pop_data['Male'].sum()`</b>.

These methods are automatically imported with <b>pandas</b> and associated to a <b>`DataFrame`</b> as soon as it is created. To have a complete list of all the methods associates with your data frame, you can use the `tab` completion feature (write your data frame followed by a dot and press *Tab* on your keyboard) and a window will show you all the available method.



### Problem: which State had the highest number of females and when?

<img src="Census2015_gender.png"  align="right" alt='Number of male and female citizens in each state.'/>

To understand the social dynamics of Australia, it is important to understand its population composition. This is the description of a population by characteristics such as age or gender. In addition, studying the ratio between women and man in a state or territory can be valuable for marketing as well. In the last year, several company invested into <b>shopping behaviour analysis</b> to understand how they can increase their sales (if you want know more about this topic, read [this article](http://www.nytimes.com/2012/02/19/magazine/shopping-habits.html?ref=general&src=me&pagewanted=all&_r=0) from the New York Times).  show that men and women are different buyer, both because they need different goods and because they are just different shopper (see for example [this article](http://www.moneycrashers.com/men-vs-women-shopping-habits-buying-decisions/)).

Demographic data provide information about the population distribution by gender and they can be used, for example, to target the market in different states and territories.

The figure above shows the gender distribution and the total population in each state for the year 2015. Although in this tutorial we will not use any plotting library as this will be the topic of the next tutorial, this image is a good example of the kind of analysis you can do with Python.

What we are trying to do here, is to identify the state with the highest number of female citizens. In our data frame, <b>`pop_data`</b>, the number of female Australians is stored in the  <b>`pop_data['Female']`</b>. So, the first things to do is to identify the position, or index, of the maximum values of <b>`pop_data['Female']`</b> and then, we can identify the state or territory (<b>`pop_data['State']`</b>) that correspond to that position.

In Pandas, the module <b>`.idxmax()`</b> allows you to identify the position of the maximum value. Remember that it does not return the actual value of the maximum, but only its position in the data frame.

<i>(Note: the position of the minimum value can be found using <b>`.idxmin()`</b>)</i>


An example is provided in the cell below:



```python
# your_dataframe[col_name].idxmax() returns the position of the max values in that columns
indx = pop_data['Female'].idxmax()
#indx is equal to the position of the maximum values
# we can use this to print the corresponding State
pop_data['State'][indx]
```




    'AUS'



Once you have identified the position of the maximum values of a column, you can display all the information in the data frame corresponding at its position. For example, the method `.ix[indx]` to access to all the information at the position `indx`, as found in the cell above:

<b>Important: you must use square bracket for .ix[index]</b>



```python
pop_data.ix[indx]
```




    Year                2015
    State                AUS
    Male            11900650
    Female          12040412
    Total           23941062
    NofBirths         302465
    N.OfDeaths        159191
    NOM_A             478650
    NOM_D             301926
    NOM-Rate            0.75
    Natural-Rate        0.61
    Name: 40, dtype: object



The output of the code above is all the information corresponding to the highest number of female citizens.

### Problem: Summary Statistics of a database

When you are dealing with large data frame, it might be useful to get information about the statistics of your data. For example, how many data points you have, the mean of your numerical data and its standard deviation and so on. In Pandas, that can be quickly done using <b>`.describe()`</b> method. For a generic data frame, <b>`your_df`</b>, you can type <b>`your_df.describe()`</b> for the statistics of the data frame as whole or <b>`your_df[`Column Name`].describe()`</b> for a column (*note: the column needs to be numerical, it must contain only number).

The output will be a table that contains:
* count: the number of data points
* mean: the mean of all the numerical data
* std: standard deviation
* min: the minimum value in each column.
Note this is the actual minimum value and no its position)
* 25%, 50%,75% [percentile](https://en.wikipedia.org/wiki/Percentile)

In the cell below, display the summary statistics of <b>`pop_data`</b>.


```python
pop_data.describe()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>Male</th>
      <th>Female</th>
      <th>Total</th>
      <th>NofBirths</th>
      <th>N.OfDeaths</th>
      <th>NOM_A</th>
      <th>NOM_D</th>
      <th>NOM-Rate</th>
      <th>Natural-Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>count</th>
      <td>45.000000</td>
      <td>4.500000e+01</td>
      <td>4.500000e+01</td>
      <td>4.500000e+01</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
      <td>45.000000</td>
    </tr>
    <tr>
      <th>mean</th>
      <td>2013.000000</td>
      <td>2.570591e+06</td>
      <td>2.597454e+06</td>
      <td>5.168044e+06</td>
      <td>68220.288889</td>
      <td>33656.666667</td>
      <td>106018.533333</td>
      <td>61363.488889</td>
      <td>0.797556</td>
      <td>0.726222</td>
    </tr>
    <tr>
      <th>std</th>
      <td>1.430194</td>
      <td>3.440740e+06</td>
      <td>3.480199e+06</td>
      <td>6.920911e+06</td>
      <td>91335.212592</td>
      <td>45246.942153</td>
      <td>142929.827769</td>
      <td>82941.769041</td>
      <td>0.441599</td>
      <td>0.265966</td>
    </tr>
    <tr>
      <th>min</th>
      <td>2011.000000</td>
      <td>1.221910e+05</td>
      <td>1.105120e+05</td>
      <td>2.327030e+05</td>
      <td>3932.000000</td>
      <td>1009.000000</td>
      <td>3479.000000</td>
      <td>2396.000000</td>
      <td>0.210000</td>
      <td>0.200000</td>
    </tr>
    <tr>
      <th>25%</th>
      <td>2012.000000</td>
      <td>2.554480e+05</td>
      <td>2.570270e+05</td>
      <td>5.124750e+05</td>
      <td>5877.000000</td>
      <td>4417.000000</td>
      <td>8308.000000</td>
      <td>5810.000000</td>
      <td>0.550000</td>
      <td>0.580000</td>
    </tr>
    <tr>
      <th>50%</th>
      <td>2013.000000</td>
      <td>1.281937e+06</td>
      <td>1.254431e+06</td>
      <td>2.536368e+06</td>
      <td>34554.000000</td>
      <td>13497.000000</td>
      <td>70623.000000</td>
      <td>39637.000000</td>
      <td>0.750000</td>
      <td>0.700000</td>
    </tr>
    <tr>
      <th>75%</th>
      <td>2014.000000</td>
      <td>2.911956e+06</td>
      <td>2.979149e+06</td>
      <td>5.891105e+06</td>
      <td>76299.000000</td>
      <td>38225.000000</td>
      <td>125794.000000</td>
      <td>68159.000000</td>
      <td>0.930000</td>
      <td>0.850000</td>
    </tr>
    <tr>
      <th>max</th>
      <td>2015.000000</td>
      <td>1.190065e+07</td>
      <td>1.204041e+07</td>
      <td>2.394106e+07</td>
      <td>312244.000000</td>
      <td>159191.000000</td>
      <td>493089.000000</td>
      <td>301926.000000</td>
      <td>2.350000</td>
      <td>1.310000</td>
    </tr>
  </tbody>
</table>
</div>



### Create a column and do some calculations

But what if we want to obtain the women percentage. We could do some calculations in order to do so, but maybe we want to store the calculations within our dataframe as a different column. A way to do this is calling our dataframe `pop_data` and naming a new column `women_per`. Thus, `women_per` may be calculated by dividing the `Female` column by the `Total` column and then multiplying the result by 100.

Here is an example. You can use the same approach (`df['new name']`)for all new columns that you want to make in a data frame *df*.


```python
pop_data['women_per'] = 100 * pop_data['Female'] / pop_data['Total']
pop_data
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>State</th>
      <th>Male</th>
      <th>Female</th>
      <th>Total</th>
      <th>NofBirths</th>
      <th>N.OfDeaths</th>
      <th>NOM_A</th>
      <th>NOM_D</th>
      <th>NOM-Rate</th>
      <th>Natural-Rate</th>
      <th>women_per</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015</td>
      <td>NSW</td>
      <td>3805197</td>
      <td>3866402</td>
      <td>7671599</td>
      <td>96808</td>
      <td>53075</td>
      <td>168727</td>
      <td>100291</td>
      <td>0.90</td>
      <td>0.58</td>
      <td>50.398906</td>
    </tr>
    <tr>
      <th>1</th>
      <td>2015</td>
      <td>VIC</td>
      <td>2964694</td>
      <td>3033229</td>
      <td>5997923</td>
      <td>74097</td>
      <td>40944</td>
      <td>133990</td>
      <td>73374</td>
      <td>1.03</td>
      <td>0.56</td>
      <td>50.571323</td>
    </tr>
    <tr>
      <th>2</th>
      <td>2015</td>
      <td>QLD</td>
      <td>2390891</td>
      <td>2416995</td>
      <td>4807886</td>
      <td>61688</td>
      <td>29496</td>
      <td>81045</td>
      <td>61739</td>
      <td>0.41</td>
      <td>0.68</td>
      <td>50.271471</td>
    </tr>
    <tr>
      <th>3</th>
      <td>2015</td>
      <td>SA</td>
      <td>843150</td>
      <td>859536</td>
      <td>1702686</td>
      <td>19546</td>
      <td>13497</td>
      <td>22665</td>
      <td>12550</td>
      <td>0.60</td>
      <td>0.36</td>
      <td>50.481181</td>
    </tr>
    <tr>
      <th>4</th>
      <td>2015</td>
      <td>WA</td>
      <td>1313474</td>
      <td>1289899</td>
      <td>2603373</td>
      <td>35183</td>
      <td>14582</td>
      <td>53917</td>
      <td>39688</td>
      <td>0.55</td>
      <td>0.80</td>
      <td>49.547222</td>
    </tr>
    <tr>
      <th>5</th>
      <td>2015</td>
      <td>TAS</td>
      <td>257543</td>
      <td>259831</td>
      <td>517374</td>
      <td>5629</td>
      <td>4603</td>
      <td>3828</td>
      <td>2751</td>
      <td>0.21</td>
      <td>0.20</td>
      <td>50.221117</td>
    </tr>
    <tr>
      <th>6</th>
      <td>2015</td>
      <td>NT</td>
      <td>128582</td>
      <td>115293</td>
      <td>243875</td>
      <td>4028</td>
      <td>1182</td>
      <td>5938</td>
      <td>5116</td>
      <td>0.34</td>
      <td>1.17</td>
      <td>47.275448</td>
    </tr>
    <tr>
      <th>7</th>
      <td>2015</td>
      <td>ACT</td>
      <td>195006</td>
      <td>198098</td>
      <td>393104</td>
      <td>5456</td>
      <td>1804</td>
      <td>8535</td>
      <td>6414</td>
      <td>0.55</td>
      <td>0.94</td>
      <td>50.393280</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2014</td>
      <td>NSW</td>
      <td>3752884</td>
      <td>3815295</td>
      <td>7568179</td>
      <td>97798</td>
      <td>52377</td>
      <td>162288</td>
      <td>93520</td>
      <td>0.92</td>
      <td>0.61</td>
      <td>50.412325</td>
    </tr>
    <tr>
      <th>9</th>
      <td>2014</td>
      <td>VIC</td>
      <td>2911956</td>
      <td>2979149</td>
      <td>5891105</td>
      <td>77582</td>
      <td>38225</td>
      <td>125794</td>
      <td>68159</td>
      <td>1.00</td>
      <td>0.68</td>
      <td>50.570292</td>
    </tr>
    <tr>
      <th>10</th>
      <td>2014</td>
      <td>QLD</td>
      <td>2363191</td>
      <td>2384871</td>
      <td>4748062</td>
      <td>63690</td>
      <td>28737</td>
      <td>81700</td>
      <td>59269</td>
      <td>0.48</td>
      <td>0.75</td>
      <td>50.228304</td>
    </tr>
    <tr>
      <th>11</th>
      <td>2014</td>
      <td>SA</td>
      <td>837692</td>
      <td>853797</td>
      <td>1691489</td>
      <td>20533</td>
      <td>13381</td>
      <td>22737</td>
      <td>12327</td>
      <td>0.62</td>
      <td>0.43</td>
      <td>50.476060</td>
    </tr>
    <tr>
      <th>12</th>
      <td>2014</td>
      <td>WA</td>
      <td>1298965</td>
      <td>1273891</td>
      <td>2572856</td>
      <td>35386</td>
      <td>13736</td>
      <td>56564</td>
      <td>41326</td>
      <td>0.60</td>
      <td>0.85</td>
      <td>49.512720</td>
    </tr>
    <tr>
      <th>13</th>
      <td>2014</td>
      <td>TAS</td>
      <td>256604</td>
      <td>258746</td>
      <td>515350</td>
      <td>5877</td>
      <td>4457</td>
      <td>3913</td>
      <td>2653</td>
      <td>0.25</td>
      <td>0.28</td>
      <td>50.207820</td>
    </tr>
    <tr>
      <th>14</th>
      <td>2014</td>
      <td>NT</td>
      <td>128311</td>
      <td>114628</td>
      <td>242939</td>
      <td>3964</td>
      <td>1172</td>
      <td>5846</td>
      <td>5147</td>
      <td>0.29</td>
      <td>1.15</td>
      <td>47.183861</td>
    </tr>
    <tr>
      <th>15</th>
      <td>2014</td>
      <td>ACT</td>
      <td>192425</td>
      <td>195441</td>
      <td>387866</td>
      <td>5631</td>
      <td>1837</td>
      <td>8536</td>
      <td>6226</td>
      <td>0.60</td>
      <td>0.99</td>
      <td>50.388794</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2013</td>
      <td>NSW</td>
      <td>3700139</td>
      <td>3759423</td>
      <td>7459562</td>
      <td>97213</td>
      <td>50111</td>
      <td>162254</td>
      <td>95425</td>
      <td>0.91</td>
      <td>0.64</td>
      <td>50.397369</td>
    </tr>
    <tr>
      <th>17</th>
      <td>2013</td>
      <td>VIC</td>
      <td>2859599</td>
      <td>2925178</td>
      <td>5784777</td>
      <td>76231</td>
      <td>36609</td>
      <td>122915</td>
      <td>65790</td>
      <td>1.01</td>
      <td>0.70</td>
      <td>50.566824</td>
    </tr>
    <tr>
      <th>18</th>
      <td>2013</td>
      <td>QLD</td>
      <td>2334169</td>
      <td>2350911</td>
      <td>4685080</td>
      <td>63430</td>
      <td>27982</td>
      <td>91863</td>
      <td>58014</td>
      <td>0.73</td>
      <td>0.77</td>
      <td>50.178674</td>
    </tr>
    <tr>
      <th>19</th>
      <td>2013</td>
      <td>SA</td>
      <td>830427</td>
      <td>846244</td>
      <td>1676671</td>
      <td>19924</td>
      <td>12842</td>
      <td>23381</td>
      <td>12045</td>
      <td>0.68</td>
      <td>0.43</td>
      <td>50.471679</td>
    </tr>
    <tr>
      <th>20</th>
      <td>2013</td>
      <td>WA</td>
      <td>1281937</td>
      <td>1254431</td>
      <td>2536368</td>
      <td>34554</td>
      <td>13478</td>
      <td>70623</td>
      <td>39637</td>
      <td>1.25</td>
      <td>0.85</td>
      <td>49.457768</td>
    </tr>
    <tr>
      <th>21</th>
      <td>2013</td>
      <td>TAS</td>
      <td>256043</td>
      <td>257905</td>
      <td>513948</td>
      <td>6080</td>
      <td>4417</td>
      <td>3786</td>
      <td>2516</td>
      <td>0.25</td>
      <td>0.32</td>
      <td>50.181147</td>
    </tr>
    <tr>
      <th>22</th>
      <td>2013</td>
      <td>NT</td>
      <td>128393</td>
      <td>114447</td>
      <td>242840</td>
      <td>4025</td>
      <td>1089</td>
      <td>7047</td>
      <td>4213</td>
      <td>1.18</td>
      <td>1.23</td>
      <td>47.128562</td>
    </tr>
    <tr>
      <th>23</th>
      <td>2013</td>
      <td>ACT</td>
      <td>190372</td>
      <td>192938</td>
      <td>383310</td>
      <td>5558</td>
      <td>1718</td>
      <td>8175</td>
      <td>6254</td>
      <td>0.51</td>
      <td>1.02</td>
      <td>50.334716</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2012</td>
      <td>NSW</td>
      <td>3651443</td>
      <td>3705407</td>
      <td>7356850</td>
      <td>101013</td>
      <td>50867</td>
      <td>150099</td>
      <td>88189</td>
      <td>0.85</td>
      <td>0.69</td>
      <td>50.366760</td>
    </tr>
    <tr>
      <th>25</th>
      <td>2012</td>
      <td>VIC</td>
      <td>2809865</td>
      <td>2870637</td>
      <td>5680502</td>
      <td>76299</td>
      <td>36536</td>
      <td>116119</td>
      <td>60385</td>
      <td>1.00</td>
      <td>0.71</td>
      <td>50.534918</td>
    </tr>
    <tr>
      <th>26</th>
      <td>2012</td>
      <td>QLD</td>
      <td>2298358</td>
      <td>2310528</td>
      <td>4608886</td>
      <td>64557</td>
      <td>28120</td>
      <td>95180</td>
      <td>51560</td>
      <td>0.97</td>
      <td>0.81</td>
      <td>50.132028</td>
    </tr>
    <tr>
      <th>27</th>
      <td>2012</td>
      <td>SA</td>
      <td>823330</td>
      <td>838867</td>
      <td>1662197</td>
      <td>20514</td>
      <td>13145</td>
      <td>22371</td>
      <td>11456</td>
      <td>0.66</td>
      <td>0.45</td>
      <td>50.467363</td>
    </tr>
    <tr>
      <th>28</th>
      <td>2012</td>
      <td>WA</td>
      <td>1254425</td>
      <td>1225081</td>
      <td>2479506</td>
      <td>34112</td>
      <td>13292</td>
      <td>88496</td>
      <td>32205</td>
      <td>2.35</td>
      <td>0.87</td>
      <td>49.408269</td>
    </tr>
    <tr>
      <th>29</th>
      <td>2012</td>
      <td>TAS</td>
      <td>255448</td>
      <td>257027</td>
      <td>512475</td>
      <td>6191</td>
      <td>4485</td>
      <td>3691</td>
      <td>2429</td>
      <td>0.25</td>
      <td>0.33</td>
      <td>50.154056</td>
    </tr>
    <tr>
      <th>30</th>
      <td>2012</td>
      <td>NT</td>
      <td>126228</td>
      <td>113066</td>
      <td>239294</td>
      <td>4048</td>
      <td>1009</td>
      <td>8308</td>
      <td>3617</td>
      <td>2.02</td>
      <td>1.31</td>
      <td>47.249827</td>
    </tr>
    <tr>
      <th>31</th>
      <td>2012</td>
      <td>ACT</td>
      <td>187865</td>
      <td>190062</td>
      <td>377927</td>
      <td>5476</td>
      <td>1722</td>
      <td>8825</td>
      <td>5810</td>
      <td>0.81</td>
      <td>1.01</td>
      <td>50.290665</td>
    </tr>
    <tr>
      <th>32</th>
      <td>2011</td>
      <td>NSW</td>
      <td>3605612</td>
      <td>3655980</td>
      <td>7261592</td>
      <td>98799</td>
      <td>50177</td>
      <td>146230</td>
      <td>90243</td>
      <td>0.78</td>
      <td>0.68</td>
      <td>50.346811</td>
    </tr>
    <tr>
      <th>33</th>
      <td>2011</td>
      <td>VIC</td>
      <td>2761846</td>
      <td>2820824</td>
      <td>5582670</td>
      <td>72907</td>
      <td>36313</td>
      <td>109518</td>
      <td>59207</td>
      <td>0.92</td>
      <td>0.67</td>
      <td>50.528224</td>
    </tr>
    <tr>
      <th>34</th>
      <td>2011</td>
      <td>QLD</td>
      <td>2254270</td>
      <td>2264335</td>
      <td>4518605</td>
      <td>62774</td>
      <td>27819</td>
      <td>90456</td>
      <td>50144</td>
      <td>0.91</td>
      <td>0.79</td>
      <td>50.111373</td>
    </tr>
    <tr>
      <th>35</th>
      <td>2011</td>
      <td>SA</td>
      <td>815548</td>
      <td>831403</td>
      <td>1646951</td>
      <td>20197</td>
      <td>12696</td>
      <td>20816</td>
      <td>10772</td>
      <td>0.62</td>
      <td>0.46</td>
      <td>50.481344</td>
    </tr>
    <tr>
      <th>36</th>
      <td>2011</td>
      <td>WA</td>
      <td>1205454</td>
      <td>1186138</td>
      <td>2391592</td>
      <td>32332</td>
      <td>12739</td>
      <td>72451</td>
      <td>28562</td>
      <td>1.89</td>
      <td>0.84</td>
      <td>49.596169</td>
    </tr>
    <tr>
      <th>37</th>
      <td>2011</td>
      <td>TAS</td>
      <td>255044</td>
      <td>256900</td>
      <td>511944</td>
      <td>6562</td>
      <td>4262</td>
      <td>3479</td>
      <td>2396</td>
      <td>0.21</td>
      <td>0.45</td>
      <td>50.181270</td>
    </tr>
    <tr>
      <th>38</th>
      <td>2011</td>
      <td>NT</td>
      <td>122191</td>
      <td>110512</td>
      <td>232703</td>
      <td>3932</td>
      <td>1023</td>
      <td>5367</td>
      <td>3695</td>
      <td>0.73</td>
      <td>1.26</td>
      <td>47.490578</td>
    </tr>
    <tr>
      <th>39</th>
      <td>2011</td>
      <td>ACT</td>
      <td>184519</td>
      <td>186589</td>
      <td>371108</td>
      <td>5254</td>
      <td>1703</td>
      <td>7929</td>
      <td>5560</td>
      <td>0.65</td>
      <td>0.97</td>
      <td>50.278895</td>
    </tr>
    <tr>
      <th>40</th>
      <td>2015</td>
      <td>AUS</td>
      <td>11900650</td>
      <td>12040412</td>
      <td>23941062</td>
      <td>302465</td>
      <td>159191</td>
      <td>478650</td>
      <td>301926</td>
      <td>0.75</td>
      <td>0.61</td>
      <td>50.291888</td>
    </tr>
    <tr>
      <th>41</th>
      <td>2014</td>
      <td>AUS</td>
      <td>11744121</td>
      <td>11876943</td>
      <td>23621064</td>
      <td>310494</td>
      <td>153929</td>
      <td>467390</td>
      <td>288630</td>
      <td>0.77</td>
      <td>0.67</td>
      <td>50.281152</td>
    </tr>
    <tr>
      <th>42</th>
      <td>2013</td>
      <td>AUS</td>
      <td>11583154</td>
      <td>11702585</td>
      <td>23285739</td>
      <td>307044</td>
      <td>148253</td>
      <td>490045</td>
      <td>283895</td>
      <td>0.90</td>
      <td>0.69</td>
      <td>50.256447</td>
    </tr>
    <tr>
      <th>43</th>
      <td>2012</td>
      <td>AUS</td>
      <td>11409025</td>
      <td>11511773</td>
      <td>22920798</td>
      <td>312244</td>
      <td>149180</td>
      <td>493089</td>
      <td>255653</td>
      <td>1.05</td>
      <td>0.72</td>
      <td>50.224137</td>
    </tr>
    <tr>
      <th>44</th>
      <td>2011</td>
      <td>AUS</td>
      <td>11206535</td>
      <td>11313763</td>
      <td>22520298</td>
      <td>302788</td>
      <td>146738</td>
      <td>456258</td>
      <td>250579</td>
      <td>0.93</td>
      <td>0.70</td>
      <td>50.238070</td>
    </tr>
  </tbody>
</table>
</div>



### Create a Subset of your data: Analysis of NSW population

Let's consider we are interested in the population of a single state only, for example the New South Wales, so that we can study the population growth in this state between 2011 and 2015 as described by the figure below.

<img src="Population_growthNSW.png"  align="left"/>


The first step is to select all the data relative to the NSW between 2013 and 2015. The easiest approach is to create a new data frame, named for example `df_nsw` , that contains only the information we are interested in.
In **pandas**, the module **`.query('expression')`** allows you to select in data frame only the data that satisfy a given condition. Such a condition is in the *`expression`*. The usage of this method is:
<center><strong>your_df.query(<italic>'expression'</italic>)</center></strong>
example, as we want only the information about the NSW we can write:
<center><strong>df_nsw=pop_data.query( 'State == "NSW"')</center></strong>

The `expression: 'State == "NSW"' ` allows you to select data based on the condition that the column `pop_data['State']` is exactly `'NSW'`.

There are two important point that you need to remember. The *expression* need to be between single quote, `' '`,as it needs to be a string. When you compare words, as
in this case, you need to add extra double quotes ( <FONT color='red'>'</FONT>State == <FONT color='red'>"</FONT>NSW<FONT color='red'>" '</FONT>).



```python
df_nsw = pop_data.query('State == "NSW"')
df_nsw.head()
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>State</th>
      <th>Male</th>
      <th>Female</th>
      <th>Total</th>
      <th>NofBirths</th>
      <th>N.OfDeaths</th>
      <th>NOM_A</th>
      <th>NOM_D</th>
      <th>NOM-Rate</th>
      <th>Natural-Rate</th>
      <th>women_per</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>0</th>
      <td>2015</td>
      <td>NSW</td>
      <td>3805197</td>
      <td>3866402</td>
      <td>7671599</td>
      <td>96808</td>
      <td>53075</td>
      <td>168727</td>
      <td>100291</td>
      <td>0.90</td>
      <td>0.58</td>
      <td>50.398906</td>
    </tr>
    <tr>
      <th>8</th>
      <td>2014</td>
      <td>NSW</td>
      <td>3752884</td>
      <td>3815295</td>
      <td>7568179</td>
      <td>97798</td>
      <td>52377</td>
      <td>162288</td>
      <td>93520</td>
      <td>0.92</td>
      <td>0.61</td>
      <td>50.412325</td>
    </tr>
    <tr>
      <th>16</th>
      <td>2013</td>
      <td>NSW</td>
      <td>3700139</td>
      <td>3759423</td>
      <td>7459562</td>
      <td>97213</td>
      <td>50111</td>
      <td>162254</td>
      <td>95425</td>
      <td>0.91</td>
      <td>0.64</td>
      <td>50.397369</td>
    </tr>
    <tr>
      <th>24</th>
      <td>2012</td>
      <td>NSW</td>
      <td>3651443</td>
      <td>3705407</td>
      <td>7356850</td>
      <td>101013</td>
      <td>50867</td>
      <td>150099</td>
      <td>88189</td>
      <td>0.85</td>
      <td>0.69</td>
      <td>50.366760</td>
    </tr>
    <tr>
      <th>32</th>
      <td>2011</td>
      <td>NSW</td>
      <td>3605612</td>
      <td>3655980</td>
      <td>7261592</td>
      <td>98799</td>
      <td>50177</td>
      <td>146230</td>
      <td>90243</td>
      <td>0.78</td>
      <td>0.68</td>
      <td>50.346811</td>
    </tr>
  </tbody>
</table>
</div>



Note that the first column show the index (position) that the data had in the original data set. This means that if you want access to the NSW total residents for the 2014 you can use index 8 (and no 1). So, for example `df_nsw['Total'][8]` will display 7568179.
Now that we have all the information about NSW population all in one place, we can study it in more details.

An important skill in data analysis is to be able to make prediction about your next data set. For example, `df_nsw`, as well as `pop_data`, only contains data until 2015.
#### So, what will be the total number of NSW residents in 2016?

To make such prediction we need to calculate the **annual growth rate**. This is simple the percentage growth of an initial population over a given numbers of year. Since we have data from 2011 until 2015, we can consider the 2011 population an initial population and the 2015 one as the final. So, that the **growth rate** (**gr**) is given by

$$gr=\frac{(p_{2015}-p_{2011})}{p_{2011}}$$

once we know the percentage growth we can calculate the **annual percentage growth rate** (**apg**) that is

$$agr=\frac{gr}{N_{years}}$$

where $N_{years}$ is the number of years elapsed.
In the two cell below there is the code to do these calculations.



```python
#growth rate from 2011 (df_nsw['Total'][32]) to 2015 (df_nsw['Total'][0])
gr = (df_nsw['Total'][0] - df_nsw['Total'][32]) / df_nsw['Total'][32]
#annual growth rate
N_year = 5
agr= gr/N_year
```


By re-arranging the two equations above, we can make any prediction over different years. For example, being $p_x$ the unknown population and $p_i$ the initial one, $p_x$ is equal to:

$$p_x=agr*N_{years}*p_i+p_i$$

We can consider the 2015 population as $p_i$ and as we want the population in 2016, $N_year=1$

So, the final piece of code is:


```python
N_year = 1
p2016 = agr * N_year * df_nsw['Total'][0] + df_nsw['Total'][0]
print("Estimated NSW population 2016 is", round(p2016))
```

    Estimated NSW population 2016 is 7758230.0


In the code below, the function `round()` just round a number to a given precision (by default, to 0 digits). Type help(round) in a command cell to know more about this function.

If you have a look at the Australia Demographic Statistic website, at the end of 2016 the NSW population was 7758000 as you can see [here](http://www.abs.gov.au/ausstats/abs@.nsf/mf/3101.0). So, our prediction is accurate enough.

<div style="background-color:LAVENDER", text-align='justify'>
<h2> <center><FONT COLOR="Purple"> Practical Session </FONT> </center></h2>
</div>
*This session is designed to help you revise the content of this tutorial. Below the cell where you put your answer for each question there is a Checkpoint cell. Follow the instructions in the Checkpoint cell to check your answer and receive some feedback*.

### Question 1

Write code to calculate the percentage of men and women in Australia.

Create a subsample of the original data frame that collects all the information relative to the entire Australia.

Your code should:
* Import pandas function
* Read the file `AustraliaDemographics.dat` into a data frame
* Create a subsample called **`df_aus`** that contains only the data relative to Australia
* Calculate the percentage of men and women _as a ratio_  (it should be a number between 0 and 1. For example, 85% is equivalent to 0.85)


```python
# WRITE YOUR CODE HERE

import pandas as pd
pop_data = pd.read_table('AustraliaDemographics.dat', sep = ' ')
df_aus = pop_data.query('State =="AUS"')

perc_men = df_aus['Male'] /df_aus['Total']
perc_female = df_aus['Female'] / df_aus['Total']
```


```python
# TO CHECK YOUR SOLUTIONS YOU NEED:
#   1) Import the solution library (import solution)
#   2) solution.q1(your_dataframe, your_male_percentage,your_female_percentage)
#    please note the order of your answers is important
import solution
solution.q1(df_aus, perc_men, perc_female)
```




    'Your dataframe is correct. Your male population percentage is correct: since 2011, the Australias male population has been ~40% Your female population percentage is correct.'



### Question 2

Using your data frame for the only Australia data, make a prediction for the Australia population for the 2022.

***Hint***: *remember to check the position of each data in your data frame will be the same in the original data frame. Keep this in mind when calculating the annual growth rate. Print your df_aus data frame to see at which year the data correspond to*



```python
df_aus
```




<div>
<table border="1" class="dataframe">
  <thead>
    <tr style="text-align: right;">
      <th></th>
      <th>Year</th>
      <th>State</th>
      <th>Male</th>
      <th>Female</th>
      <th>Total</th>
      <th>NofBirths</th>
      <th>N.OfDeaths</th>
      <th>NOM_A</th>
      <th>NOM_D</th>
      <th>NOM-Rate</th>
      <th>Natural-Rate</th>
    </tr>
  </thead>
  <tbody>
    <tr>
      <th>40</th>
      <td>2015</td>
      <td>AUS</td>
      <td>11900650</td>
      <td>12040412</td>
      <td>23941062</td>
      <td>302465</td>
      <td>159191</td>
      <td>478650</td>
      <td>301926</td>
      <td>0.75</td>
      <td>0.61</td>
    </tr>
    <tr>
      <th>41</th>
      <td>2014</td>
      <td>AUS</td>
      <td>11744121</td>
      <td>11876943</td>
      <td>23621064</td>
      <td>310494</td>
      <td>153929</td>
      <td>467390</td>
      <td>288630</td>
      <td>0.77</td>
      <td>0.67</td>
    </tr>
    <tr>
      <th>42</th>
      <td>2013</td>
      <td>AUS</td>
      <td>11583154</td>
      <td>11702585</td>
      <td>23285739</td>
      <td>307044</td>
      <td>148253</td>
      <td>490045</td>
      <td>283895</td>
      <td>0.90</td>
      <td>0.69</td>
    </tr>
    <tr>
      <th>43</th>
      <td>2012</td>
      <td>AUS</td>
      <td>11409025</td>
      <td>11511773</td>
      <td>22920798</td>
      <td>312244</td>
      <td>149180</td>
      <td>493089</td>
      <td>255653</td>
      <td>1.05</td>
      <td>0.72</td>
    </tr>
    <tr>
      <th>44</th>
      <td>2011</td>
      <td>AUS</td>
      <td>11206535</td>
      <td>11313763</td>
      <td>22520298</td>
      <td>302788</td>
      <td>146738</td>
      <td>456258</td>
      <td>250579</td>
      <td>0.93</td>
      <td>0.70</td>
    </tr>
  </tbody>
</table>
</div>



```python
# WRITE YOUR CODE HERE
yearmin_id = df_aus['Year'].idxmin()
yearmax_id = df_aus['Year'].idxmax()

gr = ((df_aus.ix[yearmax_id]['Total'] - df_aus.ix[yearmin_id]['Total']) / df_aus.ix[yearmin_id]['Total'])

#annual growth rate
N_year = 5.
agr = gr / N_year
print(agr)

N_year = 2022 - 2015
p2022 = agr * N_year * df_aus.ix[yearmax_id]['Total'] + df_aus.ix[yearmax_id]['Total']
print("Estimated AUS population 2022 is", round(p2022))
```

    0.0126176305482
    Estimated AUS population 2022 is 26055618.0



```python
# TO CHECK YOUR SOLUTIONS YOU NEED:
#   1) Import  the solution library (import solution)
#   2) solution.q2(your_dataframe, your_answer)
solution.q2(df_aus, p2022)
```




    ' This is correct in 7.0 years the Australia population will be26055618.3267'




