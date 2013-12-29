# Database Drill Intro To Sqlite 
 
##Learning Competencies 

##Summary 

 Remember to enter the <a href="https://plus.google.com/hangouts/_/event/cn84s0i6f761j9rpv4a3ljddg0o?authuser=1&hl=en" target="_blank">collaboration hangout.</a> *Please turn off your video and sound. Use the chat function.*


[SQLite](http://en.wikipedia.org/wiki/SQLite) is a really simple relational database.  Every database is a single file, which you can move around.

You should already have SQLite installed.  The default way SQLite displays data is not great though, so paste the following into your Terminal:


```bash
cat << EOF > ~/.sqliterc
.headers on
.mode column
EOF
```

Creating a database in SQLite is simple.

```bash
sqlite3 dummy.db
```

Will put you into the "sqlite" shell prompt, which looks something like this:

```text
SQLite version 3.7.13 2012-06-11 02:05:22
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite>
```

Adding a schema is easy too!  If you wanted to create a <code>users</code> table, you can paste the following into the sqlite shell and hit **enter**:

```sql
CREATE TABLE users (
  id INTEGER PRIMARY KEY AUTOINCREMENT,
  first_name VARCHAR(64) NOT NULL,
  last_name  VARCHAR(64) NOT NULL,
  email VARCHAR(128) UNIQUE NOT NULL,
  created_at DATETIME NOT NULL,
  updated_at DATETIME NOT NULL
);
```

It should look like this, afterwards:

```bash
SQLite version 3.7.13 2012-06-11 02:05:22
Enter ".help" for instructions
Enter SQL statements terminated with a ";"
sqlite> CREATE TABLE users (
   ...>   id INTEGER PRIMARY KEY AUTOINCREMENT,
   ...>   first_name VARCHAR(64) NOT NULL,
   ...>   last_name  VARCHAR(64) NOT NULL,
   ...>   email VARCHAR(128) UNIQUE NOT NULL,
   ...>   created_at DATETIME NOT NULL,
   ...>   updated_at DATETIME NOT NULL
   ...> );
sqlite>
```

Read this article about [SQLite Datatypes](http://www.sqlite.org/datatype3.html) for more information what <code>VARCHAR</code>, <code>DATETIME</code>, etc. mean.

<!--Anxious to move beyond the command line and use SQLite in Ruby?  You can interact with SQLite in Ruby using the [sqlite3](https://github.com/luislavena/sqlite3-ruby) gem.  Install it by running:

```bash
gem install sqlite3
```
-->
## Objectives
### Create a dummy database

Create your own dummy database in SQLite, and create a users schema as shown above.

### Insert some data

You now have a table, so let's insert some data!  Paste the following into the sqlite shell:

```sql
INSERT INTO users
(first_name, last_name, email, created_at, updated_at)
VALUES
('Jessie', 'Farmers', 'jesse@devbootcamp.com', DATETIME('now'), DATETIME('now'));
```

And go ahead and get the data out of the table!  Run this:

```sql
SELECT * FROM users;
```

Now add a new entry to the database with your own name and email.  Run another select statement to see both entries.


### Multi-line commands

The Sqlite3 shell is made to take multiple line commands.  So if you just type in `select * from users` and hit enter, nothing happens.  Only when you end the query with a `;` and hit `return` does the query run.

This allows SQLite to take a multi-line `INSERT` statement like the one above.  This primarily helps with readability, sometimes a more complex query can be hundreds of characters!

Now try adding Jessie to the database again, with the same data as above.  Did you get an error - `Error: column email is not unique`?  If so, can you track it down?  Make sure all your data is there by running your select statement, and try again.


### Add a column

Now add a column to the users table for "nicknames".  You'll need to use the `ALTER` statement. Make sure you add the correct type for the nickname `VARCHAR(64)` and that it is a mandatory field - ie `NOT NULL`. If you make a mistake, don't worry!  Just `.quit` out of SQLite, delete the `dummy.db` file and start over again.

Make sure the schema was updated by typing `.schema`.  Your new `nickname` column should appear last.

Now add a nickname for Jesse (he likes "pookie butt") and one for yourself.  Use the `UPDATE` statement.

Use a select statement to see the database entries, they should include the new nicknames!

Need help?  This [tutorial](http://zetcode.com/databases/sqlitetutorial/) may provide some insight.

### Change a value

Oops.  Jesse's not so pleased about his new nickname.  He's also not so pleased that his name was spelled wrong. We need to change all three of these things!
Jesse's correctly spelled name is "Jesse Farmer" and he'd likely be less perturbed with a nickname like "Ninja Coder".

Check out the [tutorial](http://zetcode.com/databases/sqlitetutorial/) for some help.  You should be able to do this with a single line SQL statement!

And don't forget to update the `updated_at` column.  It should be the current time.  (Hint: Look at the original `INSERT` statements.) BTW, when you get into development with Rails, the `updated_at` column will be managed for you.

Use a select statement to see the database entries, they should include the correct spellings and updated nickname.  Nice work!

###Submit your console history

Copy all your previous commands from the SQLite console, paste them in the gist, and submit! 

##Releases
###Release 0 

##Optimize Your Learning 

##Resources