how to combine the data depends on the use case of the app. in this case, the user will most likely only ever work on one device, especially at the same time, which means that there won't be conflicting writes for the majority of the time.
what will be important in the future though is that the data is uploaded to the servere right away, so other people can get live updates of somebody elses workout.

the state management is set up to a big part. the state object should have just one other class where it requests and receives data from, where the data comes from should be handled in this other class, I'm not sure if this is the correct name but for now I will call this the 'repository'.

## repository
in the repository, there is a function for all the crud operations.
reading: the repository should ideally return data as fast as possible, therefor returning the offline data would be the most responsive and fast experience. in almost all cases, this data will be correct anyways, but sometime this could potentially be old data. eg: the user wants to edit a workout plan, but the workout plan is the old version, and the user clicks on edit before the ui is updated with the new version, this could cause issues. 

maybe, at start up, the app could request all changes from the database once and sync them locally, and then consider the offline database as the source of truth. this would cause the app to have a long load time though potentially.

in most cases the app would run as offline only app as well, and then only updates to the database would be nice. so maybe just syncing on start of the repository, while at first displaying offline data, and then in the worst case overwriting it if newer data comes from the server would be fine.

the online database should, unless a new device is being populated, never return data for queries. the online database just returns the data where the timestamp is newer then the latest device sync. it should also only recieve data from the device queue.

## syncing from online
the app could just call for the changes since latest sync from online, and the then integrate all changes into the offline database upon receiving the data. after successfully doing so the latest sync variable would be updated.
good: the database could be synced independently from the ui and states. ie even if nobody called or listened to bodyweight yet, the bodyweight table would be synced.
downside: if the data would only be received after the repository had already displayed the old offline data, how could the state be updated with the new data?
fix: not sure if this is the best fix, but either also returning a data stream from the repo (sounds like it is then just a copy of the state) would fix the issue of updating the state, or maybe this online sync class could have access to the states. but then it would need to have access to potentially infinitely many states, also ones that haven't even been created yet.

maybe there 

## queue
when the device writes data, the data is written directly to the offline database, but also pushed into the queue. this queue will then handle the writing to the online database. it should try to push upon receiving new data, but also retry either in intervals or simply when the device goes back online (could use an online stream from a flutter package).
this queue is also stored on the device, probably inside a map with the database table name as key and a json of the data as value. the server will the handle this data.
question: is it better to recieve and handle json in the server or would it be better to do the supabase calls in the app?
question: what is the best way to store the queue data in the app for now?

## mock process
a ui element is created that need that needs data from a state. 
the state is created and the fetch function is called
the state calls the fetch function in the repository
the repository is created and the fetch function executed.
the repository 


# new process see crdts and hybrid logical clocks
