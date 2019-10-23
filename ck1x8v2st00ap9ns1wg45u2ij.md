## Is Node.js really Single Threaded? Here is what I think...

This is a very popular question in the node.js ecosystem. One that has been asked over and over again. And while many believe node.js really is single-threaded, in my opinion, i believe to really answer this question we will have to take a dive into the internals of node.js.

To really understand this article, I assume the reader understands how Node.js uses the **Event Loop** to handle the asynchronous code we write as many performance concerns about Node.js eventually boils down to how the Event Loop behaves.

## Building Blocks Of Node.js

![nodejs2.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1571448245688/jtfK9mYFU.png)

Node.js is a runtime environment for executing JavaScript code outside of a browser. Node.js internally has a collection of dependencies it uses to execute the JavaScript code we write.

The most important of these dependencies are the **V8 project** and the **libuv project**.

The **V8 project** is an open source JavaScript engine created by Google to execute JavaScript code in the browser.

The **Libuv project** is a C++ open source project that gives Node.js access to the Operating systems' underlying file system, networking and as well handles some aspects of concurrency.

When we start up a node program on our computer, node automatically creates one thread and executes all of our code in that single thread. Inside that thread, we have the **event loop** which we can think of as a structure that determines what the thread should be doing at any given instance. Every node program has exactly one event loop which is at the core of the program.

## Is Node Single Threaded?
Before i go in deeper, i have to make two points absolutely clear
- The Node Event Loop itself is **Single Threaded**
- Some of the functions included in the Node standard library are **not Single Threaded**. Which means some of the functions included in Node run outside of our event loop and outside that single thread. 
So, simply declaring that Node is single-threaded is not absolutely true.

In this article, we are going to look at a couple of examples of that by writing and executing some codes at the command line.

In your code editor, create a new file and name it `threads.js`
> Require the pbkdf2 function from the crypto module

We will run the function and benchmark how long it takes to run on our individual computers. We are not concerned here how the function runs.

```
const crypto = require('crypto')

const start = Date.now()
crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
      console.log('1:', Date.now() - start)
})
```
 Now lets see how long it takes the program to run. In your terminal, run
> node threads.js

![threads1.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1571450032878/oEexbSY6_.png)

For me, it takes aprox. 1600 milliseconds. Now lets duplicate the function and run:

```
const crypto = require('crypto')

const start = Date.now()
crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
      console.log('1:', Date.now() - start)
})

crypto.pbkdf2('a', 'b', 100000, 512, 'sha512', () => {
      console.log('2:', Date.now() - start)
})
```

I have to make it clear that both functions will be invoked at approx the same time. With that in mind, lets run the program again
> node threads.js


![threads2.PNG](https://cdn.hashnode.com/res/hashnode/image/upload/v1571450409472/10JM4UBAy.png)

We will notice that the times we are having now is above what we had before.

Now, to really understand the significance of the results we had above, i will use the diagram below

![threads3.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1571451735964/IQG60E-iB.png)

The above is a diagram of the results we would have expected to see if node were truely single-threaded.

If Node really was single-threaded, this is what we would have expected.


![threads4.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1571452915458/lbRr68hBY.png)

But in reality, this is what really happened:

![threads5.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1571453136729/VDXGkfcBt.png)

The pbkdf2 functions took approximately 2seconds to run. Clearly, this tells us something happened that went against the single-thread set up of Node because if we were running on only one single thread, we would have seen the first function call complete and then the second one execute.

## What really happened?

![threads6.png](https://cdn.hashnode.com/res/hashnode/image/upload/v1571453557624/7Z27TaAcm.png)

The way the pbkdf2() function in the node crypto module works is that it has both the JavaScript and the C++ implementation. But behind the scenes it delegates all the work to be done to the C++ side which contains refernces to the Libuv library which gives Node.js access to the underlying Operating System.

For some standard library function calls, the Node's C++ side and libuv decides to do expensive operations outside of the event loop entirely. Instead they make use of what is called a **Threadpool**.

The Threadpool is a series of four threads that can be used for running computation intensive tasks such as the pbkdf2() function. By default, libuv created four threads in this threadpool. That means that in addition to the thread used for the event loop, there are four other threads that can be used to handle expensive operations that occur in our applications which some functions in the Node standard library make use of.

## Conclusion
While the Event Loop in Node.js is single-threaded, It isn't entirely true that Node.js is single-threaded because there are some other threads available in the libuv Threadpool which Node.js uses in doing computational intensive tasks.

In my next article, we will be looking at how to enhance the performance of Node.js applications using Clustering.