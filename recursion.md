Recursion
---------
Recursion is a fairly simple concept - a function that calls itself - but it can be hard to reason about recursive
strategies.  However, many elegant algorithms are recursive (quick sort always comes to mind), and it is a very useful
tool to have in the toolbox.  Pragrmatically, recursion is a favorite topic for interviewers...

Recursion is very similar to using inductive proofs in math.  The best way to write a recursive function is to think
of your base case(s) (when do you return from the method), and code those first.  Then, think about how you solve for N
given N-1.

While recursive algorithms are often elegant, they're not always the most optimal.  Since every call of a method pushes
data onto the call stack, recursive algorithms are prone to "stack overflow", where the call stack overflows its bounds
and throws an exception (C#), seg faults (if you're lucky), or writes into bad parts of memory (if you're not).  There
are ways to refactor recursive algorithms to make them more efficient, but we'll get into that later.

Fibonacci
---------
You're probably familiar with the fibonacci sequence, but if not, take a look at the wikipedia page.  Fibonacci is a
favorite for recursion because the definition of the function is recursive, making an implementation of the function
very straight-forward.

I want you to first implement Fibonacci recursively.  Note, the unit tests for this are written to fail if they
run longer than 1 second, some of the Recursive tests will probably fail because of this.

Then, implement Fibonacci iteratively - that is, without calling itself, using a loop instead.

What is the runtime of the two algorithms?  What's the benefit of the recursive algorithm?  What's the benefit of the
iterative solution?

Towers of Hanoi
---------------
The Towers of Hanoi is a pretty common puzzle: three rods with various sized disks on them.  The disks start on
the left rod, in order of size, with the largest disk on bottom and the smallest on top.  The goal is to move the
disks to the right rod with the following restrictions: a) disks must be moved one at a time, b) a disk may never
be placed on top of a smaller disk.

Towers of Hanoi can be represented using three stacks, and I've done this for you already.  Your goal is to write
an algorithm to solve for any n (up to at least 15).

There's several ways to solve the problem.  Not all of them are recursive, but I've found the recursive ones to be
far easier to code.

This can be a pretty tough problem.  I recommend finding an online tower of hanoi game and playing with it.  Solve for
1 disk, then 2, then 3, etc... Think about how do you solve for X disks, if you assume you can solve for X-1.

One hint: The HanoiSolver.Solve method is not written to be recursive.  You'll probably want to write a private Solve
method that takes different parameters, and have the public Solve method call that.  Similar to what we did with the
StringHelper.Reverse methods.
