# Behavior Trees
- Used to program complex behaviors in AI, games, and robotics.
- Nodes are executed (ticked) with a given frequency
    - child will immediatly return 
      - *running* to parent if the execution is under way
      - *success* if it has achieved its goal
      - *failure* otherwise
- Choosing what logic to encapsulate in the BT versus the actions is an important design decision
  
## Advantages 
- More expressive than FSMs
- Efficient creation of complex systems in a *modular* and *reactive* fashion
- Used often in robotic manipulation tasks since they allow individual behaviors to be reused in the context of another higher level behavior

## Control Flow Nodes
- **Sequence**- ticks each child node in order
    - returns running upon ticking a node that returns running
    - returns failure upon ticking a node that returns failure
    - exits if failure or running are reached and doesnt tick any of the nodes after it
    - returns success only if all the children return success
- **Fallback**- ticks each child node in order
    - Returns succes or running upon reaching a child that returns one of them 
    - Returns failure if all the children it ticks return failure 
    - AKA selector/priority selector nodes
- **Parallel**- set a success threshold
    - ticks all the children from left to right
    - returns success if the number of children that return success is past the set threshold
    - return failure if the number of children that return failure is greater than N - M 
    - otherwise returns running if any of the children are still running
- **Decorator**- manipulates the return status of the child according to a user-defined rule 
  - has a single child
  - selectively ticks the child according to a predefined rule 
  - Examples:
    - Invert- inverts success/failure status
    - max-N-tries only lets its child fail N times then will always return Failure without ticking the child
      - useful if you dont want to keep calling a command on a system that went down
    - Max-T-Sec lets the child run for T seconds then if it is still runnning will return failure without ticking the child
- Control flow nodes can have memory meaning they remember what a child returned success or failure in order to avoid re-exceution until a whole sequence or fallback finishes

## Execution Nodes
- Leaf nodes are execution nodes (2 types)
- Action- executes a command when it is ticked
    - returns success if the action is correctly completed
    - returns failure if the action has failed
    - returns running while its running
- Condition- checks a proposition when ticked
    - returns success or failure depending on if the proposition holds
    - never returns running 

## Other Control Flow Architectures
- **Petri Nets** provide an alternative to FSMs that supports design of concurent systems
- **FSMs**
    - Pros
      - Common
      - Intuitive and easy to understand
      - Easy to implement
    - Cons
      - Poor maintainability/scalability since they are essentially goto statements
        - Less modular and harder to maintain since they use one-way control transfer (state transitions) just like go to statements
        - This means removing a state from a machine requires changing all transitions to that state
      - Poor reusability since transitions often depend on many internal variables
      - Scalable
- **Hierarchial FSMs (HFSMs)**
    - aka state charts
    - uses super states that contain many substates to simplify transitions 
- **Subsumption Architecture**
    - related to behavior-based robot architecture 
    - have several controllers, each implementing a task, running in parallel
    - controllers are ordered in priorty by user and the highest priorty controller out of a list of ones that want to control the robot is given access to the actuators w
- **Teleo-Reactive Approach**
- **Decision Trees**
    - directed tree representing a list of nested if then clauses to derive decisions
    - leaf nodes- decisions/conclusions/actions to be done
    - Non-leaf nodes- predicates to be evaluated