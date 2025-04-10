Databases
=========

.. contents::

Prism, like all logging plugins, goes **heavy on database**. 

Prism's database schema and connection pools are configured for the best performance we can provide but because there are a wide variety of use cases, you may need to adjust things.

.. _db101:

DB 101
------

You need a database to use Prism.

A database is a place prism can store and easily search and retreive all of the data it needs.

You'll either get one from your server hosting company (they'll give you the connection address and credentials) or you'll install a database server yourself.

We understand that many users will have a database from a shared hosting company but there are several downsides to this:

Shared servers...

- Split resources among potentially thousands of customers. This significantly reduces performance.
- May be in another country, increasing network latency (how long it takes your server to talk to the db).
- Lock configuration settings for what most users need. You can't fine-tune the db to your needs.
- Limit privileges so you can't utilize stored procedures.

.. _goodhabits:

What You Can Do
---------------

The more data you log and the longer you keep it, the more disk space the db needs. The larger a db gets, the longer your queries will take to find data.

Here are some good habits to avoid unnecessary data:

- Review your actions config and disable any that you don't want logged.
- Review your filters config and filter out junk you don't care about.
- Review your purge rules to discard data.
- Keep an eye on your database size and adjust the above to keep a good balance.

We've tried our best to create a good schema. We'll continue to make improvements. You can always make structure or index schema changes to better align with how you use Prism.

.. _prism:

What Prism Does
---------------

Out of the box, Prism does a lot for performance.

**Asynchronous Tasks**

Prism executes queries on another thread, some the game thread is not blocked.

**Connection Pooling**

Prism uses a connection pool (HikariCP). This reduces overhead needed to communicate with the database server by reusing connections. Reduce, reuse, recycle!

**Statement Batching**

Activities are recorded in batches. By recording several at a time we can reduce how often we're communicating with the database server. This is especially useful when the database server is on another machine.

You can adjust the batch size as needed - lower sizes send batches more often but in smaller chunks. Larger sizes less often and in larger chunks.

**Hikari Optimizations**

Prism uses the recommended Hikari optimizations for MySQL/MariaDB servers. This includes settings like increased statement caching, etc.

**Stored Procedures**

Stored procedures/functions can move complex db queries/logic to the database server which reduces network traffic. Things that might take multiple queries from Prism become only a single procedure call.

.. note::

    This feature is limited to users who have database permission to create procedures/functions. That's common on shared hosts, especially in MySQL/MariaDB.

