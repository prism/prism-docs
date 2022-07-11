Databases
=========

.. contents::

Prism, like all logging plugins, goes **heavy on database**. 

Prism's database schema and connection pools are configured for the best performance we can provide but because there are a wide variety of database servers and a wide variety of use cases for prism, you may need to adjust things.

.. _db101:

DB 101
------

You need a database to use Prism.

A database is a place prism can store and easily search and retreive all of the data it needs.

You'll either get one from your server hosting company (they'll give you the connection address and credentials) or you'll install a database server yourself.

Shared hosting companies typically provide MySQL databases. 

We understand that many users will have a database from a shared hosting company but there are several downsides to this:

Shared servers...

- Split resources among potentially thousands of customers. This significantly reduces performance.
- May be in another country, increasing network latency (how long it takes your server to talk to the db).
- Lock configuration settings for what most users need. You can't fine-tune the db to your needs.

.. _goodhabits:

Good Habits
-----------

(aka, What You Can Do)

The more data you log and the longer you keep it, the more disk space the db needs. The larger a db gets, the longer your queries will take to find data.

We've tried our best to create a schema that uses only as much disk space as needed, and indexes the data properly. However, it may be worth your time to customize indexes for your search habits because there's never an index that fits everyone's usage.

Here are some good habits to avoid unnecessary data:

- Review your actions config and disable any that you don't want logged.
- Review your filters config and filter out junk you don't care about.
- Review your purge rules to discard data.
- Keep an eye on your database size and adjust the above to keep a good balance.

.. _prism:

What Prism Does
---------------

Out of the box, Prism does a lot to improve performance.

**Connection Pooling**

Prism uses a connection pool. (For SQL servers, Hikari). This reduces overhead needed to communicate with the database server by reusing connections. Reduce, reuse, recycle!

**Statement Batching**

Activities are recorded in batches. By recording several at a time we can reduce how often we're communicating with the database server. This is especially useful when the database server is on another machine.

You can adjust the batch size as needed - lower sizes send batches more often but in smaller chunks. Larger sizes less often and in larger chunks.

**Hikari Optimizations**

Prism uses the recommended Hikari optimizations for MySQL servers. This includes settings like increased statement caching, etc.

**Procedures**

Procedures move complex db queries/logic to the database server which reduces connection use and how much data is sent over the network. For example, Prism uses procedures to create the activity record and relational data. This becomes a single procedure call versus multiple sql statements.

.. note::

    This feature is limited to users who have db server permissions to create procedures. Usually that means only those running their own db server.

