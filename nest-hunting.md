# Nest Hunting

# Phases

1. Search

2. Assessment

    * Evaluates nest based on various criteria

3. Recruitment

    * Tandem run

    * Infection style dissemination

    * Quorum  threshold 

4. Transport

    * Picking up and carrying other ants from the old to the new nest

# Random Thoughts

* Each node can be poster

* Each node is equipped with persistent storage locally

* Each node can receive request (vote) from a client outside colony to trigger the process

* Each node once receive the request, immediately saving the request (containing the client info) to its local storage - (A)

* Each node e.g N then (after A) start tandem run requesting other nodes to persist its (i.e. node N's) proposal and node N changes its state to Tandem run (rejecting other request) - (B)

* Each node (after B) that receives its peer request for persist the proposal do the same (request other nodes to persist proposal) - (C)

# References

[1]. [Distributed House-Hunting in Ant Colonies](https://groups.csail.mit.edu/tds/papers/Radeva/PODC15.pdf) 
