# Raft Leader Election

## Notes

* Initially 

    ```
    Stopped --(start up)--> Follower
    ```

* Leader sends periodic heartbeat

* Election Timeout

    * No heartbeat communication is received by a follower

    * A new election is triggered by the follower

### Begin a New Election

* Follower 

    * transits to **candidate** state

        ```
        Follower --(transit)--> Candidate
        ```

    * votes itself (as leader)

    * requests vote (via RequestVote message) from all members in the cluster

    * checks if one of following happens

         a. it wins the election

             - Receive votes from majority of servers

         b. another server becomes the leader

         c. a period of time no winner occurred


* Follower

# References

[1]. [In Search of an Understandable Consensus Algorithm
(Extended Version)](https://web.stanford.edu/~ouster/cgi-bin/papers/raft-extended.pdf)
