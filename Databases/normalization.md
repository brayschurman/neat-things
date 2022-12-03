# Normalization

Of course, each form depends on the previous.

## 1st Normal Form

* Each cell is single valued.

* Entries in a column are of the same type.

* Rows are unique and uniquely identified.

## 2nd Normal Form

* All attributes (non-key columns) dependent on the primary key.

For example, if we have a StudentProject table, we only need ProjectID and not ProjectName, since the name can be determined from the ProjectID.

## 3rd Normal Form

"Nothing but the key"

* No transitive dependencies.

* All fields must only be determinable by primary key
  
For example, a table containing these three properties, PlayerID -> PlayerSkillLevel -> PlayerRating

PlayerRating is a transitive dependency, it should be put into a PlayerSkillLevel table and referenced there.
