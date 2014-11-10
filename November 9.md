# Design notebook for week ending November 9, 2014

## Description

This week, I finished (maybe) the IR and started the parser.  I'm not entirely
sure about my IR setup; it seems like doing a search over such an IR would be a
complete pain.  I'm not sure whether to deal with that in the IR or later, in
the semantics.  I also haven't tried to compile yet --- that's something I should
look into next week.

Basically, I think the IR might have to be a lot more complicated than it
currently is (which is pathetically simple).

## Questions

Any opinions on how to make the IR less dumb?  I feel like the current one is
probably workable, but would be completely un-extensible.

**How much time did you spend on the project this week? If you're working in a
team, how did you share the labor?**

I spent about 7 hours this week.  A lot of that was just sitting around thinking
about the IR, and I'm still not quite happy with it.  It ended up with a really
simple implementation, but I think that's going to have to change.

## Post-critique summary
There's a lot of sheer programming (and therefore maybe not so much design).
Maybe the design could be increased by doing more complicated syntax or adding
more extensibility.  Another thing might be visualizing the tree.

## Post-critique reflection
Agreed that there's a lot of sheer programming if I'm just doing the current toy
child-parents relationships.  I might get around to doing more extensibility ---
at the very least, I want to keep that option open, which is already giving me
some design headaches since I don't want to make life difficult for me later.  I
don't think I'll do visualization as part of the class project --- it's not
design, and it's probably kind of a sheer programming pain.  I might do it after
the class ends, as a personal side project.
