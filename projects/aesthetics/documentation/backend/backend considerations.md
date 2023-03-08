as of now, 10.02.2023, the backend is firebase.
only exercises and bodyweight have been implemented yet

### considerations 10.02.2023
I was planning on using it for the MVP. I thought having less than 1000 reads per user per session within the first year sounded very reasonable, but it will be hard to migrate later. so now I would have the opportunity to set it up the right way, which would allow me to seamlessly expand later.
Now I have the problem that I really need online and offline sync. Adrian suggested Supabase, but I don't know if this handles offline. Having seperate online and offline backends and syncing by hand seems like it would set back the launch by a month. I don't want to build something that I will have to spend a lot of time on to change later.
monetary considerations: 
firebase should definitely be swapped out sooner than later.
appearently you can host supabase on your own server (don't know how expensive or time consuming that is) and only pay for cpu costs (have no idea about that yet)
appwrite is also an option, of which I know that you can host it yourself.

now it's just a question of what I can best sync with the offline database (could be sqflite)
and also what structure fits best to my data, and what is the most commonly used one, in case I get associates or need to switch database later

Supabase + Floor + Stock
https://blog.xmartlabs.com/blog/get-flutter-offline-support-in-supabase/

Supabse pricing
https://supabase.com/pricing

## considerations 04.02.2023
good comment on implementation: https://www.reddit.com/r/FlutterDev/comments/n14wvf/sync_solution_for_local_sqlite_to_remote_mysql/

I've looked innto multiple things, prisma, brick, flutter cache...
all these packages are either poorly maintained, offer bad documentation or use alot of generated code
I'm trying to implement my own database syncing. to do so I will use supabase and sqflite and write some code that manages the syncing between the two.

### spitball aproach
save last synced datetime to shared preferences
on intervals or events check database for new data
update shared preferences with new sync datetime and merge online changes into offline database - missing details 
crud offline first saves to offline database
also writes these changes to some queue
this queue waits for connectivity, has multiple tries and so on. when connection is available, data is sent to server (transaction?)
if server received data, queue is emptied
server then has to merge data with existing database - missing details

## database usage for gym tracker app
most users will have 1 device from which they use the app.
sometimes users will have it downloaded on 2 devices, but even then it will hardly ever be used on both phones at the same time.

later, trainers should be able to view training sessions live, but this will be read only, so this should not interfere.
for now, in 99.9% of the cases it can be trusted that the newest data is the source of truth. if the lastChangedDateTime is newer then this will persist.

### issue with indices in lists
biggest issue right now: what happend to data that is in an ordered list, who keeps the index? the index should be part of the child, since this is the sql way to doing things, and it is also relevant for statistics to the children, not to the parent.
if the index and parentId are a composite index, which would be a functioning index, then what happens on reorder? during changing all of the indices, some composite index errors will happen, unless the changes happen sequentially in the right order and await each other.
addition: this doesn't have anything to do with it being a primary index, the same problem would arise if it would be selected by workoutId and index in list. the only way to go around this is to just give them uids, in which case they could be selected without the need for being careful with having two indices equal at the same time

