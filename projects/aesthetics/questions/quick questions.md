
how to organize documentation?
is something like this as .md with github a valid approach?

service for exercises and exercise draft

how to organize "components" like exercises (file structure)

how to organize parts of these components like exercises and exercise drafts

active workout list can skip appstate loading indicator right?

documentation:
how much time to invest?
why not do it in obisidian rather than blank text files


active session all in one state or multiple states
pro one state:
- simpler
- less boiler plate
- easier to sync with database

cons:
- small changes cause big ui updates
	- but only thing really changing is the exercise list, which would be a sinlge state as well
- "tight coupling"?
- state has many responsibilities

pro multiple states:
- seperated into little blocks

cons:
- hard to keep all in sync
- a lot of boilerplate
- much work for no real upside?