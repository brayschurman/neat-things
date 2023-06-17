# Normalization: An Elven Tale of Orderliness

Normalization, a discipline practiced by the wise elves, is the process of efficiently organizing data in a database. There exist various stages, known as normal forms, each depending on the previous, much like an intricate story passed down through the ages. Herein, we shall delve into the first three. Learn more about it on [Wikipedia](https://en.wikipedia.org/wiki/Database_normalization).

## The 1st Normal Form: The Single Valued Cell

In this form, we ensure:

-   Each cell is single valued, akin to an elf focusing on a single task.
-   Entries in a column are of the same type, much like an elven kin sharing the same lineage.
-   Rows are unique and uniquely identified, as each elf is distinct and has a unique name.

> **For instance**, [Spotify](https://www.spotify.com/) uses unique identifiers for each of its songs, albums, and artists, thus ensuring that each row is unique and uniquely identified. They also ensure that entries in a column, such as 'song duration' or 'artist name', are of the same type.

## The 2nd Normal Form: The Dependence on the Primary Key

At this level, we adhere to the principle of each attribute (non-key column) being dependent on the primary key. It mirrors the elven way of life where everything depends on their ruler, the primary key.

> **For instance**, imagine a table in Airbnb's database named 'PropertyBookings'. Here, we would only need 'PropertyID' and not 'PropertyName', since the name can be determined from the 'PropertyID', much like the elven king's decree determining the actions of his subjects. Airbnb would employ such a strategy to ensure that their booking data adheres to the second normal form.

## The 3rd Normal Form: "Nothing but the key"

This form abides by the adage "Nothing but the key", emphasizing the elimination of transitive dependencies. It requires all fields to be only determinable by the primary key, similar to the way an elf's lineage is defined by their ancestor's name.

> **For instance**, a Spotify table containing 'SongID', 'AlbumID', and 'AlbumReleaseYear' properties exhibits a transitive dependency. 'AlbumReleaseYear' depends on 'AlbumID', which in turn depends on 'SongID'. To adhere to the 3rd Normal Form, 'AlbumReleaseYear' should be moved to a separate 'Albums' table and referenced there, much like the elven practice of associating characteristics with specific elven clans.

Want to delve deeper into database normalization? Visit this comprehensive guide at [StudyTonight](https://www.studytonight.com/dbms/database-normal-forms.php).
