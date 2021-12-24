# The Elements of Programming
A powerful programming language is more than just a means for instructing a computer to perform tasks.

The language also serves as a framework within which ideas about proceses can be organized.

Every powerful language has three mechanisms for accomplishing this:

* **primitive expressions**, which represent the simplest entities the language is concerned with,
* **means of combination**, by which compound elements are built from simpler ones, and
* **means of abstraction**, by which compound elements can be named and manipulated as units.

In programming, there are two kinds of elements that are dealt with:
- procedures and data.

Any powerful programming language should be able to describe primitive data and primitive procedures and should have methods for combining and abstracting procedures and data.

## Expressions

This is a very simple primitive expression (a number).

Expressions like these will consist of the numerals that represent the number in base 10.
```python
486
```
> 486

Expessions representing numbers may be combined with an expression representing a primitive procedure (such as + or *) to form a compound expression that represents the application of the procedure to those numbers.

```python
137 + 349
```
> 486

```python
1000 - 334
```
> 666

```python
5 * 99
```
> 495

```python
10 / 5
```
> 2

```python
2.7 + 10
```
> 12.7

Expressions such as these, which combine other primitive expressions in order to denote procedure application, are called *combinations*.

* The middle element (+, -, etc.) is called the ***operator***.
* The other elements are called ***operands***.

The value of a combination is obtained by applying the procedure specified by the operator to the *arguments* that are the values of the operands.

The combinations can be *nested* using parenthesis, that is, to have combinations whose elements are themselves combinations:

```python
(3 * 5) + (10 - 6)
```
> 19

There is no limit (inc principle) to the depth of such nesting and to the overall complexity of the expressions.

```python
(3 * ((2 * 4) + (3 + 5))) + ((10 - 7) + 6)
```
> 57

## Naming and the Environment

A critical aspect of a programming language is the means it provides for using names to refer to computational objects.
* The name identifies a *variable* whose *value* is the object.

```python
pi = 3.14159
age = 18
```

Here are some further examples:
```python
pi = 3.14159
radius = 10

pi * (radius * radius)
```
> 314.159

```python
circumference = (2 * pi * radius)
circumference
```
> 62.8318

The ability to assign values to names is the language's simples means of abstraction, for it allows the usage of simple names to refer to the results of compound operations, such as `circumference` computed above.

It should be clear that the possibility of associating values with symbols and later retrieving them means that the interpreter must maintain some sort of memory that keeps track of the name-object pairs.

* This memory is called the *environment* (more precisely the *global environment*).

## Compound Procedures
Some of the elements that must appear in any powerful programming langauge:

* Numbers and arithmetic operations are primitive data and procedures.
* Nesting of combinations provides a means of combining operations.
* Definitions that associate names with values provide a limited means of abstraction.

Another much more owerful abstraction technique by which a compound operation can be given a name and then referred to as a unit is called ***procedure definitions***.

Example: Square Procedure

"To square something, multiply it by itself".
```python
def square(n):
    return n * n
```
This is a ***compound procedure***, which has been given the name `square`.

* The procedure represents the operation of multiplying something by itself.
* The thing to be multiplied is given a local name, `n`.

The general form of a procedure definition is
```
def name(formal parameters):
    body
```

* The *name* is a symbol to be associated with the procedure definition in the environment.
* The *parameters* or *formal parameters* are the names used within the body of the procedure to refer to the corresponding arguments of the procedure.
* The *body* is an expression (or a sequence of expressions) that will yield the value of the procedure application when the formal parameters are replaced by the actual arguments to which the procedure is applied.

Calling a procedure,
```python
square(21)
```
> 441
```python
square(7 + 5)
```
> 49
```python
square(square(3))
```
> 81

It is also possible to use `square` as a building block in defining other procedures.

For example, $x^2 + y^2$ can be expressed as
```python
square(x) + square(y)
```

Procedure `sum_of_squares` can be easily defined, given any two numbers as arguments, produces the sum of their squares.
```python
def sum_of_squares(x, y):
    return square(x) + square(y)

sumOfSquares(3, 4)
```
> 25

Now `sum_of_squares` can be used as a building block in constructing further procedures:
```python
def (a):
    return sum_of_squares(a + 1, a * 2)

f(5)
```
> 136

Compound procedures are used in exactly the same way as primitive procedures.

* One could not tell by looking at the definition of `sum_of_squares` given above whether `square` was built into the language, like `+` and `*`, or defined as a compound procedure.

## Conditional Expressiosn and Predicates
The expressive power of the class of procedures that can be defined at this point is very limited, because there is no way to make tests and to perform different operations depending on the result of a test.

For instance, at this point a procedure can't be defined that computes the absolute value of a number by testing whether the number is positive, negative, or zero and taking different actions in the different cases according to the rule

$$
|x| = \begin{cases}
	x &\text{if } x>0\\
	0 &\text{if } x=0\\
	-x &\text{if } x<0\\
	\end{cases}
$$

This construct is called a *case analysis* and there is a special form in pythonthon for notating such a case analysis. It is called `if`, and it is used as follows:

```python
def abs(x):
    if x > 0:
        return x
    elif x == 0:
        return 0
    elif(x < 0):
        return -x
```

The general form of a conditional expression is
```
if (predicate <p1>):
    // expression
elif (predicate <p2>):
    // expression
...
else:
    // expression
```
It consists of:

* the symbol `if`, `elif`, or `else`.
* The clause inside the paranthesis is called the *predicate* - that is, an expression whose value is interpreted as either `True` or `False`, 
* followed by expressions to execute if the predicate turns out to be true.

Conditional expressions are evaluated as follows:

* The predicate \<p1> is evaluated first.
* If its value is false, then \<p2> is evaluated and so on.
* The process continues until a predicate is found whose value is true, in which case the interpreter returns the value of the conditional expression.
* If all the predicates are false, it returns the value of `else` expression.

The word *predicate* is used for procedures that return true or false, as well as for expressions that evaluate to true or false.

It is also possible to use the `else` expression to write a procedure for the absolute value of x.
```python
def abs(x):
    if x < 0:
        return -x
    else:
        return x
```
This could be interpreted as "if $x$ is less than zero return $-x$; otherwise return $x$."

In addition to primitive predicates such as `<`, `=`, and `>`, there are logical composition operations, which enable the construction of compound predicates.

The three most frequently used are these:

* <$e_1$> `and` <$e_2$>
The interpreter evaluates the expressions <$e$> one at a time, in left-to-right order. If any <$e$> evaluates to false, the value of the `and` expression is false, and the rest of the <$e$>'s are not evaluated. If all <$e$>'s evaluate to true values, then the value of the `and` expression is true.
* <$e_1$> `or` <$e_2$>
The interpreter evaluates the expressions <$e$> one at a time, in left-to-right order.
If any <$e$> evaluates to a true value, then true is returned as the value of the `or` expression.
If all <$e$>'s evaluate to false, the value of the `or` expression is false.
* `not` <$e$>
The value of a `not` expression is true when the expression <$e$> evaluates to false, and false otherwise.

As an example of how these are used, the condition that a number $x$ be in the range $5<x<10$ may be expressed as
```python
(x > 5) and (x <10)
```
As another example, a predicate can be defined to test whether one number is greater than or equal to another as
```python
def greaterOrEqual(x, y):
    return not(x < y)
```

## Example: Square Roots by Newton's Method
Procedures are much like ordinary mathematical functions.

* They specify a value that is determined by one or more parameters.
* But there is an important difference between mathematical functions and computer procedures.
    * Procedures must be effective.

Square root function can be defined as
$$\sqrt{x} = \text{ the } y \text{ such that } y\geq 0 \text{ and } y^2 = x$$

This describes a perfectly legitimate mathematical function.
On the other hand, the definition does not describe a procedure.
Infact, it tells us almost nothing about how to actually find the square root of a given number.

The contrast between function and procedure is a reflection of the general distinction between describing properties of things and describing how to do things, or, as it is sometimes referred to, the distinction between declarative knowledge and imperative knowledge.

* Mathematics is usually concerned with declarative (what is) descriptions,
* Computer science is usually concerned with imperative (how to) descriptions.

So to compute square roots, the most common way is to use Newton's method of successive approximations, which says that when a guess $y$ for the value of the square root of a number $x$ exists, perform a simple manipulation to get a better guess (one closer to the actual square root) by averaging $y$ with $x/y$.
Continuing this process will produce better and better approximations to the square root.
When the guess is good enough for intended purpose, the execution halts.

It's also essential to properly define what "good enough" means:
* The idea is to improve the answer until it is close enough so that its square differes from the radicand by less than a predetermined tolerance (here 0.001):

```python
def sqrt(x):
    return sqrt_iter(1, x)

def sqrt_iter(guess, x):
    if (is_good_enough(guess, x)):
        return guess
    else:
        return sqrt_iter(improve(guess, x), x)

def is_good_enough(guess, x):
    if abs(square(guess) - x) < 0.001:
        return True
    else:
        return False

def improve(guess, x):
    return average(guess, x / guess)

def abs(x):
    if x < 0:
        return -x
    else:
        return x

def average(a, b):
    return (a + b) / 2

def square(n):
    return n * n
```

The `sqrt` program also illustrates that the simple procedural language introduced so far is sufficient for writing any purely numerical program.
* `sqrt_iter` demonstrates how iteration can be accomplished using no special construct other than the ordinary ability to call a procedure.

## Procedures as Black-Box Abstractions

`sqrt` is the first example of a process defined by a set of mutually defined procedures.

Note that the definition of `sqrt_iter` is *recursive*; that is, the procedure is defined in terms of itself. The idea of being able to define a procedure in terms of itself may be disturbing; it may seem unclear how such a "circular" definition could make sense at all, much less specify a well-defined process to be carried out by a computer. This will be addressed more carefully later.

<img src="/Users/cipher7d3/Library/Application Support/typora-user-images/image-20211222214217763.png" alt="image-20211222214217763" style="zoom:53%;" />

* Observe that the problem of computing square roots breaks up naturally into a number of subproblems:
    * How to tell whether a guess is good enough, how to improve a guess, and so on.
* Each of these tasks is accomplished by a separate procedure.
* The entire `sqrt` program can be viewed as a cluster of procedures that mirrors the decomposition of the problem into subproblems.

The importantce of this decomposition strategy is not simply that one is dividing the programs into part as it's possible to take any large program and divide it into parts -the first ten lines, the next tenlines, and so on. Rather, it is crucial that each procedure accomplishes an *identifiable task* that can be used as a module in defining other procedures.

For example,

* The `square` procedure is regarded as a "black box" when the `is_good_enough` procedure is defined in terms of it.

    * *How* the procedure computes its result is not relevant, only that it computes the square.
    * The details of how the square is computed can be suppressed, to be considered at a later time.

* Infact, as far as the `is_good_enough` procedure is concerned, `square` is not quite a procedure but rather an abstraction of a procedure, a so-called *procedural abstraction*.

    * At this level of abstraction, any procedure that computes the square is equally good.

* Thus, considering only the values they return, the following two procedures for squaring a number should be indistinguishable.
    * Each takes a numberical argument and produces the square of that number as the value.

    ```python
    from math import log, exp
    
    def square(x):
        return x * x
    
    def double(x):
        return x + x
    
    def square(x):
        return exp(double(log(x)))
    ```

* So a procedure definition should be able to suppress detail. The users of the procedure may not have written the procedure themsevles, but may have obtained it from another programmer as a black box.

    * A user should not need to know how the procedure is implemented in order to use it.

### Local names

One detail of a procedure's implementation that should not matter to the user of the procedure is the implementer's choice of names for the procedure's formal parameters.

Thus, the following procedures should not be distinguishable.

```python
def square(x):
  return x * x

def square(y):
  return y * y
```

The parameter names of a procedure are local to the body of the procedure.

* A formal parameter of a procedure has a very special role in the procedure definition, in that it doesn't matter what name the formal parameter has.
* Such a name is called a *bound variable*, and the procedure definition *binds* its formal parameters.
    * The meaning of a procedure definition is unchanged if a bound variable is consistently renamed through the definition.
* If a variable is not bound, then it is called *free*.
* The set of expressions for which a binding defines a name is called the *scope* of that name.
    * In a procedure definition, the bound variables are declared as the formal parameters of the procedure have the body of the procedure as their scope.
* In the definition of `is_good_enough` above, `guess` and `x` are bound variables but `abs` and `square` are free.

### Internal definitions and block structure

There is one kind of name isolation available so far: The formal parameters of a procedure are local to the body of the procedure.

Another way of controlling the use of names is illustrated by the square-root program.
The existing program consits of separate procedures:

```python
def sqrt(x):
    return sqrt_iter(1, x)

def sqrt_iter(guess, x):
    if (is_good_enough(guess, x)):
        return guess
    else:
        return sqrt_iter(improve(guess, x), x)

def is_good_enough(guess, x):
    if abs(square(guess) - x) < 0.001:
        return True
    else:
        return False

def improve(guess, x):
    return average(guess, x / guess)

def abs(x):
    if x < 0:
        return -x
    else:
        return x

def average(a, b):
    return (a + b) / 2

def square(n):
    return n * n
```

The problem with this program is that the only procedure that is important to users of `sqrt` is `sqrt`.

* The other procedures (`sqrt_iter`, `is_good_enough`) only clutter things up.
* The problem is especially severe in the construction of large systems by many separate programmers.
    * For example, in the construction of a large library of numerical procedures, many numerical functions are computed as successive approximations and thus might have procedures named `is_good_enough` and `improve` as auxiliary procedures.
* Localising the subprocedures, hiding them inside `sqrt` so that `sqrt` could coexist with other successive approximations, each having its own private `is_good_enough` procedure is a good idea.

To make this possible, allow a procedure to have internal definitions that are local to that procedure.

For example, in the square-root problem

```python
def square(n):
    return n * n

def average(a, b):
    return (a + b) / 2

def sqrt(x):
  	def is_good_enough(guess, x):
      	if abs(square(guess) - x) < 0.001:
          	return True
    		else:
          	return False
          
		def improve(guess, x):
    		return average(guess, x / guess)
      
    def sqrt_iter(guess, x):
        if (is_good_enough(guess, x)):
            return guess
        else:
            return sqrt_iter(improve(guess, x), x)
		
    return sqrt_iter(1, x)
```

Such a nesting of definitions, called *block structure*, is basically the right solution to the simplest name-pack