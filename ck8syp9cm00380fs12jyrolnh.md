## The Classic Hello World Program in GO

## Introduction

To write your first code in any programming language, it has become a norm to start with a simple hello world program. In this program, I will be showing how to write a program in GO and explain all the parts of the program. Lets begin!👍🏼

## Program

The first step is creating a helloworld folder in your `$GOPATH`. To learn more about how to do this, view my previous article [here](https://fabcodes.hashnode.dev/what-the-dollargopath-is-about-ck8stjzhh004y07s129623r3v).

In the `main.go` file, write the following piece of code:
```
package main

import "fmt"

func main() {
   fmt.Println("Hello World!")
}

```

## Explanation

- `package main`  should always be first statement in a GO program. This creates an executable GO program. Every GO file can only belong to a single package.

- ` main`  represents the name of the package which this file belongs to.

- `import fmt`: This line imports the fmt package. [fmt](https://golang.org/pkg/fmt/) is a package that comes with the GO standard library. 

- `func main` is an entry point to this program. It is a special function which tells GO where to start execution. In all executable programs, almost everything will be run under this function.

- `func` represents a function. A function contains a block of code that can be executed when the function is called. It is used for reusable code.

- `fmt.Println`: This line prints "Hello World" to the terminal when the program is run. [Println](https://golang.org/pkg/fmt/#Println) is a method of the fmt package that writes to the standard output.

## Running the Program

There are two(2) tools available to run a GO program.

1. **go build**: this command compiles the GO program and we can then run afterwards. First we compile the program using:
```
$ go build
```
It seems as though nothing happened but then we need to use the `ls` or `dir` command to see the executable file. And then we run it by typing `./helloworld`.

 > This way of running GO programs is best suited for deployment.

2. **go run**: this command both compiles and run the GO program.
```
$ go run main.go
```
 > This is the most suitable for prototyping i.e. when developing

## Conclusion
That is all when trying to write and run your first program in GO. With this, we should be able to:
- understand the basic parts of a GO program.
- what statements like the package main and import clause does.
- how to print to the console.
- how to run a GO program.


## Other Articles 📖
- [What the $GOPATH is about](https://fabcodes.hashnode.dev/what-the-dollargopath-is-about-ck8stjzhh004y07s129623r3v)