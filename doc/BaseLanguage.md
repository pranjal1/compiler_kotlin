# Base Language

## Types

* `Boolean`
* `Int`
* `String`
* `Unit` - indicates the absence of a value. unit is the only value of type Unit

* Structure: `struct <identifier> { <identifier> : <type>, ... }`
* Array: `[<type>]`

* `Any` - super type of all types

## Expressions

Expressions are composed of operands, operators and function calls. Expression evaluates to a value. The order of execution for the operators can be summarized in the table below.

| Operator      | Type     | Associativity |
|---------------|----------|---------------|
| + - % *       | Arithmetic | left to right |
| \>, >=, <, <= | Comparison | left to right |
| ==, !=        | Equality | left to right |
| !, &&, &#124; | Logical    | left to right |

An expression can be composed of no operator, a single operator or multiple operators.

```
"Hello"; 
2+3;
4 + 5 * 3;
test_function(x); //x is a variable
```

### Arithmetic (+, -, %, *)

Arithmetic operators can be applied to integers `Int`. The result of an arithmetic operation is also an `Int` value. 
- `+` performs the addition operation between two integers.
- `-` performs the subtraction operation between two integers. It can be also used to perform the negation operation on an integer. Eg. `-5`.
- `%` performs the modulo operation. `a % b` returns the remainder value when `a` is divided by `b`.
- `*` performs the multiplication operation between two integers.

Binary arithmetic operators (+, -, %, *) consume two `Int` values
Unary arithmetic operators (-) consume one `Int` value

### Comparison (>, >=, <, <=)

Comparison operators produce a `Boolean` value. Comparison operators consume two values that are either both `Boolean`, `Int`, or `String`.

For boolean comparison, the following expressions result in `true` output: 
- `true` > `false`
- `false` < `true`
- `true` >= `false`
- `false` <= `true`

For `String` comparison, we consider the Unicode values of each character. The comparison involves checking the Unicode value of the characters from zeroth index till the end of the strings.

### Equality (==, !=)

Equality operators produce a `Boolean` value. Equality operators consume two values that are of any type. 

Like with the comparison operation, for `String` equality check we consider the Unicode values of each character. The comparison involves checking the Unicode value of the characters from zeroth index till the end of the strings. Equal strings must have equal length and have same Unicode values for characters in the same index.

### Logical (!, &&, ||)

Logical operators produce a `Boolean`.

Binary logical operators (&&, ||) consume two `Boolean` values. Unary logical operators (!) consume one `Boolean` value.

Here is the truth table for the logical operators.

| x  | y | x && y  | x &#124;&#124; y | !x |
|----------|---------------|----------|------------|---------------|
| true | true | true | true       | false |
| true | false | true | false      | false |
| false | true | false | true       | true |
| false    | false | false    | false      | true |

Binary logical operators "short-circuit". If the result of the expression can be determined from only evaluating the left-hand side value, the right-hand side value is not evaluated.

### Literal values

Literal values of each type are expressions.

* Boolean: `true`, `false`
* Int: Recognized by the regular expression: `^-?[0-9]+$`. Examples: `-5`, `10`, `100`, etc.
* String: Strings are put inside the double quotes and consists of zero or more characters. Examples: `"hello world"`, `"Compilers"`.
* Unit: Indicates the absence of value. `unit` is the ony value of type Unit. One of its usages is to specify the return type of functions with no return value.
* Structure: It is a way to group multiple related variables in a place. The variables belonging to a struct are called its members. Structure has to be declared before its usage. `struct` keyword is used to define the Structure. Example:
```
// declaration
struct Point { x: Int, y: Int }

// usage
var P1: Point = Point(10, 20);
var P2: Point = Point(100, 200);
```
* Array: Array is a collection of variables of the same type. Example:
```
var arr:[Int] = [1,2,3];
var arr:[String] = ["Hello", "World"];
var pts:[Point] = [P1, P2];
```

### Index

Individual elements of an array can be accessed using square brackets (e.g., `a[0]`). A valid index is in between 0 and the (length of the array - 1).

### Select

Fields of a structure can be accessed using a dot (e.g., `p.x`). 
```
struct Point { x: Int, y: Int }
struct Triangle { v1: Point, v2: Point, v3: Point }


var P1: Point = Point(0,1);
var P2: Point = Point(1,0);
var P3: Point = Point(-1,0);

var T1: Triangle = Triangle(P1, P2, P3);

print(P1.x); // accessing member x of P1 of type Point.
print(T1.v1.x); // multiple structs can be chained and the nested members can be accessed using dot.
```

### Precedence and grouping

Arithmetic, comparison, equality, and logical operators have precedence and associativity that you'd expect coming from C. Here is a table showing the operator precedence:

| Operator     |Associativity|
|--------------|-------------|
| *, %         | Left to right|
| +, -         | Left to right|
| <, <=, >, >= | Left to right|
| ==, !=       | Left to right|
| &&           | Left to right|
| &#124;&#124;      | Left to right|

The table lists the operators with their precedence in descending order. The operator with the highest precedence is in the top of table.


Parenthesis, `(` and `)`, can be used to group expressions and can be used to change the order of execution in the expression. It is a good practice to use grouping to enhance readability to show the order of execution.

## Statements

Statements do not produce a value. They produce a side-effect. Example: `return` returns a value from a function.

### Assignment

Assignment statements store a value in a location (variable, structure field, or array element). The type of the value must be compatible with the type of the location.

### Block

A block is a sequence of statements surrounded by braces `{` and `}`

### Expression statement

An expression followed by a semi-colon `;` is am expression statement

### If

An if statement executes one of two statements based on some condition value (e.g., `if (c) s1 else s2`)

### While

A while loop executes the body repeatedly as long as the condition expression evaluates to true (e.g., `while (c) s`)

## Variables

Variables are declared using the "var" keyword. Variables must specify their type and must be initialized with an expression (e.g., `var x: Int = 5;`)

## Functions

Functions calls look like C: `callee(argument1, argument2, ...)`

Functions are declared using the "fun" keyword. Functions must have a name, and declared their parameter types and return type. See below for examples.

Values can be returned using the "return" statement. Functions whose return type is Unit do not need to contain a return statement. All other functions must return a value of the appropriate type.

### Builtin functions:

* `fun print(s: String) -> Unit { ... }`
* `fun concat(s1: String, s2: String) -> String { ... }`
* `fun str(a: Any) -> String { ... }`

