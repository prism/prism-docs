Parameters
==========

.. contents::

Parameters
----------

Parameters are optional ways to filter query results. They're the same for lookups, rollbacks, restores, and purges.

They are always entered after the command you're using. For example ``/pr lookup a:break p:viveleroi``.

A query with no parameters will return everything.

Parameters act as an "AND" condition, but parameters that support multiple entries act as an "OR". You may need to run multiple commands if your parameters might conflict. For example ``p:viveleroi m:stone e:cow`` will return "No Results" because there's no way all three values can exist in a single record. If you truly need to be this exact, split it up into ``p:viveleroi m:stone`` and ``p:viveleroi e:cow``.

However, a single parameter that accepts multiple entries will work as expected. ``p:kermit,fozzy m:stone`` will find records in which kermit **or** fozzy acted upon stone.

.. _actions:

Actions Parameter
-----------------

Use the ``a:`` parameter to list one or more actions.

* ``a:[action keys]``
* ``a:[action families]``

Supports multiple (comma seperated)!

"Actions" are standardized names for "events" prism listens to. For example, ``block-break`` and ``item-drop``.

The "action key" is a unique identifier for each action type, like ``block-break``.

The "action family" is the word following the hyphen in the action key. So, ``break`` for ``block-break``. Sometimes, actions are similar and you may want to query multiple without listing them individually. Example: ``hanging-break`` and ``block-break`` are both in the ``break`` family.

To lookup all "break" actions, use: ``/pr l a:break`` (includes **any** actions that match ``*-break``)

To lookup multiple specific actions, use ``/pr l a:block-break,block-place`` (includes **only** results for these two actions)

.. _at:

At Parameter
----------------

Use the ``at:[x],[y],[z]`` parameter to confine or center the search on a single coordinate. Similar to wand usage.

For example, ``at:0,0,0`` would search exclusively for activities affecting that block. 

If defined, this location will be used as the center for the :ref:`radius`, :ref:`in`, and :ref:`world` parameters (instead of your player's location).

This can make it easy to search for a radius around a location you're not currently at or from the console.

.. _before:

Before Parameter
----------------

Use the ``before:[time code]`` parameter to confine the search to activities that occured before the given time.

For example, ``before:3d`` would include records logged before three days ago. More recent records would be excluded. 

For help with time codes, see :ref:`timecodes`.

Also see :ref:`since`.

Block Tags Parameter
--------------------

Use the ``btag:[blocks tag]`` parameter to more efficiently search for materials included in the tag.

Tags are a Minecraft concept for organizing blocks, items, and entities into groups. There are quite a lot already defined in Minecraft but you can also create your own via datapacks.

For example, ``btag:minecraft:dirt`` would search for any dirt-like materials including ``dirt``, ``coarse_dirt``, and ``podzol``. `See the full list <https://minecraft.wiki/w/Block_tag_(Java_Edition)#dirt>`_.

You can even supply multiple tags, like ``btag:minecraft:corals,minecraft:coral_blocks,minecraft:coral_plants``.

Defining your own tags would be an extremely powerful way to group materials. 

Read more about `Tags <https://minecraft.wiki/w/Tag>`_.

.. _bounds:

Bounds Parameter
----------------

Use the ``bounds:[minX],[minY],[minZ]-[maxX],[maxY],[maxZ]`` parameter to search within a rectangular region, defined by a "min" and "max" coordinate (a.k.a. the corners of a box).

For example, ``bounds:0,0,0-10,10,10`` would search exclusively for activities within a rectangle starting at ``0,0,0`` and ending at ``10,10,10``.

.. _cause:

Cause Parameter
-------------------

Use the ``cause:`` parameter to search for activities with a specific non-player cause.

- ``cause:[causename]``

"Causes" are names of any non-player "actor" that initiated an activity.

For example when axolotls kill glow squid, the ``entity`` is ``glow_squid`` and the ``cause`` is ``axolotl``.

A search for ``cause:axolotl`` will return mobs killed by an axolotl.

A search for ``cause:lava`` will return a lot of bat deaths.

"Cause Names" will usually be block or entity names, or "environment", but may include other things.

Players are a special kind of cause. To search for player-caused activities see :ref:`player`.

.. _entity:

Entity Parameter
----------------

Use the ``e:`` parameter to list one or more entity types.

- ``e:[entitytype]``

Supports multiple (comma seperated)!

"EntityType" is a term the Bukkit API uses to define mobs that exist in vanilla Minecraft.

``e:cow`` will query activities that acted upon cows.

.. _in:

In Parameter
-------------

Use the ``in:(chunk|world)`` parameter to confine the search to a pre-defined boundary.

- ``chunk`` uses your current chunk. It sets the lower and upper bound coordinates to that of the chunk you stand in.
- ``world`` uses your current world, without coordinate criteria. 

This parameter automatically limits the search to your current world.

.. _materials:

Materials Parameter
-------------------

Use the ``m:`` parameter to list one or more materials.

- ``m:[material]``

Supports multiple (comma seperated)!

"Materials" is a term the Bukkit API uses to define blocks and items that exist in vanilla Minecraft.

``m:stone`` will query activities that acted upon "stone" blocks. Currently matches are exact so you'll need to list every stone variant if you intend to include them.

.. _player:

Player Parameter
----------------

Use the ``p:`` parameter to list one or more players.

- ``p:[playername]``

Supports multiple (comma seperated)!

Searches for activities caused by a player.

``p:viveleroi`` will query activities in which ``viveleroi`` was the cause.

.. _radius:

Radius Parameter
----------------

Use the ``r:[number]`` parameter to confine the search to a radius around you.

If you're standing at (x/y/z) 0,0,0 and use ``r:5``, the search will find records with coordinates between -5,-5,-5 and 5,5,5.

This parameter automatically limits the search to your current world.

.. _reversed:

Reversed Parameter
------------------

Use the ``reversed:(true|false)`` parameter to include/exclude activities which have been reversed.

``reversed:true`` means a record has been rolled back by a user or plugin using Prism's API. ``reversed:false`` means the end result remains in-world or has been restored by a user or plugin using Prism's API.

.. _since:

Since Parameter
---------------

Use the ``since:[time code]`` parameter to confine the search to activities that occured after the given time.

For example, ``since:1h`` would include records logged after one hour ago. Older records would be excluded.

For help with time codes, see :ref:`timecodes`.

Also see :ref:`before`.

.. _world:

World Parameter
---------------

Use the ``world:[worldname]`` parameter to confine the search to the given world.

For example, ``world:resource`` would include records logged in the world named "resource".

For you current world, ``in:world`` works exactly the same.

.. _timecodes:

Timecodes
---------

Prism uses a user-friendly short-hand to define a point in time. Timecodes can be used individually or combined.

The available time codes are always in the format ``[number][unit]``:

- ``s`` = second
- ``m`` = minute
- ``h`` = hour
- ``d`` = day
- ``w`` = week

Example timecodes:

- ``3w`` = 3 weeks
- ``1h30m`` = 1 hour, 30 minutes (``90m`` also works)
- ``1d12h`` = 1 day, 12 hours

These can be used in any parameter which supports timecodes.