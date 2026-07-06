# Notes 
Based on Kaggle Intro to Programming course and Python course
## Printing 
```python
print(3)
print("Hello, world)
```
## Arithmetic
General arithemetic operators 
|Operation     | Symbol        |  
|:-----------: |:-------------:|
|Addition      |+              |
|Substarction  |-              |
|Multiplication|*              |
|Division      |/              |
|Exponent      |**             |
|Floor division| //            |
|Modulus       | %             |
|Negation      | -             |

Order of operations : PEMDAS rule 
  1. Parentheses first
  2. Exponents
  3. Multiplications and Division : read from left to right
  4. Addition and Substraction : read from left to right
  5. Floor division : division without fractional parts - always gives int result
  6. Normal division the outcome is always float type

## Comments
"#" in the beginining of phrase
## Variables
Rules:
  1. They can't have spaces
  2. They can only include letters, numbers, and underscores
  3. They have to start with letter or undercsore
By assinging a variable - we assing it globally

* **Swapping variables :**
  ```python
  tmp = a
  a =b
  b = tmp
  ```
  diffrent approach
  ```python
  a, b = b, a
## Functions
Every function is composed of two pieces
  1. Header - Remember, the header of a function ends with ":"
  2. Body - each row has to begin with Tab
```python
  def function_name (args):
      ...
      return 
```
* Function is read from top to bottom
* Use lowercase letters when naming a function
* Variable created inside a function Body can't be accesed outside the function
* ***math.ceil(variable)*** zaokrąglanie w górę
* ***abs()*** returns absolute value of an argument
* ***help(function)*** build-in repository, with definining new functions we can write our own documentation that will be shown after calling help() function - the description called **docstring """** is a triple-quoted string thet comes immediately atfer the header of a function
* if function doesn't have **return** keyword at the end the result of calling them is the spetial value **None** (similar to null)
* in ***print(stirng, sep=' ')*** parameter **sep** allows to put some spetial string in between our printed arguments
* in ***max(... , key=function)*** by default returns the lagest of its arguments. But if we pass in a function using the optional **key** argument, it returns the argument x that maximizes key(x)
*  ***round(... ,ndigits = )*** , when ndigits = -1 it rounds to the nearest 10, when -2 it rounds to nearest 100 and so on... 
## Data Types
  |data type  | expample   |
  |:---------:|:----------:|
  |Integer    |int {-1,0,1}|
  |Float      |float - numbers with fractional parts (liczby zmiennoprzecinkowe) |
  |Bolleans   |bool {True, False}|
  |Strings    |str - collection of chars contained in quatation marks- respesentation of text |
  
 * ***type(variable)*** to verify the data type
 *  ***round(variable, number)*** lets you round a number to a specified number of decimal places
 *  1. 1.0 1.00 will be read as float
 * ***not True == False ,not False == True***
 * Possible to add strings and multiply string by integer
 * to convert float to an integer you use ***int(float)*** Negative floats are always rounded UP to the closest integer. Positive floats are always rounded DOWN to the closest integer.
### Strange cases
 * When you multiply an integer or float by a boolean with vaule ***True***, it returns that same integer or float - equivalent to mmultiplying by 1
 * When you multiply an integer or float by boolean with value ***False***, it always returns 0, equivalent for positive and negative numbers
 * When multiplying string by a bolean with value ***True***, it just returns the same string
 * When multiplying a boolean with vaule ***False***, it returns an empty string - string with leangth zero.
**Wniosek:** Mnożenie liczby przez Boolean może zastąpić nam konstrukcję if(True) ... w sencie:
```python
  gold_plate_cost = 50
  plate_engraving_cost = 7
gold_solid_cost = 100
solid_engraving_cost = 10

  def cost_of_project(engraving, solid_gold):
      cost = solid_gold*(gold_solid_cost+solid_engraving_cost*len(engraving))+(not solid_gold)*(gold_plate_cost+plate_engraving_cost*len(engraving))
      return cost
```
gdzie zmienna engraving jest typu string, a solid_gold przyjmuje typ boolean

## Conditions and Conditional Statements

|Symbol | Meaning|
|:-----:|:------:|
|==     | equals |
|!=     | does not equal |
|<      | less than|
|<=     | less than or qeual to |
|>      | greater than|
|>=     | greater than or equal to|

### Conditional Statements
  * ***if statement :
    ...elif...
    else :***

### Boolean Values
  * ***and*** is logical and operator
  * ***or*** is logical or operator
  * ***not*** is logical negation operator

### Strange Cases
  * Python has a ***bool()*** function which turns things into bools such as:
    ```python
    bool(1) #True
    bool(0) #False
    bool("not empty string") #True
    bool("") #empty string - False

    ```

## Lists
  * To create a list use square brackets [,]
  * You can gest an item at a specified position, chech the number of items, add, romove items
  * List are mutable, meaning they can be modified "in place"
  ### Familiarised functions
  1. ***len(name)***
  2. indexing : begine with 0 - list[0]
  3. Slicing : to pull the first x entries, you use [:x], and to pull the last y entries, you use [-y:], another option : [a:b] as a and b are indexes
  4. ***namelist.remove(element)***
  5. ***min() ,max()***
  6. ***sum()***
  7. adding items ***namelist.append(item)***
  8. turning string into a list ***stringname.split(here put the mark that separates two elements)***
  9. ***sorted(list)*** returns a sorted version of a list, if string - sorted in alphabethical order

Remember that when we add booleans, it returns the total number of entries in the sum that are True

# Objects
  1. Overall : objects carry some things around with them. **You access thet stuff using Python's dot syntax**
  2. Function attached to an object is called **method**, non-function things called **attributes**
  ## Examples
  List as object has defined methods such as:
    1. ***list.append()***
    2. ***list.pop()*** - removes and returns the last element of a list
    3. ***list.index(element)*** - returns index of searched element
  
  To find out wheather a list contains a particular value use **in** operator
  ```python
  #example
    "3" in primes
  ```
# Tuples
  1. The syntax for creating them uses parentheses instead of square brackets
  2. They cannot be modified - immutable
  3. used for functions that return multiple values
```python
#Example- swapping
  a = 1
b = 0
a, b = b, a
print(a, b)
```
