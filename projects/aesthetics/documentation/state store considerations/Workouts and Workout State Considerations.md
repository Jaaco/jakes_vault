# Before, Firebase
in firebase a big problem where the reads, and trying to keep them as little as possible.
Now what I did at first was download all Workouts from the database, since it was considerably less read-intensive just downloading all at once rather than reading some multliple times for stats, the calendar and so on. This brought a big problem with it, all the state was in one Workouts State, and everybody that needed access to any sessions had to communicate back and forth with it.
This made particularly syncing the active workout with all workouts hard, since changes had to be made in both states, as well as in the database.

# SQL Considerations
when using sql, reads won't be as much of a consideration. Many changes can be made regarding the structure of the project. This should help with the following areas:
- tight coupling
- state syncing issues
- 'talking to database for somebody else'
- readability and clean code
- more options for pagination
- potentially less downloaded data in total


## Still Working Out
can I just use the offline cache right away? This way I would hardly ever have to cache any data, most could be gotten from database and displayed right away. This would mean less data in the state, and easier to manage.

specific implicatios

### Workouts in Calendar as just Dates
The database could be queried to just return the dates of workouts, that's all that's needed for the calendar widget on the calendar page.

### Workouts in Calendar Page one by one
Upon clicking on a date in the calendar, the relevand data for this particular date could be retrieved. No need to store the dates of all workouts in one state.

### Charts
for many charts, the relevant data for 