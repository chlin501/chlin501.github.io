# What is it?

A minimum finding algorithm. It's compries two parts:

    1. Preprocessing phase

    2. A sequence of iterations

# Preprocessing Phase (Setup)

    1. Every entity exchanges its Id with its neighbors. 

    2. The entity will orient the link toward the largest id. 

        * The entity x has id 5, with its neighbor y having id 7. The link is 5 -> 7.

        * Both sides will do the same. So at the entity y, the link is 5 -> 7.

## Property 

    * Directed acyclic graph 

        * 3 types of Nodes

            * Source (local minimum)

            * Sink (local maximum)

            * Internal Node

## Consequence

Every node knows its role (source, sink, or internal node)

# A Sequence of Iterations

# Reference 

[1]. [Design and Analysis of Distributed Algorithms.](http://people.scs.carleton.ca/~santoro/DADA-CourseNotes.html)
