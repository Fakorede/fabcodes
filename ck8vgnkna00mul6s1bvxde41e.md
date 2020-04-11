## Variables in GO

## Introduction
GO stores a variable inside a computer memory. A variable occupies some space on the memory depending on the variables type. Variables are only created after you run your program so they only become alive at the runtime not the compile-time.  GO only knows the type at compile-time.

A variable stores a value with a type because GO is a strongly typed language. This is why we can't store an integer variable inside a variable which has a string type.

**Variable Name** allows us access the variable.

**Variable Type** GO is a statically typed programming language. In GO, every variable has a type. It is called _static type_ since we can't change the type of a variable once we declare it.

Since a Variable should have a type, its only important to talk about the basic data types.

## Basic Data Types
**int** - An int type represents numbers without a fractional part. It can be negative, zero, or positive numbers . It ranges from -128 to 127. These are called _integer literals_. GO has several built-in integer types for storing signed and unsigned numbers with varying sizes.

**float64** - A float type are used to store numbers with a fractional part ex -2.5, 0.5, 1.5. These are called _float literals_.

**bool** - The bool type can only represent two values, *true* and *false*. These are called boolean values and are pre-declared constants.

**string** -  The string type is used for representing human readable text data. An example string literal is "hello world!". A string can contain english and non-english characters.

## How to Declare a Variable
In GO, we need to declare a variable before we can use it unlike in a dynamic language where we can assign a value to a variable even before declaring it. This is important and necessary for the compile-time safety.

**Example**
```
var speed int
```
The `var` keyword which is short for variable starts the variable declaration. It simply tells GO to declare a variable.

After the var keyword, we need to give a unique name to the variable. Here, `speed` is the name of this variable. A variable name can also be referred to as an identifier. It helps us understand which variable we are referring to.

`int` is the type of this variable. In GO, every variable has a type. This is because GO is a `strongly-typed` programming language. This helps the compiler find bugs in our program even before we run it. A variable type determines what type of value we can store in it and where we can use it.

**Naming Rules**
- A name should only start with a letter or an underscore character. When the name starts with an uppercase letter, that name becomes exported so that other packages can use it.
- A name can contain uppercase letters.
- A name can have unicode letters. This works because GO can understand unicode letters.
- A name cannot contain reserved keywords.

## Zero Values
Now if we try to print this variable to the console, we get 0. This is because a variable gets initialized to a _zero value_ when its declared without an initial value.
```
var speed int
fmt.Println(speed) // 0
```
Every GO type has a zero value. An empty variable gets a _zero value_ depending on its type.
```
var speed int
var temperature float64
var off bool
var name string

fmt.Println(speed) // 0
fmt.Println(temperature) // 0
fmt.Println(off) // false
fmt.Printf("%q\n", name) // ""
```

## Declaring Multiple Variables
By using a multiple declaration, we can declare multiple variables at once in the same declaration statement.
```
var (
   speed int
   temperature float64
   off bool
   name string
)
```
This is exactly the same as the previous declaration. Its purpose is to improve readability. Its better to use this style when you intend to group a few related variables together.

We can also declare multiple variables that have the same times like so:
```
var speed, velocity int
```
We don't have to define the types of each variable if their types are the same.

## Type Inference
We can declare variables without specifying its type. This is because GO uses what is called _Type Inference_ which means that GO can figure out the type of the variable automatically. 
```
var age = 10
fmt.Printf("Variable has a type %T\n", age) // int
```

## Short Declaration
In GO, we don't even need to use the `var` keyword. Just the name of the variable and its value is enough. In this case, we use the _Short Declaration Syntax_ using the `:=` operator like so:
```
isSafe := true
fmt.Printf("Variable has a type %T\n", isSafe) // bool
```

## Multiple Short Declaration
We can declare and initialize multiple variables using short declaration.
```
month, day := "April", 11
fmt.Println(month, day) // April 11
```
Here "Fab is assigned to name and 22 is assigned to age. The first variable gets the first value and the second variable gets the second value.

## Redeclaration
Redeclaration allows us to use existing variables in multiple short declaration variables i.e. declaring new variables while assigning values to existing variables.
```
var firstname string
firstname, lastname := "Nikola", "Tesla"

fmt.Println(firstname, lastname)
```
* One of the variables must be a new variable or the redeclaration won't work.

## When to Use Declaration vs When to Use Short Declaration
Use normal declaration:
- If you don't know the initial value
- When you want to group variables together

Use short declaration:
- If you know the initial value
- To keep the code concise
- For redeclaration

## Blank Identifier
What happens when we don't use declared variables? A variable declared in every block scope should be used or there will be an error.
```
func main() {
   var name string // ERROR: name declared and not used
}
```
Running this program will cause a compile-time error because the variable name was declared but not used.

The _Blank Identifier_( _ ) can be used to prevent unused variable error. It is like a black hole which consumes the variable.
```
func main() {
   var name string
   _ = name
}
```

## Conclusion
Variables are a very important concept of any programming language. Therefore, it is important to understand the work-arounds around them. In this article, the following concepts were introduced:
- Variable Declaration
- Zero Values
- Declaring Multiple Variables
- Type Inference
- Short Variable Declaration
- Multiple Short Declaration
- Redeclaration
- Blank Identifiers

A link has also been provided to the GO Playground to demonstrate everything we have learnt in this lecture. Thanks for reading and any feedback would be much appreciated. 👋🏼

## Other Articles 📖
- [What the $GOPATH is about](https://fabcodes.hashnode.dev/what-the-dollargopath-is-about-ck8stjzhh004y07s129623r3v)

- [The Classic Hello World Program in GO](https://fabcodes.hashnode.dev/the-classic-hello-world-program-in-go-ck8syp9cm00380fs12jyrolnh)

- [An Introduction to GO Packages](https://hashnode.com/edit/ck8uq9xq700ablcs1rmd4na8w)

#### Code Samples - https://github.com/Fakorede/Learning-Golang
#### GO Playground - https://play.golang.org/p/bF3u5v-Er39

