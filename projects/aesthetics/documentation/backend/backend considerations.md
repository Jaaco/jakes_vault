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

