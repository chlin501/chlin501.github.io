# Note

  * The information here is ripped from the paper [1].
 
# Protocol

  * The protocol samples the arrival time of heartbeats.

  * The protocol maintains a sliding window of the mostrecent samples.

      * The (sliding) window is used to estimate the arrival time of the next heartbeat.

  * The distribution of past samples is used as an approximation for the probabilistic distribution of future heartbeat messages.

# Concepts

## Unreliable Failure Detector

### Properties

  1. Strong completeness

      * There is a time after which every process that crashes is permanentlysuspected by all correct processes

  2. Eventual strong accuracy

      * There is a time after which correct processes are not suspectedby any correct process 

## Quality of service of failure detector

  * Detection time TD

      * The time that elapses since the crash ofpanduntilqbegins to suspectppermanently

      * This definition relates to completeness

  * Average mistake rate λM

      * This  measures  the  rate  at  which  a  failure  detector generates wrong suspicions.

      * This relates to the accuracy of the failure detector

# Accural Failure Detector

  * Accrual failure detectors output suspicion information on a continuous scale.

      * The higher the value, the higher the chance that the monitored process has crashed.

## Architecture

  * Receiver (Supervisor)

      * Monitoring 

          * Gather information (from supervisee)

      * Interpretation

          * (Gathered) Information is and interpreted

      * Action

          * Respond to trigger suspicions

          * Done by Application

      * Accurual Failure Detector merely performs monitoring operation whilst Application performs Interpretation and Action.

## Definition

  * A failure detector that outputs a value associated with each of the monitored  processes. 

### Properties 

  3. Asymptotic completeness

  4. Eventual monotony   

  5. Upper bound

  6. Reset 

# φ-Failure Detector

## Principle

  * φ*p* 

      * φ p = 0, no confidence at p (that p has crashed).

      * φ p = ∞, lute confidence that p has crashed.

  * Formula

      ```
      φ p = −log 10 (1 − P acc )
      ```

## Implementation

  * History *H*: Arrival intervals of heartbeat messages per a monitored process.

  * Window *W*: A set of histories of the processes.

  * Aₖ: The arrival time for the *k*-th heartbeat message.

  * H*q*:

# Reference

  [1] [The φ Accrual Failure Detector](https://pdfs.semanticscholar.org/11ae/4c0c0d0c36dc177c1fff5eb84fa49aa3e1a8.pdf)

  [2].[Two-ways Adaptive Failure Detection with the φ-Failure Detector](http://citeseerx.ist.psu.edu/viewdoc/summary?doi=10.1.1.4.3455)
