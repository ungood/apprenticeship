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

You're going to 
