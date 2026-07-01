# Notes 
Based on Kaggle Intro to Programming course
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

Order of operations : PEMDAS rule 
  1. Parentheses first
  2. Exponents
  3. Multiplications and Division : read from left to right
  4. Addition and Substraction : read from left to right

## Comments
"#" in the beginining of phrase
## Variables
Rules:
  1. They can't have spaces
  2. They can only include letters, numbers, and underscores
  3. They have to start with letter or undercsore
By assinging a variable - we assing it globally

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
  * ***if...elif...else***
