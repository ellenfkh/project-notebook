# Design notebook for week ending November 16, 2014

## Description

This week, I settled (more or less) on the syntax for the declarations, and
updated the IR and parser to reflect that syntax.  Right now, the IR supports
only parent-child relationships, and also has a dummy Self relationship for
single, unconnected nodes --- since the graph is an edge list, unconnected
nodes would otherwise be unreachable.  Examples of the syntax can be found in
`src/test/scala/treeTracer/parser/parserTest.scala`.  I've also gotten rid of
the triangular parent-parent-child relationship I had before, which was causing
problems because triangular edges in an edge list are awkward.  The Parent and
Child relationship classes now also have a third, redundant argument, "parent"
and "child" respectively, so that later I might be able to create a generic
Relationship class to support user-defined relationships.

I've also written tests for the parser, which are passing!  It's super
exciting.  At the moment, the parser doesn't do reciprocal relationships ---
for instance, if I say 

```
Fred is child of Freddy
```

then I get the `Child(Fred, Freddy, "child")` relationship, but no
corresponding `Parent(Freddy, Fred, "parent")` relationship.  I couldn't figure
out how to do that in the parser, so I might end up having to do a semantic
pass specifically to add those in.

## Questions

I need to design my querying syntax.  The main query I want to support will be
something along the lines of

```
Who is Fred to Freddy?
```

which should return something like `Fred is Child of Freddy`.  If there are
more complex relations, for instance

```
Fred is child of Freddy
Freddy is child of Fredina

Who is Fred to Fredina?
```

I think a preliminary behavior would be to return something like `Fred is Child
of Freddy is Child of Fredina`.  Later, I might be able to compress this and
generate a new direct edge between Fred and Fredina, getting `Fred is
Grandchild of Fredina`.  I'm not sure how to do this, though.  It would
probably require reading up on some graph algorithms.  Thoughts?

Another problem I'm having right now is that my semantic pass for making
reciprocal relations isn't working because of immutable set problems.  I think
that's just a question of reading the docs.

I also need to think about what other queries (if any) I want to support, and
how to implement them.  Any ideas on what would be useful for the user?


I worked about 4 hours this week.  Should probably step it up next week. :(

## Post-critique summary

## Post-critique reflection
