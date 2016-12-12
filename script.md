# Generators
However, we wouldn’t want to use generators alone in production code because they forces us to reason about a process over time. And each time we call next, we jump back to our generator like a GOTO statement.

Coroutines understand this and remedy this situation by wrapping a generator and abstracting away all of the complexity.

Iterators are a special kind of behavior, a design pattern actually, where we step through an ordered set of values one at a time by calling next().

The iterator interface (introduced in ECMAScript 2015) is a sequential data access protocol which enables the development of generic and composable data consumers and transformers. Their primary interface is a next() method which returns a { value, done } tuple, where done is a boolean indicating whether the end of the iterator has been reached, and value is the yielded value in the sequence.