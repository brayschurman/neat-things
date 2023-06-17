# Caching: A Wizard's Perspective

## The Conundrum of Cache-based Storage

Ah, dear friend, the journey to entrust thy data in a nimbler, yet more bounded, storage system be fraught with unique trials and tribulations.

## In the Search for Data

When in need of backend data, one would be wise to first seek in the [cache](<https://en.wikipedia.org/wiki/Cache_(computing)>). Should fortune smile upon you and the sought data be found therein, you need only make use of it, saving yourself the laborious quest of unearthing it from the far slower depths of main storage.

> **Note:** Utilising the cache can hasten data retrieval, diminishing the need to venture into the main storage.

Alas, if the sought data remains elusive in the cache – a circumstance known amongst the common folk as a 'cache miss' – then one must brace oneself for the arduous journey into the depths of the main storage. Yet, once the treasure is unearthed, it would be wise to place it in the cache for future use.

## A Lesson from the Elves: Caching within Spotify

To better understand this magic within the bounds of a web application, let us examine [Spotify](https://www.spotify.com). Contemplate how they employ caching to manage elements like the play count of a song. If a certain melody gains the favour of many, constantly updating the database with each replay could slow the rhythm of the system, placing undue burden on the database.

Instead, the more elegant strategy is to increase the play count in a cache, a place much quicker due to its memory-based nature, with each replay. Then, when the time is right, transfer the accumulated count back into the database in one swift motion.

```javascript
const NodeCache = require('node-cache');
const myCache = new NodeCache();

// Store something within the cache
myCache.set('song1234PlayCount', 0);

// Later, when a song is played
let playCount = myCache.get('song1234PlayCount') || 0;
playCount++;
myCache.set('song1234PlayCount', playCount);

// At specific intervals, the cached play count is saved to the database and the cache is cleared
let finalPlayCount = myCache.get('song1234PlayCount') || 0;
myCache.del('song1234PlayCount');
// At this point, finalPlayCount would be written back into the database
```

In a realm as vast as Spotify, a distributed cache would be the wisest choice so that all servers might share in the same cache data.

The game of cache management can indeed be a "tricky" business, as one must ensure the two copies of data (the cache and the main storage) remain in harmony. This battle is known as cache invalidation and is considered a daunting foe. Thus, I wish thee luck in your endeavours.

Cache Invalidation: A Tale from Middle-Earth

Listen closely, young hobbit, for cache invalidation is not a tale to be spun before the fainthearted. It's the dark sorcery of ensuring that a mere facsimile of data held in the cache aligns with the original, oftentimes secreted away in a deep and mysterious database or long-term repository. One must tread this path with the caution of Bilbo sneaking past Smaug, for it's fraught with potential pitfalls and inconsistencies as confounding as Gollum's riddles.

In this shadowy realm, various strategies exist, each with its unique blend of merits and perils:

## Time to Live (TTL): The ticking timepiece of data

This method is as simple as Samwise, yet it can sometimes be as effective as Frodo. Each piece of data in the cache is granted a lifespan, a ticking clock as inexorable as the march of the Ents. When the end comes, the item is discarded as stale as lembas left forgotten in a pack. When next you seek this data, it will be drawn anew from the deep mines of the database. But beware, for this method can be as treacherous as the paths of Moria. Should the original data transform before the TTL expires, you're left with an outdated phantom, a stale ghost of its former glory.

## Write-Through: The unbreakable vow

This method binds the cache and database together in an unbreakable bond, strong as the fellowship itself. Every whisper to the cache is echoed in the echoing halls of the database simultaneously, ensuring their unity like a well-coordinated orchestra of elves. The price for such harmony? The speed of your write operations will be slow, as sluggish as a Treebeard's stride, for they are confined by the slow rhythm of the database.

## Write-Back (or Write-Behind): The fleeting speed

Ah, the deceptive allure of speed, as tempting as the One Ring itself. Writes are cast to the cache, leaving the duty of informing the database for a later time, just as Frodo postponed his mission. Indeed, it might seem an elegant solution, as your write operations are swift as a Great Eagle. However, do not be entranced. The complexity of the spell increases, for now you must prepare for scenarios akin to the cache receiving the data, yet the database write failing like a broken sword.

In this perilous journey through the dark arts of cache invalidation, one must never forget the ominous shadow of complexity, particularly in the realms of distributed systems, where multiple caches lurk like Nazgûl in the night. The chosen strategies rely heavily on the unique demands of your application, such as the freshness of data, the tolerable latency, and the degree of data inconsistency you dare to brave. Often, one finds themselves weaving a tapestry of these methods to achieve the desired outcome, much like creating a grand map of Middle-Earth.

Remember, cache invalidation is not a child's play, but for those who master it, it becomes a powerful tool, a weapon against the dark forces of inefficiency. Tread carefully, and may the light of Eärendil guide you.

# Caching: The Lore from the Shire

## The Boons of Caching

### The Tale of Latency and Throughput

In our tale, the roles of the swift-footed messenger and the diligent scribe take form as a memory cache, such as the trusted companion [Redis](https://redis.io/) or [Memcached](https://memcached.org/). They perform their tasks with a haste that dwarfs that of the steady databases akin to [MySQL](https://www.mysql.com/) or [PostgreSQL](https://www.postgresql.org/). Why so, you ask? These nimble caches exploit the swiftness of the realm of RAM, while their steadier counterparts rely heavily on the deliberate pace of disk-based storage. Even when compared to the most advanced solid-state disk, the agility of RAM soars like an eagle above the Misty Mountains.

> **Example**: Visualise a scribe, tirelessly scribbling onto a parchment (akin to a cache). The speed and efficiency of this method greatly outshine the painstaking labor of etching onto a slab of granite (a comparison to a database). Just as our scribe takes advantage of the parchment's expedience over the stone, so do memory-based systems over their disk-based counterparts.

### The Skirmish of Consistency vs Speed

Now turn your gaze towards the homely scene of a bakery in the Shire, a mirror image of a caching system. The baker, with the agility of a nimble hobbit, bakes bread and sells them without the burden of recording each loaf's destiny. Alas! Should an unforeseen fire (or a system crash) consume the bakery, the precious loaves in the oven (or the unsaved data) may succumb to the flames. This bustling bakery stands in stark contrast to a meticulous factory, symbolic of a database, methodically noting every loaf's creation and destination, thus moving at a slower, yet steady pace due to these additional tasks.

> **Example**: The Battle of Consistency versus Speed: Databases carry a weighty burden of overhead due to the multitude of features they offer, like transactions, consistency, and durability, akin to the many tasks of our factory. Contrarily, caching systems like Redis follow the mantra of 'scribble and disregard', operating with a freedom and speed that can be jeopardized by a system crash, a risk many deem acceptable in caching scenarios.

### The Journey of Network Latency

Consider now a courier, tasked with delivering a light missive (representing small cache data) to a neighboring hamlet or lugging a substantial trunk (symbolizing large database data) to a distant metropolis. While the journey (akin to the network operation) is laborious, delivering a letter (writing to the cache) is undeniably quicker than transporting a heavy trunk (writing to a database).

> **Example**: On Network latency: Although the network operations required to write to a distributed cache may be arduous, the data inscribed into the cache often pales in size compared to that inscribed into a database.

### The Art of Batching

Lastly, imagine a diligent postman, amassing letters (analogous to cache updates) from the homes of the Shire. Rather than darting off to the post office (a metaphor for the database) after each pickup, the postman collects all letters before delivering them in one efficient journey. This approach mirrors the art of batching in caching, optimizing time and conserving energy, while easing the burden on the database.

> **Example**: When using a cache before committing to a database, one can employ the technique known as batching. This involves gathering all modifications before delivering them to the database in one fell swoop,
