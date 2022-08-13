Actions
=======

"Actions" are specific in-game events that Prism monitors, like ``block-break`` or ``item-drop``. They are always two lower-case words with a hyphen.

"Action Families" are related actions. They're related in that they share the second word, like ``block-break`` and ``hanging-break``. They're both "break" events.

Prism records most actions by default but they can be disabled in the config.

.. note::

    Many actions that were separate in v3 are now combined, making this list appear shorter than it is. For example, any mob/liquid break is just ``block-break`` with appropriate causes.

The following is a list of all actions Prism v4 can monitor.

- `Default` indicates whether Prism monitors this action by default. Some are disabled for performance or spam reasons.
- `Reversible` indicates whether the action can be reversed (see :doc:`modifications`)

+-----------------+----------------------------------+----------+-------------+
| Action          | Monitors                         | Default? | Reversible? |
+=================+==================================+==========+=============+
| bed-enter       | villager/player entering bed     | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| block-break     | blocks broken                    | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| block-fade      | blocks fading (snow melt, etc)   | No       | Yes         |
+-----------------+----------------------------------+----------+-------------+
| block-form      | blocks forming (snow, obsidian)  | No       | Yes         |
+-----------------+----------------------------------+----------+-------------+
| block-harvest   | harvest crop w/out break         | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| block-ignite    | blocks set on fire               | Yes      | No*         |
+-----------------+----------------------------------+----------+-------------+
| block-place     | blocks placed                    | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| block-shift     | blocks moved by pistons          | No       | Yes         |
+-----------------+----------------------------------+----------+-------------+
| block-spread    | blocks spreading/growing         | No       | Yes         |
+-----------------+----------------------------------+----------+-------------+
| block-use       | player uses a block              | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| bonemeal-use    | player uses bonemeal             | Yes      | No*         |
+-----------------+----------------------------------+----------+-------------+
| bucket-empty    | player empties bucket contents   | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| bucket-fill     | player fills bucket              | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| entity-dye      | player dyes entity (aka sheep)   | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| entity-eat      | entity eats (aka sheep)          | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| entity-leash    | player leashes an entity         | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| entity-kill     | mobs killed                      | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| entity-shear    | entity is sheared                | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| entity-unleash  | entity is unleashed              | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| fluid-flow      | water/lava flows (not breaks)    | No       | Yes         |
+-----------------+----------------------------------+----------+-------------+
| hanging-break   | frames/paintings broken          | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| hanging-place   | frames/paintings placed          | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| inventory-open  | player accesses an inventory     | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| item-dispense   | items dispensed by dispenser     | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| item-drop       | items dropped by player          | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| item-insert     | items inserted into an inventory | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| item-pickup     | mob/player picking up items      | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| item-remove     | items removed from an inventory  | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| item-throw      | mob/player throwing items        | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| player-join     | player connecting to server      | No       | No          |
+-----------------+----------------------------------+----------+-------------+
| player-quit     | player disconnecting from server | No       | No          |
+-----------------+----------------------------------+----------+-------------+
| player-teleport | player teleporting               | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| vehicle-enter   | mob/player enters boat/minecart  | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| vehicle-exit    | mob/player exits boat/minecart   | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| vehicle-place   | player/block places boat/minecart| Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| xp-pickup       | player gains XP                  | No       | No          |
+-----------------+----------------------------------+----------+-------------+

Asterisk (*) means action is not reversible but may produce other events which are.

Paper-Only
----------

Some actions are only available, or have improved coverage on Paper-based servers.

- ``block-ignite`` - Improved detection for the ignition source of TNT.


Natural Spam
------------

Several events are disabled by default because they `mostly` log natural events that you won't care about. These are especially spammy after fresh chunk gen as water starts flowing and blocks adjust to their environment.

- ``block-fade`` - Snow melt, grass/nylium blocks fading into dirt/netherrack, etc.
- ``block-form`` - Snow fall, obsidian formation, etc.
- ``block-spread`` - Vine, amethyst, mushroom, and other growth. Grass, mycelium, and mushrooms, spreading.
- ``fluid-flow`` - Tracks the flow of fluids. Strongly recommend a drain tool. Still tracks flow breaking blocks.

If you plan to enable any of these, we *strongly* recommend you use a filter or increase their purge rate.

Here are some example filters you might start with and tailor to suit your needs:

.. code-block:: hocon

    // Ignore block-fade for nylium into netherrack in the nether
    {
        actions=[
            block-spread
        ]
        behavior=IGNORE
        materials=[
            cave_vines,
            twisting_vines,
            vine,
            grass_block,
            mycelium
        ]
        worlds=[]
    }

    // Ignore spread actions for all vines, grass, and mycelium
    {
        actions=[
            block-spread
        ]
        behavior=ALLOW
        materials=[
            large_amethyst_bud,
            medium_amethyst_bud,
            small_amethyst_bud
        ]
        worlds=[]
    }
