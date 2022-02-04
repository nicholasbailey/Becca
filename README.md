# Becca
A simple dynamic language for exploring language design

## What is Becca

Becca is a simple dynamic programming language. 

## Should you use Becca?

If your goal is to write programs to solve real world problems then _absolutely not_. Becca is not designed to be a production language. It's almost completely untested, and there's no guarentee whatsoever the interpreter is bug free. Even if Becca were a battle tested language, the interpreter is unsophisticated and not remotely performance tuned. The interpreter is written in Go which while very fast is not likely to perform at the level of a pure C/C++ interpreter. Literally any language would be a better choice for solving real world problems - even PHP!

However, if you want to explore writing your own language, Becca is a great place to start. Because the interpreter is written in Go, the internals are more accessible to the average developer. Since Becca doesn't consider performance a concern, the interals are comparatively easy to follow. The language is deliberately designed to be easy to modify and extend.

## Syntax

### Basics

Becca is a dynamically typed procedural language in the C family. Becca's syntax is closest to Javascript, with some features drawn from Python, C# and Scala. 

Here's Hello World in Becca:

```
print("Hello World");
```

### Variables

Like many other languages, Becca uses `=` to assign values to variables

```
x = 1;
y = 2;
print(x, y);
```

Becca is dynamically typed, meaning values of any type can be assigned to any variable

```
x = 1;
x = "One";
x = true;
```

Values have a runtime type which can be accessed via the `type` function

```
x = 1;
print(type(x)); // int
x = "One";
print(type(x)); // string
```

Values can be compared with `==` and `!=`. Becca is much stricter about comparisons than many other dynamic languages. Two values of different types are never equal, so `0.0 == 0` is false. Another way of thinking about this is that Becca never peforms implicit type conversions.

### Blocks and Statements

Becca statements must be terminated by a semicolon. This feature is likely to go away in the future, but for now it make the parser way easier to write.

Becca blocks are delimited by braces like this 

```
if (true) {
    print("IT'S REAAAAAAL");
}
```

In Becca, all statements have a value (though it's not always possible to assign that value into a variable currently). The value of an assignment is the value assigned. The value of a block is the last statement executed in a block. The value of a loop or a conditional is the value of the last block executed. 

Note that currently Becca does not support block scoped variables. All variables are scoped to the enclosing function, or globally if there is no enclosing function.

### Types

Becca supports several built in types

#### Integers

Becca ints are 64 bit integers. Becca doesn't support integers of other precisions. Note that because of how Becca is implemented all ints are 'boxed' as objects, meaning ints actually take up substantially more space. 

Becca ints support all of the normal mathematical operations. Note that division of two ints performs 'integer division', dropping any remainder. 

```
x = 1
y = 2
// Addition
x + y 
// Subtraction
x - y
// Multiplication
x * y
// Division
x / y
// Modulo
x % y
// Exponentiation
x ** y
```

Becca doesn't support 'math + assignment' operators. There's no `++`, `--`, `+=`, `-=` or the like. They may be added in a future versions.

#### Floats

Becca floats are 64 bit floating point numbers. Becca doesn't support floats of other precisions. Like ints, floats are boxed and so actually take up quite a bit more space than 64 bits.

```
x = 1.0
y = 2.0
// Addition
x + y 
// Subtraction
x - y
// Multiplication
x * y
// Division
x / y
// Exponentiation
x ** y
```

#### Strings

Becca strings are (currently) implemented as Go strings under the hood, which means they are utf-8 encoded sequences of bytes. 

#### Booleans

Becca supports a boolean type with two values `true` and `false`


#### Records
COMING SOON

#### Lists
COMING SOON

### Control Flow

#### Conditionals

Becca supports the familiar if/else if/else syntax from other C derived languages

```
if (age < 18) {
    print("Too Young");
} else if (age < 21) {
    print("You Can Vote");
} else {
    print("You Can Drink");
}
```

Becca doesn't currently have any kind of `switch` statement or pattern matching. Maybe someday!

#### Loops

Becca supports traditional while loops

```
x = 1;
while (x < 10) {
    print(x);
    x = x + 1
}
```

Other loop types will be added soon


### Functions

Becca functions work similarly to other dynamic procedural languages. Functions are defined with the `def` keyword

```
def isABigInt(value) {
    return type(value) == 'int' && value > 100;
}
```

Currently, Becca functions without a return statement return the last value in the function

```
def isABigInt(value) {
    type(value) == 'int' && value > 100;
}
```

I can't decide if I like this behavior, so we'll see if I keep it.

Functions are called by passing in arguments,
separated by commas. 

```
isABigInt(10); // returns true
isABigInt("10"); // returns false
```

