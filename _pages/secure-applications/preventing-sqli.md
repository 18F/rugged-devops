---
permalink: /secure-applications/preventing-sqli/
title: Preventing SQL Injection
---

## WHat is is SQL injection?

*SQL injection* (SQLi) occurs when an attacker is able to modify a database query by "injecting" parameters that aren't escaped and are thus executed by the database. For example, you're vulnerable if you're constructing queries using string interpolation:

```python
query = "SELECT * FROM accounts WHERE username = '%s';" % request.POST['username']
```

If a user sent a `username` like `"joe"`, the query would be:

```sql
SELECT * FROM accounts WHERE username = 'joe'
```

This is safe, but what if the attacker used a username of `' OR 1=1;`? The query would end up being:

```sql
SELECT * FROM accounts WHERE username = '' OR 1=1;
```

... which would disclose the entire contents of your `accounts` table.

If you find [this XKCD comic](https://xkcd.com/327/) funny, then you  understand SQL injection attacks:

![http://xkcd.com/327/](http://imgs.xkcd.com/comics/exploits_of_a_mom.png)

## Preventing SQLi

There are several techniques you can employ to prevent SQL injection attacks. In order of preference, they are:

* Option #1 (preferred): Use a database abstraction layer that protects against SQL injection automatically.
* Option #2 (acceptable): Use parameterized queries
* Option #3 (last resort): Escape all user-supplied input

Read on for details!

### Preventing SQLi using database abstraction layers (preferred)

Most modern database abstraction layers automatically protect against SQL
inject attacks. If you're using a modern web framework, or modern ORM/database abstraction layers, you probably have strong protections out of the box. However, you should double-check your library/framework's documentation to be sure, and to read about any caveats.

Here's a list of our recommended libraries -- ones we know to have good, solid
protections -- along with some pointers to caveats:

* Django's model layer (Python/Django) - with the exception of [methods specifically devoted to executing raw SQL](https://docs.djangoproject.com/es/1.9/topics/security/#sql-injection-protection), all of Django's "queryset"
APIs are SQLi-safe.

* SQLAlchemy (Python) - like Django's model layer, [unless you're explicitly using methods that construct and execute raw SQL](http://docs.sqlalchemy.org/en/rel_1_0/faq/sqlexpressions.html?highlight=security#how-do-i-render-sql-expressions-as-strings-possibly-with-bound-parameters-inlined), all queries using SQLAlchemy are SQLi-safe.

* ActiveRecord (Ruby/Rails) - most ActiveRecord methods are safe; but some are not. See [Rails SQL Injection](http://rails-sqli.org/) for documentation.

We strongly recommend using one of the above libraries -- or something equivalent -- to defend against SQLi. This is the easiest *and* the most effective SQL injection protection technique.

### Preventing SQLi using parameterized queries (acceptable)

Obviously, there are situations where a heavy-weight framework or ORM doesn't fit. In those situations, lower-level SQL libraries can be safely used, as long as you make sure to always use *parameterized queries*. Parameterized queries separate the SQL from the dynamic variables, forcing developers to pass them separately. This lets the database distinguish between code and data, and safely handle anything an attacker might enter.

For example, here's what a parameterized query looks like in Python, using the low-level [Python DB-API](https://www.python.org/dev/peps/pep-0249/):

```python
db.execute("SELECT * FROM accounts WHERE username = ?", username)
```

And in Ruby, using the [Sequel](http://sequel.jeremyevans.net/) library:

```ruby
DB[:accounts].where("username = ?", username)
```

The key here is to **always pass queries and parameters**, and **never use string operations on SQL parameters**.

### Preventing SQLi by escaping (not recommended)

As a last resort, you can escape user-supplied parameters. However, this methodology is very weak compared to the previous two techniques, and isn't recommended. Escaping data is difficult to get correct, hard to use consistently, and quite error-prone.

In fact, SQL escaping is so complicated that it's beyond the scope of this document. If you must protect against SQLi by escaping, you should carefully read your database and database driver's documentation to understand how to correctly escape data. Another good resource is [OWASP's guide to SQL escaping](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet#Defense_Option_3:_Escaping_All_User_Supplied_Input), which covers Oracle, MySQL, SQL Server, and PostgreSQL.

## Further reading

- [Mozilla: Preventing SQL Injection](https://wiki.mozilla.org/WebAppSec/Secure_Coding_Guidelines#Preventing_SQL_Injection)
- [OWASP: SQL Injection Prevention Cheat Sheet](https://www.owasp.org/index.php/SQL_Injection_Prevention_Cheat_Sheet)