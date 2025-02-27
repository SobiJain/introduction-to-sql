# INSERT

To add data to your database, you would use the `INSERT` statement. You can insert data into one table at a time only.

The syntax is the following:

```
INSERT INTO table_name(column_name_1,column_name_2,column_name_n) VALUES('value_1', 'value_2', 'value_3');
```

You would start with the `INSERT INTO` statement, followed by the table that you want to insert the data into. Then you would specify the list of the columns that you want to insert the data into. Finally, with the `VALUES` statement, you specify the data that you want to insert.

> The important part is that you need to keep the order of the values based on the order of the columns that you've specified.

In the above example the `value_1` would go into `column_name_1`, the `value_2` would go into `column_name_2` and the `value_3` would go into `column_name_x`.

Let's use the table that we created in the last chapter and insert 1 user into our `users` table:

```
INSERT INTO users(username, email, active) VALUES('greisi', 'g@devdojo.com', true);
```

Rundown of the insert statement:

* `INSERT INTO users`: First, we specify the `INSERT INTO` keywords which tells MySQL that we want to insert data into the `users` table.
* `users (username, email, active)`: Then, we specify the table name `users` and the columns that we want to insert data into.
* `VALUES`: Then, we specify the values that we want to insert in.

## Inserting multiple records

We've briefly covered this in one of the previous chapters, but in some cases, you might want to add multiple records in a specific table.

Let's say that we wanted to create 5 new users, rather than running 5 different queries like this:

```
INSERT INTO users(username, email, active) VALUES('user1', 'user1@devdojo.com', true);
INSERT INTO users(username, email, active) VALUES('user1', 'user2@devdojo.com', true);
INSERT INTO users(username, email, active) VALUES('user1', 'user3@devdojo.com', true);
INSERT INTO users(username, email, active) VALUES('user1', 'user4@devdojo.com', true);
INSERT INTO users(username, email, active) VALUES('user1', 'user5@devdojo.com', true);
```

What you could do is to combine this into one `INSERT` statement by providing a list of the values that you want to insert as follows:

```
INSERT INTO users
  ( username, email, active )
VALUES
  ('user1', 'user1@devdojo.com', true),
  ('user2', 'user2@devdojo.com', true),
  ('user3', 'user3@devdojo.com', true),
  ('user4', 'user4@devdojo.com', true),
  ('user5', 'user5@devdojo.com', true);
```

That way, you will add 5 new entries in your `users` table with a single `INSERT` statement. This is going to be much more efficient.

## Inserting multiple records using another table

In the previous section, we have discussed how we can insert multiple records using a single INSERT query.
But sometimes there are cases where we need to insert multiple records which are residing in some other table.

In this section, we are going to learn how we can insert multiple records at once using a single INSERT query. 

Consider a table, say `prospect_users`, which stores the information of the people who want to become the users of our service, but they are not yet actual users.

In order to add them to our user database, we have to insert there entries into our `users` table.
We can achieve the same by writing an `INSERT` query with multiple `VALUES` listed in them (as discussed in previous section).

But there is an easier way where we achieve the same by querying the `prospect_users` table.


```
INSERT INTO users ( username, email, active )
SELECT username, email, active FROM prospect_users WHERE active = true;
```

Using the above statement, an entry for each active prospect users will be made in our `users` table.