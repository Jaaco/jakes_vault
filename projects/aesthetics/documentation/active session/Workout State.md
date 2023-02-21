so the main 'poblem' is that the state is of type AppState<WorkoutM?>, and ideally it should not be nullable (Adrians input)

### why it was nullable
AppState just provided the status of the database fetch, and wether it was null or WorkoutM decided if there existed an active workout

### ways to achieve it
since the WorkoutsState already reflects the same AppState from the database, this could be used as the 'has it loaded or not' layer in the UI. and then, AppStateReq in WorkoutState could stand for is there an active workout or not.

my issue with it:
here AppState is used in 2 different, but connected, places in 2 different ways. In WorkoutsState it stands for the connection to the database, in WorkoutState it stands for state of 'is there an active workout', and has nothing to do with the database

I will implement this now, this might be subject to change later
