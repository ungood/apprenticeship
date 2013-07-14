Hash tables
----------

Hash tables are another interviewer favorite.  In fact, they're probably the #1 most used data structure in
Amazon interviews.  And, on top of that, they're useful for almost everything.  If I had to rank the data
structures I use most often on real projects, it would go: lists, hash tables, arrays.  In many languages,
hash tables are basically how classes are implemented, so suffice to say they're important.

To explain a hash table, it might help to use an example.  Suppose I was working at a university, and I wanted to
store students so that I could easily look them up by a 9-digit student ID.  I might have a class called Student, with
properties for StudentId, FirstName, LastName, etc...

One solution would be to store them all in an array or a linked list.  It would be fast to load into memory, and be
memory efficient, but searching would be problematic - to find a student by id would require scanning the list and
comparing the student id of each to the one I'm looking for.  At best, the student would be at the front of the list,
and so it would be O(1), but at worst it would be at the end O(n).  The average case would be O(n/2) which is just
O(n).  That's not terrible, but consider we might have several hundred thousand student entries (past students,
applicants, etc...) and it's not great.

Another option would be to sort the list of students by ID (maybe you do something smart, and store them in the
filesystem already sorted, so you just load them that way).  Now, we can do a binary search (if you haven't
learned about binary search, go read up on it, it's a good recursive algorithm to know), which is O(lg n), which
is significantly better.  But, we have a different problem now.  Either we have to keep our list sorted, which means
inserting or removing into our list is no longer O(1), or we have to sort or list every time we want to look something
up... and that sort is O(n lg n), which is worse than just scanning the list.

Now, like all trade offs, either of these two options may be fine.  It depends on your use cases.  If you only rarely
insert or delete students, but need to search often, option #2 is good enough.  If, on the other hand, you often insert
and delete students, but very rarely need to search for them, than option #1 might be acceptable.

However, there's another option - a hash table, which has some of the benefits of both, with (of course) some different
downsides.  But before we go there, let's describe a third option:  You could simply decide to store students in an
array, using the student id as the index.  Student #123456789 would be stored in students[123456789].  This is a fairly
reasonable thing to do if your range of ids is small and fits in memory.  Insert, remove, and search all all O(1).  But,
if your data is sparse (you have less students than the range of possible student ids), you're wasting a bunch of
memory with null entries.  And, if your range of values is too large, it becomes impossible to fit it all in memory
at once - it's probably not possible (and certainly isn't smart) to allocate a 1-trillion student array to store a few
hundred thousand students.

Thus, enters the hash table.  Instead of storing students in an array by their student id, we will come up with some way
to map student ids to an array index, and store them based on that code.  So, Student ID #123456789 might map to code
1337, and we would insert that student at students[1337], and likewise, we would know to look for that student there
when searching.  Inserting, removing, and searching would still be O(1) (as we'll see, this is average case), but we
would be saving a bunch of memory.

Hash codes
----------
The code that you calculate to store an item in a hash table is called a hash code.  For any given hash table, you
need to be able to consistently calculate array indices from key values (in our example, student ids).  It needs to
be a consistent calculation, because you must get teh same index when you store an element as when you search for it.

For integers, this is usually pretty simple.  If your array is size N, then all you need is the modulus of your key by
N (key % N) or equivalently, the remainder after dividing by N.  x % N will always result in a number between 0 and N-1.

So, a very simple hash table for integer keys might be something like:

  const int Size = 100;
  Student[] students = new Student[Size];
  
  void Put(Student student) {
    int index = student.Id % Size;
    students[index] = student;
  }
  
  Student Get(int studentId) {
    int index = studentId % Size;
    return students[index];
  }
  
However, what if your key is not a number, but, for example, a string?  Well, luckily all things stored on a computer
are ultimately numbers, so as long as you can convert your key into an int, you can then use the same procedure as
above to find the hash code.  For strings, a common way to do this is to just add up the numeric value of all the
characters in your string and use that as the hash code.

Collisions
----------
If you were paying attention, you'd note that there is a problem with our simple hash table above.  What do you do
if multiple student ids map to the same index?  Our simple hash table might map multiple students to index 3, for
example, and whichever one was added last would overwrite the previous ones.  That's not (usually) what we want.  This
is called a hash collision.

Collisions are usually inevitable with hash tables.  For obvious reasons, you can't store hundreds of thousands of
students in an array with 100 elements.  So, you have to handle collisions somehow.  And there are many, many ways to
do so.  We'll discuss two:

One way would be, instead of having an array of Students, would be to have an array of lists of students.  Then, when
we put a student in our hash table, we calculate the hash code and add it to the list (sometimes called a bucket) at
that index.  To find a student by id, we calculate the hash code, then search the proper list until we find the student
with that id (if we reach the end of the list, no such student exists).  This strategy is called "chaining".

Another way would be to allocate a bigger array of Students - at least big enough to hold all our students - and have a
back up plan if we get a collision.  One such backup plan would be to try storing a new student at the correct index,
but if that one is full, to increment the index until an empty spot is found.  Then, to find a student, we start at
the correct index, and keep looking until we find the id.  If we come to an empty spot, we quit looking.  (One problem
with this strategy is that it's hard to remove items - we'll leave empty spots all over the place.)  This streagy is
called "probing".

Runtime Complexity
------------------
With collision resolution, we now have a workable solution.  But is it efficient?  Well, let's examine both collision
strategies:

For chaining, inserting is always O(1) (assuming inserting into your bucket is O(1)).  Searching is O(1) to lookup
the correct bucket, then O(N/M) average case to search the buckets, where N is the number of things to store, and M
is the number of buckets.  With an M close to N, then this is close to O(1) for searching.  However, there's a trap
to watch out for: this assumes our keys hash uniformly to buckets. If we come up with a bad hash code, we might
accidentally put all of things in one bucket... and then we're back to O(N) for searching.  (For example, what would
happen if all our student ids end in 0, and the number of buckets we have is a multiple of 10?)

Probing is a bit more complicated.  The runtime of both inserting and searching depends on how full our array is.  As
we insert more and more things, the likelihood of a collision increases, and the more spots we have to iterate over
to find an empty spot.  I won't go over all the math, but it works out that inserting and searching is pretty efficient
and close to O(1) when the array is <70-80% full for this type of hash table.

Implementation Details
----------------------
So, to actually implement a hash table for a given type, that type needs to meet a few contracts:

1. The type must have a key.  Sometimes this is a natural key (user accounts often use the email address as the key
for the user account, because they are already unique), or artificial (student ids are an arbitrary number that
a university gives to a student to make sure all students have a unique id - you aren't born with a student id).
2. The key must have a method to calculate the hash code.
3. The key must also have a method to determine if two keys are equal.

In C#, we might define some interfaces to define types that could be stored in a hash table.  It might look something
like:

  public interface IStoreable {
    IHashable GetKey();
  }
  
  public interface IHashable {
    int GetHashCode();
    bool Equals(IHashable other);
  }
  
Then we could write a hashtable that stores anything that implements IStoreable.

However, storing things in hash tables is so common that C# decided to build these things into the Object class - which
is the class that all other's derive from.  All objects already have a GetHashCode() method and an Equals() method.

For numeric basic types (int, long, etc...) the hash code is just the number itself, and the equals method just returns
this == other.

For strings, the hash code is as described above (actually it xors all the characters together instead of adding them,
but it's similar), and the Equals method is a case-sensitive equals.

For other objects (such as Students, or Cars), the hash code is based on the concept of reference identity - ie: two
objects of type Student are equal if they point to the same location in memory, and the hash code is calculated from
the memory location.

This is not always ideal (for example, you may want Student objects to be considered equal if they have the same
Student Id, even if you happen to have two objects in different memory locations), so you can overrride the GetHashCode
and Equals methods for classes you define, if you want to use them as a key in a hashtable.

Assignment
----------
Finally, the assignment! You will implement a hash table using either the chaining or probing method for conflict
resolution.  You will also implement two ADTs - IMap and ISet - which are often implemented with hash tables (though
like most ADTs, can be implemented in a variety of ways).  Maps are simply the abstract definition of what a hash
table does (store items by a key), and are also known as dictionaries (e.g. C# calls them this) or associate arrays.
Sets are related to the mathematical notion of a set - a collection of distinct things - where you don't really 
care to search, you just want to know if the set contains some element.

Like before, I'll provide the interfaces to implement, and a stubbed hash table class, but I won't provide the unit
tests - it's your turn to write them.
