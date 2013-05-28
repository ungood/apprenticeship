Assignment #2 - Reverse a string
--------------------------------

The goal of this assignment is to get you a bit familiar with the C# syntax (which should look fairly similar to
C++, but with classes) and unit testing. I've pushed a change to your TestRepository with a C# solution (Visual
Studio's word for a collection of related projects) containing 2 projects (or in C#, assemblies).  The first project
"AssignmentsCore" will contain the source code for this (and possibly future) assignments.  It contains a class
"StringHelper" with a single public method "Reverse", which should reverse a string - you will provide the implementation
for this method.  The AssignmentsCore assembly is setup to be a console application, and contains a simple main function that will
test the StringHelper.Reverse method.  You should be able to build and run the whole project, and test it manually
that way.

However, there are better ways to do testing.  This brings us to the second assembly, AssignmentsTest, which
will contain unit tests written to test the functionality of code you write.  For this assignment, I've written
the unit tests for you (as a professor might do, for grading a large number of student assignments).  In future
assignments, you'll write the unit tests too - because writing good tests is part of writing good code.

Unit testing
------------

Testing is a complicated, and important part of writing good code.  There's many ways to do testing, such as:

* Acceptance Testing: This is when you "finish" a project and the client starts testing to make sure it does
  what they paid you to do (or the professor tests it to make sure it does what he asked).
* Manual Testing: This is what you do when you're writing the code, and constantly keep rerunning the thing
  to make sure it works.  The problem with this kind of testing is that you have to keep re-testing it every
  time you make a change.  Maybe you broke the widget module while fixing the cookie factory.
* Automated Testing: Maybe you get smart, and you write a bunch of scripts that run your program and test it
  for you.  This is a kind of black-box testing where all you care about are the inputs into the program, and
  the outputs.  A SDET (software developer engineer in test) will typically write suites of scripts to do this
  kind of testing for complicated software.
* Integration Testing: This is a type of automated testing that tests multiple pieces of software working together.
  Maybe it tests that Program A can write a record to a database, and then Program B will read that record and do
  something with it.
* Unit Testing: This is what we are concerned with here.  Unit tests are automated tests that are written to test
  the smallest "unit" of code that makes sense to test alone.  Typically they are written in the same language
  as the code being tested, by the same person who wrote the code to begin with.  Good unit tests should test as
  few classes as possible, be simple, run quickly, and test (or "cover") as much of the code as is feasible.
  
Unit testing is a difficult art.  It's easy to make your tests too complicated (and risk being slow, and therefore
not run often enough), or to actually write tests that test the wrong thing, or to make your code overly complicated
in order to test it.

However, good unit tests are amazing tools.  They will make your code simpler (code that is simple to test is generally
simple to read, maintain, and change in the future), and if done write, will give you confidence that your code is
correct, even as you refactor it to make it simpler.  In addition, someone who writes good tests rarely ever starts
up the debugger - the unit tests do all the troubleshooting for him.

For C#, there is a unit testing framework called NUnit (aka ".NET Unit", a port of jUnit, a Java unit testing framework).
I've already downloaded it, and referenced it correctly in the AssignmentsTest project.

Steps
-----

* You'll need to "git pull" the changes to the repository that I made to your local machine.
* If you're using VS 2012, you're in luck, do this:
  * Go to "Tools -> Extensions and Updates"
  * Click "Online" on the left
  * Search for "NUnit Test Adapter"
  * Download it to install (you may have to restart)
  * Now you can simply right click in one of the test methods and "Run Tests"
  * You can also debug tests in VS, which is sometimes nice.
* If you can't do the above for some reason, you'll need to download the NUnit test runner
  * http://www.nunit.org/index.php?p=download
  * Install the win MSI
  * Make sure you've built the Assignments solution.
  * Start NUnit
  * Create a new project (call it whatever, store it somewhere you'll remember)
  * Project -> Add Assembly...
  * Find "AssignmentsTest.dll" in your project directory, under "AssignmentsTest/bin/Release"
  * Now you can run tests - they're in a tree, so you can run all of them, all from one class, or just one in particular.
* Okay, now that you can build and test the code, go implement the StringHelper.Reverse method.
  * You may need to spend some time getting familiar with C#.  I'll leave this to your own direction.
    It's a bit different from C++ in some key areas, but it should be fairly familiar.  The main thing
    to note are that all code must be in a "class" which is like a struct with methods.  This is what
    it means to say that C# is "purely" object-oriented.
  * Try to come up with a solution the reversing a string problem on your own without searching for it.  The
    solution is pretty straight forward if you consider a string as just an array of characters.  Let me know
    if you need hints, hints are okay.  It can be hard to learn a new programming language and solve a problem
    at the same time.
* Once you get the tests to pass, commit your changes to git, and push them up to github.

Feel free to ask me any questions, of course.
