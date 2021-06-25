# Rubbish obedience 

## Properties

  * Id

      * A distributed unique/ comparable hash value (e.g. 123 -> 7b and 111 -> 6f, then 7b > 6f)

  * Role: Leader/ None

      ```
      trait Role
      case object Leader extends Role 
      
      // a function that returns a node's role
      trait Node {
        def id: String // sip hash
        def role: Option[Role]
      }
      ```

## ID Generation

  * Distributed hash id 

      * Determinstic[1] 

      * Default to sip hash

  * TODO (Improvment)

      * Based on some properties of the node that a **better** (e.g. performance) node would produce larger id

## Assumption

  * All ndoes in the group is sound - meaning no node is in a vicious cycle where a node is constantly crashes, starts up. 

      * The node in a constant crashing and start-up cycle should be improved by excluding that node (with failure detection to record and consult the historical status records e.g. consecutively 3 times crash-startup then that node is excluded though it still stays in the group list.

  * The group member is fixed/ static (dynamic membership may be considered later on)

  * A node may crash and recover

  * No Byzantine failure

## Time of `Russhish Obedience` can be started

  * When a group is formed i.e. all members are joined

## Phases

  1. Group Creation

      * Nodes start to join in order to form a group

  2. Obedience (actual logic)

  3. Stable phase (for query)

## Failure Detection

  * Phi Accural failure detector or

  * SWIM failure detector (for lesser message generation)

## PROs and CONs

  * PROs

      * No vote procedure is required

  * CONs

      *  Message generated grows when the nodes are increased (??? need test)

## Phases Detail

### Group Creation Phase Messages

  * Join(`the node's id info`)

  * Group(`memembers info`)

  * Exchange(`the node's id info`)

### Obedience Phase Messages

  * Obey(`the sender's id info`) 

      * sent by follower

      * act as follower's ack

      * sent to the leader

  * Confirm(`leader's id info`)

      * act as leader's ack

      * send to follower

      * send by leader

  * During this phase, leader is not determined yet

### Stable/ Determined Phase

  * Leader is determined

  * All nodes (in this phase) can reply the current leader when receiving Obey or WhoIsLeader message

  * WhoIsLeader

      * asked by any nodes (in the member list)

      * repied by the node in this phase only with CurrentLeader message

  * CurrentLeader(`current leader id info`)

      * sent by the nodes in the stable phase 

      * requestor will go back to Obedience phase to re-obey the leader

### Group Creation

  1. When the node starts up

      * the node creates its own distributed unique id 

  2. The node X joins another node Y (to form a group)

      * the node X exchanges its own id (and related info) with the node Y it tries to join

      * the node Y being joined sends the group list it holds to the node X

      * the node X talks to the members in the group in exchaing id (and related info)

### Rubissh Obedience 

  * Check if a higher id (than its own) exists

      * if yes

          * then simply follow the leader (does not need to compare the id, even its id is higher than the leader) by sending `Follow(its own id)` to the leader

      * if no

          * compare its id with the rest of nodes' in the list it holds

              * if itself holds the highest id, wait for other nodes to obey

                  * if no Obey messages received from lower ids and it's the highest id (meaning there is a leader exists after its own comparison)  

                      * then it send obey message to the second highest id node <----- this needs to be examined

              * if its id dose NOT hold the highest id, then it sends Obey message to the leader

  * A refresh start obedience (election) logic is no difference than that when a node crashes then recover

# Examples

  A. Happy path - Fresh round

      * All nodes check the id in its member list, finding the highest id

      * Send Obey message to that highest id

  B. When the node having highest id fails

      * All nodes check the id in its member list, finding the highest id

      * When recovering, it wlll wait for receving Obey message from other nodes but no nodes will obey because another leader is obeyed

          * A a period of time (how long???), the node having higest id will broadcast who is the current leader query to the nodes in its own member list

          * The rest of nodes who receive the query and in stable phase will reply the leader node they obey

          * The node having the highest id once reives the current leader id info would then issue obey message to the current leader

   C. When the node (non highest id node) fails 

      * when recovering, it will send Obey message but since the leader is not the highest and the onde who receives this (obey) message (and in stable phase) will reply with CurrentLeader(...) message, replying with the current leader id info to the query node; or the receiver (who receives Obey mesage) will reply Confirm message

# References

  [1]. [SipHash: a fast short-input PRF](https://www.aumasson.jp/siphash/siphash.pdf)
