**Kate Pollock**

**December 4, 2021**

**Foundations of Programming: Python**

**Assignment08**

**GitHubURL \&lt;** [https://github.com/katepollock/IntroToProg-Python-Mod08](https://github.com/katepollock/IntroToProg-Python-Mod08) **\&gt;**

# **Classes**

#

# Introduction

In Module 8, I learned about classes as a way to group data and functions and objects to access the code in the class. I additionally learned about many of the other major concepts that make up a class such as constructors, setters and getters as well as attributes. I used my new knowledge to modify a script that utilizes a Product class to create product objects with name and price attributes.

#

# Planning my &quot;Product &quot; Script

I began my scripts with a header and the global variable for my text file (_ **See Figure 1** _)

_# ------------------------------------------------------------------------ #
 # Title: Assignment 08
 # Description: Working with classes
 # ChangeLog (Who,When,What):
 # RRoot,1.1.2030,Created started script
 # RRoot,1.1.2030,Added pseudo-code to start assignment 8
 # KPollock,12/3/21, Modified code to complete assignment 8
 # ------------------------------------------------------------------------ #

 # Data -------------------------------------------------------------------- #_ strFileName = **&#39;products.txt&#39;**

_ **Figure 1 – Script Heading and Variable** _

Product Script

My script contains 3 classes: Product, File Processor and Input/Output.

The Product class is displayed below in Figure 2. It has a constructor which automatically runs when I create an object from the class. The constructor has 2 parameters – name and price. I used the key word &#39;self&#39; to indicate an object instance. I used an input from user method as a part of this class to request a name and price and instantiate an object. I used getters and setters for both name and price – raising an exception if the name contains numbers and if the price is not an integer or float. The\_\_str\_\_method overrides the default object and returns the object attributes as strings._ **See Figure 2** _ **.**

**class** Product:
_&quot;&quot;&quot;Stores data about a product:

 properties:
 name: (string) with the products&#39;s name
 price: (float) with the products&#39;s price
 methods:
 str method to change default to product name and product price
 changelog: (When,Who,What)
 RRoot,1.1.2030,Created Class
 KPollock, 12/3/21, Modified code to complete assignment 8
 &quot;&quot;&quot;

 # --Constructor--#_
  **def** \_\_init\_\_(self, name, price):
_# --Attribute--#_
self.name = name
self.price = price

@staticmethod
**def** input\_from\_user():
 name = input( **&#39;What product would you like to add? &#39;** ).replace( **&#39;,&#39;** , **&#39;&#39;** )
 price = input( **&#39;What is the price of the product? &#39;** ).replace( **&#39;,&#39;** , **&#39;&#39;** )
print() _# extra line for looks_
**return** Product(name, float(price))

_# --Properties--#_
@property
**def** name(self): _# getter_
**return** self.\_\_name

@name.setter
**def** name(self, value): _# setter_
**if not** value.isnumeric():
self.\_\_name = value
**else** :
**raise** Exception( **&quot;Names cannot be numbers&quot;** )

@property
**def** price(self): _# getter_
**return** self.\_\_price

@price.setter
**def** price(self, value): _# setter_
**if** type(value) == float **or** type(value) == int:
self.\_\_price = value
**elif** type(value) == str **and** value.isnumeric():
self.\_\_price = float(value)
**else** :
**raise** Exception( **&quot;Price must be a number&quot;** )

_# ---Methods---#_
**def** \_\_str\_\_(self):
**return** self.name + **&#39;,&#39;** + str(self.price)

_ **Figure 2 – Product Class code** _

The file processing class saves data to a text file and reads data from the file. I used the static method as this class is focused on processing data. _ **See Figure 3** _.

_# Processing ------------------------------------------------------------- #_
**class** FileProcessor:
_&quot;&quot;&quot;Processes data to and from a file and a list of product objects:

 methods:
 save\_data\_to\_file(file\_name, list\_of\_product\_objects): --\&gt; return None
 read\_data\_from\_file(file\_name): -\&gt; return (a list of product objects)

 changelog: (When,Who,What)
 RRoot,1.1.2030,Created Class
 KPollock, 12.3.2021, Modified code to complete assignment 8
 &quot;&quot;&quot;_
  @staticmethod
**def** save\_data\_to\_file(file\_name, list\_of\_product\_objects):
_&quot;&quot;&quot; Writes data from the list to the file using csv_
**:param** _list\_of\_product\_objects:_
**:param** _file\_name: (string) with name of file_
**:return** _: list of rows that was written to file
 &quot;&quot;&quot;_ file = open(file\_name, **&quot;wt&quot;** )
**for** product **in** list\_of\_product\_objects:
 file.write(str(product) + **&#39;**** \n ****&#39;** )
 file.close()
**return None**

@staticmethod
**def** read\_data\_from\_file(file\_name):
_&quot;&quot;&quot; Reads data from a file into a list of dictionary rows_
**:param** _file\_name: (string) with name of file_
**:return** _: (list) of product\_objects
 &quot;&quot;&quot;_ list\_of\_product\_objects = [] _# start with empty list_
**try** :
 file = open(file\_name, **&quot;r&quot;** )
**except** FileNotFoundError:
**return** list\_of\_product\_objects

**for** line **in** file:
 name, price = line.strip().split( **&#39;,&#39;** )
 list\_of\_product\_objects.append(Product(name, float(price)))
 file.close()
**return** list\_of\_product\_objects

_ **Figure 3 – File Processing code** _

The IO Class performs methods including printing the menu for the user, prompting input of a menu choice, and displaying the products stored in the list. _ **See Figure 4** _.

_# Presentation (Input/Output) -------------------------------------------- #_
**class** IO:
_&quot;&quot;&quot;Performs input and output tasks:

 methods: print menu, input choice, print current products,
 input new product and price

 changelog: (When,Who,What)
 RRoot,1.1.2030,Created Class
 KPollock, 12.3.2021, Modified code to complete assignment 8
 &quot;&quot;&quot;

 # Presentation (Input/Output) -------------------------------------------- #_
  @staticmethod
**def** print\_menu\_tasks():
_&quot;&quot;&quot; Display a menu of choices to the user_

**:return** _: nothing
 &quot;&quot;&quot;_ print(**&#39;&#39;&#39;
 Menu of Options
 1) Display current data
 2) Add a new Product
 3) Save Data to File and Exit Program
 &#39;&#39;&#39;** )
print() _# Add an extra line for looks_

@staticmethod
**def** input\_menu\_choice():
_&quot;&quot;&quot; Gets the menu choice from a user_

**:return** _: string
 &quot;&quot;&quot;_ choice = input(**&quot;Which option would you like to perform? [1 to 3] - &quot;**).strip()
print() _# Add an extra line for looks_
**return** choice

@staticmethod
**def** print\_current\_products\_in\_list(products):
_&quot;&quot;&quot; Shows the current products in the list of dictionaries rows_

**:param** _products: (list) of products you want to display_
**:return** _: nothing
 &quot;&quot;&quot;_ print( **&quot;\*\*\*\*\*\*\* The Current Products are: \*\*\*\*\*\*\*&quot;** )
**for** product **in** products:
print( **f&#39;**** { **product.name** } **** @ $ ****{** product.price **:****.2f ****}****&#39;**)
print( **&quot;\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*\*&quot;** )
print() _# Add an extra line for looks_

_ **Figure 4 – Input and Output code** _

Main Body of Script

The main body of my script first reads the data from the file to update the list if needed. I then use a series of if-elif statements based on the user choice and call the appropriate methods to display, process the data and save the data to the file (_ **See Figure 5** _).

_# Main Body of Script ---------------------------------------------------- #
 # Load data from file into a list of product objects when script starts
 # Show user a menu of options
 # Get user&#39;s menu option choice
 # Show user current data in the list of product objects
 # Let user add data to the list of product objects
 # let user save current data to file and exit program_ **def** main():
 lstOfProductObjects = FileProcessor.read\_data\_from\_file(strFileName)

**while True** :
 IO.print\_menu\_tasks()
 strChoice = IO.input\_menu\_choice()

**if** strChoice == **&#39;1&#39;** :
 IO.print\_current\_products\_in\_list(lstOfProductObjects)

**elif** strChoice == **&#39;2&#39;** :
 product = Product.input\_from\_user()
 lstOfProductObjects.append(product)
print(product.name, **&quot;has been added!&quot;** )

**elif** strChoice == **&#39;3&#39;** :
 FileProcessor.save\_data\_to\_file(strFileName, lstOfProductObjects)
print( **&#39;Data has been saved. Goodbye!&#39;** )
**break

 else**
  :
print(**&#39;Please enter choices [1 to 3]&#39;**)

 main()

_ **Figure 5 – Main body of script** _

# Results of Script

I ran the code in the command prompt and the results were as expected (_ **Figure 6** _).

![](RackMultipart20211206-4-1gtbxqx_html_d4252197b37d86bf.png)

_ **Figure 6: Output in Command Prompt** _

# Summary

I have written the Python program above by utilizing the new concepts learned in Module 8 of this course. These concepts include classes, objects, methods, and attributes. I&#39;m looking forward to learning about the concept of inheritance next week.
