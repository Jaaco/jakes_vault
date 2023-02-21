there are two major ways in which this can be implemented:

## Single Workout Exercises
- both of type workout exercise
- connected via property with superset id
- connected visually
- arbitrary exercises can be pulled together to supersets
- reordering exercises can destroy or expand supersets

## Compound Workout Exercises
- all superset exercises within one card
- reordering doesn't affect supersets at all
- visually completely obvious
- would make things like not doing the first set of the first exercise possible
- harder to implement
- extremly hard to safe this way in database
- same effect could be achieved with old backend, and combining them just for the UI

