# Design notebook for week ending December 7, 2014

## Description

This week, I redesigned the IR so that the graph of people was represented as a
map from Person to an edge list instead of simply a giant edge list.  This was
necessary because I want to do some sort of graph search to resolve queries, and
an unorded set of edges is a bad representation for any sort of graph algorithm.

I also decided to get rid of predefined relationships (ie. Child, Parent) and
instead am using a generic Edge case class, with an identifier string as one of
its values.  The user can therefore declare any arbitrary relationship between
two people.

In terms of functinality, I've added the load and delete commands, and
implemented a depth-1 query resolver.

The load function takes a file with a program using the same syntax as the event
loop and executes it; it's a way to pull in a larger universe without having to
type it all in again.  There's an example load file in `/resources/fred.txt`.

The delete function removes a person from the universe, as well as all edges
that reference that person.

The depth-1 search (flatSearch) function takes in two people `x` and `y`, and
searches for a direct relationship between `x` and `y`.  It only succeeds if the
set of edges associated with `x` includes one or more edges to `y`.

In addition to the new functinality, I also improved the output formatting to be
more readable, and updated the parser tests.

Next week, I want to improve the search to be arbitrary depth, instead of flat.

## Questions

How do you think I should go about doing the search?  I'm considering whether or
not to implement some sort of depth-first-search myself, or try to look for a
library to do it for me.  The problem with using a library is that I'll probably
have to convert my IR into what the library wants, and then convert it back
again, and it might be more work than just implementing search myself.

I also want to add some semantic tests, but don't know how.  The trait we were
using for external-lab wants the eval function to return an int, but my eval
returns a `Map[Person, Set[Edge]]` instead, so it doesn't complile.  Did you run
into similar problems?

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**
I worked about 10 hours this week.

## Post-critique summary
* I forgot to to a project notebook last week. :(
* Real-time queries would be nice but maybe a reach goal?
* Since we're coming to the end of the semester, maybe start thinking about
feature freeze and make the current set work better.

## Post-critique reflection
* Yeppp.  I didn't check for deadlines because I was busy being lazy over
Thanksgiving break. :(
* I have real-time queries now!  The read-eval-print loop works.  The goal now
is to make querying less pathetic.
* Stopping and fixing up my current feature set is a pretty good idea.  I really
want to get better queries up, but I think my current implementatiton of things
is actually good enough to do a prototype demo with.  I'll keep the demo in mind
next week, and probably stop somewhere around Wednesday to focus entirely on
polishing things up for the demo.
* Real-time queries would be nice but maybe a reach goal?
* Since we're coming to the end of the semester, maybe start thinking about
feature freeze and make the current set work better.
