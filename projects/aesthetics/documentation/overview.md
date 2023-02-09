**this app will be seperated by components. the structure of the documentation is very similar to the structure of the code.**


# Purpose

## General Purpose

## User Groups

## Uniqueness in Market


# Structure

## Components
 [[Exercises Overview | Exercises]]
Active Session
Calendar
Workouts
Blueprints
Bodyweight

## Terminology


### **at 08.02.2023**

#### Session
a 'session' or 'workout' that was done
includes the exercises with set, rep and weight numbers
with start and end time

#### Exercise
the model of an exercise, describing what it is
name, equipment, muscle groups, etc


#### Workouts
this describes a 'blueprint' of a session
this is a 'session' or 'workout' that has not been done yet
this could 

#### Plans
a plan that is done over multiple weeks
like a mesocycle or a simpler version of it
a succsesion of planned 'workouts', with start and end date

### **Problems**
a 'session' is usually refered to as workout in common language
the distinction between a session and workout is maybe hard to understand
a plan could maybe be confused with a planned workout as well

**suggestions**

#### Sessions -> Workouts
this would make sense to most people
'Today I had a hard workout.'

#### Workouts -> ???
ideas:

##### Workout Blueprints
'Blueprints' is a word that is not commonly used in this context
has to be explained

##### Planned Workouts
better, but kind of implies that this workout is already planned for a date

##### Workouts Plans
better than previous. doesn't imply that it is set for a day as much

##### Workout Routine
competes with Workout Plan

##### Routine
just calling it routine gives it  clearer distinciton as 'Workout Routine'
but I don't like the word

##### Workout Draft
props lorena
best so far, more concise than plan, nicer work than routine


#### Plan -> ???

##### Plan
a good name for it alread, but doesn't really mention what is planned. Could be a sinlge session, multiple sessions?
inconcise

##### Cycle
sounds like hopping on gear

##### Meso Cycle
this may only be a subset of what 'Plans' in this app could do
maybe there are plans without 'lenght' or end date, no fatigue tracking and no rir.
If you strip all of these things from a Plan, is it still a Meso Cycle?

##### Split
commonly used term
describes the purpose really well


**conlusion for now**

**Session -> Workout
Workout -> Workout Plan / Routine
Plan -> Split**


## Reasoning of this Structure
the reasoning behind this structure is to seperate the different parts of the app into seperate blocks. This should avoid problems in the future where parts might have to be taken out or expanded. If all parts of the app are tightly coupled this will interfere  with maintainability.
The code should be easy to debug. These seperate packages should also be able to be used in different places in the app, should the need arise. 




# Coding Principles

## Maintainability

## Consistency

### State Management

### Coding Conventions

### Frameworks and Packages

## Documentation
