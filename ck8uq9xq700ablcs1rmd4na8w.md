## An Introduction to GO Packages

**GO Packages** are like an imaginary box which can contain lots of GO files.  In this respect, a package is only a directory inside your GO workspace containing one or more GO source files, or other GO packages. All files should belong to the same package and this is declared as the very first statement in GO code using the syntax:
```
package <packagename>
```

A package in GO can either be an _Executable Package_ or a _Library Package_.

## Executable vs Library Packages

### Executable Packages
These are programs that can be run from the command line. A program is executable if it starts with the `package main` statement. Every executable program should have a `main()` function which serves as the entry point of an executable program.

An example of an executable program is one i have written in this [post](https://fabcodes.hashnode.dev/the-classic-hello-world-program-in-go-ck8syp9cm00380fs12jyrolnh).

### Library Packages
These are reusable pieces of code that are used by other programs to perform certain tasks. They encourage us to build upon existing code. They are non-executable and can be imported into any GO program.

A Library Package does not have a `main()` function. Functions in a Library Package can have any name and should be capitalized for it to be accessible outside the package.

Great examples of Library Packages are the packages found in the [GO standard library](https://golang.org/pkg/#stdlib). There are also several third-party packages some of which can be found [here](https://github.com/golang/go/wiki/Projects#table-of-contents).


## Conclusion

The purpose of this article was to introduces GO Packages and also explain what Executable and Library Packages are. In the next article, I will be demonstrating how to create Library Packages and how to use them in a project. Thanks for reading.👋🏼

## Other Articles 📖
- [What the $GOPATH is about](https://fabcodes.hashnode.dev/what-the-dollargopath-is-about-ck8stjzhh004y07s129623r3v)

- [The Classic Hello World Program in GO](https://fabcodes.hashnode.dev/the-classic-hello-world-program-in-go-ck8syp9cm00380fs12jyrolnh)

#### Code Samples - https://github.com/Fakorede/Learning-Golang