# Caching

The decision to house data in a more agile, albeit restricted, storage system brings about its unique set of challenges and benefits.

## Cache-based Storage and Its Merits and Challenges

Choosing to entomb data in a sprightlier, albeit limited, storage system yields its distinctive trials and tribulations. When the requirement arises to access backend data, the first place to scrutinize is the cache. Should you be fortunate enough to unearth it there, you merely utilise that data, sparing yourself the onerous task of excavating it from the significantly slower main storage.

Alas, if the data fails to grace the cache – an unfortunate circumstance colloquially known as a 'cache miss' – one must undertake the expedition to fetch it from the main storage. Nevertheless, you then display the wisdom to house it within the cache for future endeavors.

## Caching within Web Applications: A Spotify Case Study

To better grasp these principles within the parameters of a web application, take Spotify as an instance. Reflect upon the use of caching to manage elements like the play count of a tune. Should a specific melody bask in the limelight of popularity, incessantly updating the database with each replay could morph into a dreadfully slow undertaking, exerting undue pressure on the database server.

A more artful stratagem would be to increment the play count in a cache (predominantly memory-based and therefore swifter) with each replay, and then, at judicious intervals, decant the amassed count back into the database in one fell swoop.

```javascript
const NodeCache = require('node-cache');
const myCache = new NodeCache();

// Stash something within the cache
myCache.set('song1234PlayCount', 0);

// Later, upon the playing of a song
let playCount = myCache.get('song1234PlayCount') || 0;
playCount++;
myCache.set('song1234PlayCount', playCount);
```

// At measured intervals, the cached play count is returned to the database and the cache is purged
let finalPlayCount = myCache.get('song1234PlayCount') || 0;
myCache.del('song1234PlayCount');
// At this juncture, finalPlayCount would be inscribed back into the database

// At measured intervals, the cached play count is returned to the database and the cache is purged
let finalPlayCount = myCache.get('song1234PlayCount') || 0;
myCache.del('song1234PlayCount');
// At this juncture, finalPlayCount would be inscribed back into the database
In the realm of a distributed system like Spotify, it would be advisable to employ a distributed cache so that all servers might partake of the same cache data.

The game of managing caches can indeed be a "tricky" endeavour, owing to the duel of the two data copies (the cache and the main storage) to maintain synchronisation. This battle is recognized as cache invalidation and is reputed to be a formidable opponent. Hence, I bid you good fortune in your endeavours, soldier.

## Cache Invalidation

Listen closely, cache invalidation is not a subject for the faint of heart. It's the dark art of ensuring that a mere copy of data held in the cache aligns with the original, often sequestered in some database or long-term repository. One must tread this path with caution, for it's riddled with potential pitfalls and inconsistencies.

There are various strategies, each with their own merits and disadvantages, mind you:

Time to Live (TTL): A simplistic, yet sometimes effective method. Each piece of data in the cache is given a lifespan, a ticking clock, if you will. Upon reaching its end, the item is discarded as stale. When next you seek this data, it will be fetched anew from the database. But beware, for this method is far from perfect. Should the original data alter before the TTL expires, you're left with outdated information, a stale ghost of its former self.

Write-Through: This method ties the cache and database in an unbreakable bond. Every whisper to the cache is echoed in the database simultaneously, ensuring their unity. The price for such perfection? The sluggish speed of your write operations, as slow as a Mandrake's growth, for they are limited by the slow drawl of the database.

Write-Back (or Write-Behind): Ah, the deceptive allure of speed. Writes are cast to the cache, leaving the responsibility of informing the database for a later time. Indeed, it might seem an elegant solution, as your write operations are as swift as a Golden Snitch. However, do not be fooled. The complexity of the spell increases, for now you must prepare for situations where the cache successfully receives the data, yet the database write fails.

In this perilous journey through the dark arts of cache invalidation, one must not forget the ominous shadow of complexity, particularly in distributed systems, where multiple caches lurk. The chosen strategies heavily depend on the peculiar demands of your application, such as the freshness of data, acceptable latency, and the degree of data inconsistency you dare to tolerate. Often, one finds themselves weaving a tapestry of these methods to achieve the desired outcome.

Remember, cache invalidation is not a child's play, but for those who master it, it is a powerful tool. Tread carefully.

## Why is caching useful?

### Latency and Throughput

The concept of Latency and Throughput: When penning an entry into a memory cache, such as Redis or Memcached, you will find that it proceeds with far greater celerity than scrawling to a database, akin to MySQL or PostgreSQL. The reason being, these caches primarily exploit the swiftness of RAM, whereas the databases rely heavily on the sluggishness of disk-based storage. Even the most advanced solid-state disk pales when juxtaposed with the agility of RAM.

Conjure in your mind a scribe, feverishly transcribing onto parchment (akin to a cache). The speed and efficiency of this method greatly outshine the painstaking labor of etching onto a slab of granite (a comparison to a database). Just as our scribe takes advantage of the parchment's expedience over the stone, so do memory-based systems over their disk-based counterparts.

### Consistency vs Speed

Visualize a humble local bakery, the quintessence of a caching system. The baker bakes bread swiftly and sells them without meticulously documenting each loaf's destiny. However, should an unforeseen fire (or system crash) consume the bakery, the loaves within the oven (or the unsaved data) may succumb to the flames. Now contrast this with a large-scale factory, emblematic of a database, laboring methodically, recording every loaf's creation, and consequent destination, thereby operating at a slower pace due to these additional tasks.

#### Example

The Battle of Consistency versus Speed: One must not ignore that databases bear the weight of additional overhead, primarily due to the plethora of features they provide. These include transactions, consistency, and durability, to name a few. While undoubtedly essential for various operations, they invariably impose lethargy on the databases. Contrarily, cache systems usually follow the mantra of 'scribble and disregard'. Taking Redis as an instance, it doesn't feel the compulsion to inscribe every piece of data onto the disk instantaneously (though the configuration for such a task exists, but at the cost of speed). Such disregard bestows speed but also implies that a system crash might result in the loss of recent entries. A concession, though, many find acceptable in caching scenarios.

### Network Latency

Now, consider a courier, bearing the task of delivering a missive (representing small cache data) to a neighboring hamlet or lugging a substantial trunk (symbolizing large database data) to a distant metropolis. While the journey itself (akin to the network operation) is time-consuming, dispatching a letter (writing to the cache) is undeniably quicker and less arduous than transporting a heavy trunk (writing to a database).

#### Example

On Network latency: As you astutely observed, network operations required to write to a distributed cache are rather languid in nature. Yet, the data penned into the cache is often a mere shadow in size compared to the data inscribed into a database. In the realm of your play count scenario, you would merely increment a counter in the cache, as opposed to spawning an entirely new row within the database.

### Batching

Lastly, imagine a postman, amassing letters (analogous to cache updates) from a multitude of residences. Instead of darting off to the post office (a metaphor for the database) after each pickup, the postman strategically collects all letters before delivering them in one efficient trip. This approach, much like batching, optimizes time and conserves energy, all while minimizing the load of write operations to the database.

# Example

The Art of Batching: When one opts to inscribe into the cache before eventually committing the same to a database, it opens up the opportunity to employ a technique known as batching. Rather than running to the database each time you modify the cache, you instead periodically gather all your modifications and deliver them to the database in one fell swoop. A strategy you'll find is significantly more efficient.
