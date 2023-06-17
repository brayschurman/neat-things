# Caching

-   about storing data in a faster but also smaller storage system

-   when you want to access some backend data, you first check if it's in the cache. if it is, use that data and save the time of fetching it from the slower main storage.

-   if the data is not in the cache (a "cache hit miss"), you fetch it from main storage and also store it in the cache for potential future use.

In the context of a web application like Spotify, caching could be used to store things like the play count of a song. If a song is played very frequently, updating the database every time someone plays it could be very slow and put a lot of load on the database server. Instead, every time the song is played, the play count could be updated in a cache (which is usually memory-based and hence faster), and then every so often, the cached count could be written to the database in one go.

Here's a simple JavaScript example using node-cache, a simple caching module for Node.js:

```js
Copy code
const NodeCache = require( "node-cache" );
const myCache = new NodeCache();

// Put something in the cache
myCache.set("song1234PlayCount", 0);

// Later, when a song is played
let playCount = myCache.get("song1234PlayCount") || 0;
playCount++;
myCache.set("song1234PlayCount", playCount);

// Periodically, you'd write the cached play count back to the database and reset the cache
let finalPlayCount = myCache.get("song1234PlayCount") || 0;
myCache.del("song1234PlayCount");
// Here you'd write finalPlayCount back to the database
```

This is a very simple example and real-world usage can be more complex. For example, in a distributed system like Spotify, you'd likely use a distributed cache so that all servers can share the same cache data.

Caches are be "tricky" because you're dealing with two copies of the data (the cache and the main storage) and you need to make sure they stay in sync. This is known as cache invalidation and is widely regarded as a hard problem. Good luck, soldier.
