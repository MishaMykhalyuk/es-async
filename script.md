http://2014.jsconf.eu/speakers/philip-roberts-what-the-heck-is-the-event-loop-anyway.html
https://github.com/jhusain/asyncgenerator

#JavaScript Engine

There are actually several different implementations of JavaScript engines but by far the most popular version is Google Chrome’s V8 engine (which is not limited to the browser but also exists in the server via NodeJS). But what exactly does the JavaScript Engine do? Well, it’s actually quite simple — it’s job is to go through all the lines of JavaScript in an application and process them one at a time. That’s right — one at a time, meaning that JavaScript is single-threaded. The main repercussion of this is that if you’re running a line of JavaScript that happens to take a longggggg time to return, then all the code after that will be blocked. And we don’t want to write code that’s blocking — especially on the browser. Imagine that you’re on a web site and click on a button … and then it just hangs there. You try clicking on other buttons but nope, nothing happens. The most likely culprit of this (assuming no bugs) is the button click triggered some JavaScript code to execute but it’s blocking.


#Call stack

So how does javascript engine know how to process a single line of javascript at a time?

It uses a Call Stack. Call Stack is like a shopping bag, the first item that enters in the shopping bag is the last item to exit and vice-versa. Javascript engine adds all line in call stack and executed it in LIFO method (Last in First Out). In short call stack is a data structure that records and identifies where we are in the program.


#Callbacks
The real problem with callbacks it that they deprive us of keywords like return and throw. Instead, our program's entire flow is based on side effects: one function incidentally calling another one.

And in fact, callbacks do something even more sinister: they deprive us of the stack, which is something we usually take for granted in programming languages. Writing code without a stack is a lot like driving a car without a brake pedal: you don't realize how badly you need it, until you reach for it and it's not there.

The whole point of promises is to give us back the language fundamentals we lost when we went async: return, throw, and the stack. But you have to know how to use promises correctly in order to take advantage of them.

The following code will throw an uncaughtException and there is no way to catch it. Even if core were to delegate this exception back to the callee this is potentially error-prone, as multiple callbacks have undefined behaviours.

# Generators
However, we wouldn’t want to use generators alone in production code because they forces us to reason about a process over time. And each time we call next, we jump back to our generator like a GOTO statement.

Coroutines understand this and remedy this situation by wrapping a generator and abstracting away all of the complexity.

Iterators are a special kind of behavior, a design pattern actually, where we step through an ordered set of values one at a time by calling next().

The iterator interface (introduced in ECMAScript 2015) is a sequential data access protocol which enables the development of generic and composable data consumers and transformers. Their primary interface is a next() method which returns a { value, done } tuple, where done is a boolean indicating whether the end of the iterator has been reached, and value is the yielded value in the sequence.


#Async iterator
While many data sources encountered by the JavaScript programmer are synchronous (such as in-memory lists and other data structures), many others are not. For instance, any data source which requires I/O access will be typically represented using a event-based or streaming asynchronous API. Unfortunately, iterators cannot be used to represent such data sources.


#Introducing Observable

If a generator function modifies a function and causes it to return multiple values and the async modifier causes functions to push their values, an asynchronous generator function must push multiple values. What data type fits this description?

ES6 introduces the Generator interface, which is a combination of two different interfaces:

- Iterator
- Observer
The Iterator is a data source that can return a value, an error (via throw), or a final value (value where IterationResult::done).