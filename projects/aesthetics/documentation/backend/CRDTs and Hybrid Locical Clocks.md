https://www.dotconferences.com/2019/12/james-long-crdts-for-mortals
https://jaredforsyth.com/posts/hybrid-logical-clocks/
https://cse.buffalo.edu/tech-reports/2014-04.pdf
https://github.com/jlongster/crdt-example-app/blob/master/shared/timestamp.js

## Hybrid Logical Clocks
hlcs record the physical time, a logical counter and the node id.
the physical time can be bound by a max clock drift in case one wall clock is too far off. the node id is used for tiebreaks in case of equal physical and logical parts of the hlc. the node id is probably just the device id.

###  Saving Process to Database
a value is changed in the app
the current value of the local hlc is incremented
the table, row id, column, new value and hlc are compiled into one message
message is added to online and offline queue, or make one queue with bool fields online successful, offline successful
message is sent to database
offline queue seems stupid, since this will be an offline sqflite table in itself
upon recieving the data in the db, it has to compare the old and new timestamps and then write these

### main question for now:
where is the timestamp saved to?
just to the row?
one new column per field called 'field_name_hlc'?
inside the field with a delimeter? ugly af...

https://github.com/cachapa/tudo/blob/master/app/lib/crdt/tudo_crdt.dart
this seems to be doing it on a row basis

#### hlc per row
in this case, as far as I can see, the whole row data has to be sent every time an update to a field is made
example why I think that:
if there are two clients updating row 1
client a updates field x first but is offline
client b updates field y and syncs to db, saves field y and hlc
then if client a goes online and uploads the changes, the database will see a later timestamp and discard the changes
then, client a receives the changes from the serves, sees the later hlc and integrates it into it's own db 
in this case client a would locally update field y and leave his own changed field x, while the server and client b still have the unchanged field x

therefor, the upload message for a row based hlc would have to include the whole data of the row, in order to ensure convergence of the data on all clients

## message to James Long
Hey James!
I'm Jacob, a 23 year old Flutter dev and AI bachelor student and I'm working on an app.
I was stuck for 2 months on how to do my own syncing to create an offline first app for better UX, because being tied to Google's Firestore didn't seem like a scalable solution. (black box, pricey, offline for long periods is not really meant to work perfectly, limited offline cache sizes...). So I was completely psyched when I stumbled upon your talk about crdts and hlcs. Thank you so much for providing this content, this should be way more mainstream knowledge, especially in the Flutter  community as well.

I had one question about the specific implementation though: in your example, every change is uploaded with an hlc, table name, column name, and a new value. then these changes are applied to the database, if they lie after the current hlc. But where do you store the hlc in the actual table? Having it per row does not seem enough, since this would lead to issues if two clients update different fields of the same row, the later one would not receive the changes of the first one? Or do you have an extra hlc column for every regular column? (this seems overkill)
Or do you embed the hlc AND the value inside where the regular value would go? (seems to make queries stupid since the data would have to be processed to not show the hlcs)
Or am I misunderstanding completely and there is no HLC data in the tables at all? But then I don't see how a client would accept any changes that come from the server that are timestamed 'yesterday'?

Thanks for providing all this value and thanks for taking the time to read my problem!
With kind regards, Jacob

# analyzing James Long's GitHub Example
https://github.com/jlongster/crdt-example-app

in client/sync.js I found what seems to be the answer to my question

#### hlc per message
you find all messages (since last sync?)
then the client compares them with the existing changes
(it creates a map with all existing changes that maps the new message to a list of the existing messages for this dataset, row and column. the existing messages are sorted first) not what's happening

how can this work when all messages in question are just the ones passed in, no old vs new?

when parsing the messages, the internal hlc clock should be updated with the clocks of the received messages as to not be behind. if a new message would be received and if it had a newer timestamp than the current local timestamp, then changes done locally would be discarded later by the server. 

the actual database doesn't hold any data of the timestamps. just the table of messages has the timestamps. when applying messages, all messages relevant to this table, column and row have to be sorted, and every changed that hasn't been applied yet will be applied in the correct order. 



maybe include a new table on the client side with foreign user id + table + row id to indicate that changes on foreign objects should be watched as well

