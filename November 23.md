# Design notebook for week ending November 23, 2014

## Description

I realized this week that I'd completely neglected to account for my DSL
actually being two DSLS, one for declaring and one for querying.  Because of
this, I had to rework my IR and parser quite a bit.  I also decided to use a
read-eval-print loop instead of reading in a text file, to make the DSL more
interactive.  This required changing the semantics, and also another pass at the
parser.

The IR's AST now splits into two "branches", one for edges and one for queries.
Both have subtypes for the specific edge or query (though there's only one kind
of query right now).  I also got rid of the Graph case class, since it was
basically a wrapper over Set[Edge] and was getting in the way. I might want to
add it back later for abstraction reasons, but I doubt it.

The parser is now significantly simpler than it previously was.  The main
differences are that it now parses directly to edges and queries, without going
through more parse subfunctions; this is better since my syntax is very flat,
and doesn't really need a tree structure.

The semantics have changed such that the eval function takes both a parsed AST
and a set of edges, and returns an updated set of edges.  This turned out to be
the easiest way to handle dealing with some commands with side effects
(declarations) and some without side effects.  The eval loop has to store the
graph after every step.

Left to implement are:
* the actual query engine, which means graph algorithms yaaaaay
* more relationships (or user-defined ones?)
* a gui (to make it more than just a sad Prolog-clone?)

## Questions

I don't really have any questions, I think.  Right now, I think I have a pretty
good idea of where to go next.  If nothing else, I guess I'd like feedback on
whether user-defined relationships are a good idea.  They seem like they'd be a
decent amount of work, though possibly not too bad if I could manage to make
everything a generic relationship with a classification string instead of
matching on case class.  If you think user-defined is a bad idea, then what
predefined relationships should I choose?

I spent about 7 hours this week on this project.  About three of those were
totally useless and dead ends, and a lot of the rest was figuring out how to
rededesign around the query half of the langugage, so not much actually got
done.

## Post-critique summary
* Get querying up
* Add more relationships
* Dealing with reciprocal relationships should NOT be in the parser, interpreter
should handle it
* Graphs! Do a "connect" pass over the graph to make all possible edges?
* Suggestions on the type of queries to include

## Post-critique reflection
As the critique suggested, I got querying set up (only kind of, but the
framework is there).  The meat of it will have to wait for graph algorithms.  I
decided not to add more relationships right now, since I can always do that
later, and if I've written my DSL well, it should be pretty trivial.

The suggestions for the queries are good, I added them in and then took them
back out for now.  As with the other relationships, I'll try to put them back in
once the DSL works with the basic stuff I have now.

I think the "connect all possble edges" approach is not feasible, given that
it'd have to be recalculated after every step in the eval loop; there might be
ways to make it fast given that I'm adding only one edge, or two at most (with
reciprocal edges), but it's still probably not optimal.  Also, given that that
could possibly end up a fully connected graph stored as an edge list, it'd also
be expensive in space.  Instead, I think I'll try to use a search algorithm that
returns the path between two people (or all paths from one person to everyone,
or to another person, or whatever), and then "collapse" only that/those
path(s) with another pass.



