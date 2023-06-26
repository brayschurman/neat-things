# Database Normalization

Each form of normalization depends on its predecessor.

## 1st Normal Form

- Each cell contains a single value.
- Entries in a column are of the same kind.
- Rows are unique and identified uniquely.

> **Example**, in Airbnb's case, if we have a 'Guest' table, it's better not to have columns for 'GuestName' and 'GuestAddress' in the same table. Instead, we should create separate tables for 'GuestName' and 'GuestAddress', and then reference these in the 'Guest' table.

## 2nd Normal Form

- All attributes (non-key columns) are dependent on the primary key.

> **Example**, for Airbnb's 'PropertyBooking' table, we only need 'PropertyID' and not 'PropertyName', as the name can be determined from the 'PropertyID'.

## 3rd Normal Form

- "Nothing but the key" - no transitive dependencies.
- All fields must only be determined by the primary key.

> **Example**, suppose Airbnb has a 'HostRating' table with the properties 'HostID' -> 'HostExperienceLevel' -> 'HostRating'. This table isn't in 3NF because 'HostRating' is a transitive dependency and should be moved to a separate 'HostExperienceLevel' table, then referenced from there.
