Assignment #3 - A singly-linked list
------------------------------------

Here, I've pushed a change to the same repository containing a new class SingleLinkedList, with a stub implementation.
We are going to use this data structure in the future, so first you need to implement it (it'd be cheating to use the
built in C# List class, of course).

One new thing here is that you'll notice it has a weird <T> syntax.  This means it is a generic class.  The T represents
any type (you can name the generic parameter anything you like (like ItemType), T is is just traditional).  When you
create an instance of a generic class, you specify what type T will be for that instance.  This way you don't need
to reimplement a LinkedList for every type of thing you may want to store.  You can use the same class to store ints,
or strings, or Widgets.

Things to learn in this one: Generics, properties, indexers, exceptions, and writing good tests.

Notes
-----
* The Node class in SingleLinkedList is called an "inner" class.  Because it's private, it can only be accessed
  by that class.
* RemoveAt is probably the hardest method there to implement.

Commenting
----------
I've commented this class mostly how I would do it in real life.  The /// and XML comments are a C# convention
hat will produce documentation for you automatically when you compile the code.  This is really nice if you
are writing a public library for other people to use.  Java and python have similar conventions

As I've mentioned before, the professor-driven convention of commenting every line of code drives me insane.  Good
code should be self-commenting - you shouldn't need comments to understand what it does.  Occasionally, you have to
break that rule to implement something really crazy, but in general, good comments should explain why, not how.

Writing libraries is a different beast.  In that case, you're writing code to be used by other programmers, and 
documentation is important.  They might not want to or be able to look at the source code you wrote to figure out
what something does.  In general, I try to write at least a summary for every public class and public member (method,
property, etc...)

I saw someone at work write the following:

  // returns the result
  return result;
  
This pissed me right the hell off.  Don't do this ;)

Tasks
-----
* Implement the missing methods in SingleLinkedList<T> per the documented API.
* Write unit tests to test that your code works.  (I've written a test program, but only for instructional purposes).
* Document the big-O complexity of each of the methods.
