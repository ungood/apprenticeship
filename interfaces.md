Assignment #4 - Abstract Data Types
-----------------------------------

In assignment #3, you implemented a singly-linked list, which is one type of data structure.  You may have
noticed that a linked list has similar operations as an array - both store data in an particular order, can
get and set items by index, and can be iterated.  This is because both data structures are instances of a
particular abstract data type.  Abstract data types (ADT) define a category of data structures by the operations that
are allowed on that type.  A particular ADT may have many ways to implement it, each with their own pros and cons.

In addition, one concrete type can implment multiple ADTs

Interfaces
----------

In C# (and Java), ADTs are called "interfaces".  They are like classes, in that they can have members: properties
and methods, but they don't define an implementation for any of their members.  Instead, a class can implement an
interface, which tells the compiler simply that anything that expects a variable of the interface type can be called
with an object of the type implementing the interface.

A common example:

  public interface IDrawable
  {
    void Draw();
  }
  
  public class Spaceship : IDrawable
  {
    public void Draw() { /* Draw a spaceship... */ }
  }
  
  public class Asteroid : IDrawable
  {
    public void Draw() { /* Draw an asteroid... */ }
  }
  
  public void GameLoop(params IDrawable[] gameObjects)
  {
    while(gameIsRunning)
    {
      GetUserInput();
      UpdateObjectPositions();
      ClearScreen();
      for(IDrawable obj in gameObjects)
        obj.Draw();
    }
  }
  
  DrawGame(new Spaceship(), new Asteroid(), new Asteroid(), etc...);
  
The advantage of using interfaces is that it allows you to design code with "loose coupling", which means that one
class knows as little as possible about other classes it communicates with.  In the previous example, withouth 
interfaces, GameLoop might need a big switch statement (if the object is a spaceship, call DrawSpaceship(), if it's
an asteroid, call DrawAsteroid(), etc..)  This gets hard to maintain when you start adding lots of different types
of objects.
  
Stacks and Queues, oh my!
-------------------------

Three common ADTs that crop up a lot in computer science are stacks, queues, and dequeues (or deque).  These all vary
slightly depending on who you ask, but these ADTs are defined by at least the following operations:

* stack - push, pop
* queue - enqueue, dequeue
* dequeue - add_front, add_back, remove_front, remove_back

I've provided some interfaces to represent each of these ADTs as well as one way to implement each using a 
dynamicly-sized array.  I've also provided one unit test for each.

Tasks
-----

You're going to implement your own versions of IStack, IQueue, and IDequeue using a double-linked list.  You have
several options for doing so: you can create a DoubleLinkedList class and use it as a private field in your
implementations, or you can use it as a base class.  You can even decide to simply implement all 3 interfaces in the DoubleLinkedList
class.

1.  Create a dummy implentation of each interface, however you want.
2.  Replace the ArrayStack, ArrayQueue, and ArrayDequeue constructors in the unit tests with your implementations.
3.  The unit tests should now fail (because your implementation is currently a dummy).
4.  Finish the implemntations, making the tests pass.
5.  Add unit tests as necessary to test every edge case.
6.  Comment on the pros/cons of a linked list implementation for each ADT vs an array.

Notes
-----
Okay, this one is similar to the last.  I promise I'm building up to some more fun assignments with more problem
solving.  I first gotta cover the basics, though.  If you want a teaser, look up the tower of hanoi problem - but
DONT CHEAT by reading any solutions. :)
