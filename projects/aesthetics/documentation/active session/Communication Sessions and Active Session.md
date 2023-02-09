## Problem

these two states have to communicate in some way in order for
- ActiveSessionState to get initial session or null from SessionsState
- SessionsState to recieve an update of every change in ActiveSessionState

## Solutions

### Don't Sync

in theory ActiveSessionState could write to repo by itself
only need to get initial session, could be handled by widget
pros
- less code
- easy solution
cons
- not possible to display active session in calendar
- app is not really "in sync"

 this would be lazy and suboptimal, so this is not gonna be the way

### Mediator as Service

a mediator handles the interactions between them
eg. mediator as singleton in the style of a service that holds both states
pros
- handles all interactions without tight coupling
cons
- has to implement a function for every single crud operation of ActiveSession
- would have to be called by the widgets, tightly coupling it to the widget tree (if that makes sense)

### Mediator as Listener

maybe there is a solution where a mediator could be made that listens to one or both states and can inform the other of changes
this would work really well to sync the continuing changes of ActiveSessionState to SessionsState

the question remains: how can SessionsState inform ActiveSessionState of the initial session once the read from database has occured?


pros
- no explicit functions have to be called by the widgets (UI)
- works on top of existing sturcture
- nothing breaks if you add it or take it out
- less code, only needs to listen to any changes and invoke one function on change
- simpler, less error prone
- as loosly coupled as I can think of right now
cons
- don't know how to implement it exactly
- need to figure out who holds this object or instantiates it
- still leaves open the question of how ActiveSessionState gets the initial session

#### Initial Session Problem

##### Sessions just calls ActiveSessionService

this would be the easiest solution and would fix the problem in one line. But this tightly couples the states which I wanted to avoid

##### Mediator as Listener

maybe the same pattern that I wanted to use in the first example could be used here as well
a mediator that this time works the other way around:
- listens to state changes in SessionsState
- filter the state changes: only if state change goes from Req or Err to Ok the changes will be pushed to ActiveSessionState