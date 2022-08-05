Actions
=======

"Actions" are specific in-game events that Prism monitors, like ``block-break`` or ``item-drop``. They are always two lower-case words with a hyphen.

"Action Families" are related actions. They're related in that they share the second word, like ``block-break`` and ``hanging-break``. They're both "break" events.

Prism records most actions by default but they can be disabled in the config.

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
| block-ignite    | blocks set on fire               | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| block-place     | blocks placed                    | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| block-spread    | blocks spreading/growing         | No       | Yes         |
+-----------------+----------------------------------+----------+-------------+
| entity-kill     | mobs killed                      | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| hanging-break   | frames/paintings broken          | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| item-drop       | items dropped by player          | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| item-pickup     | mob/player picking up items      | Yes      | No          |
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

Natural Spam
------------

Several events are disabled by default because they `mostly` log natural events that you won't care about. These are especially spammy after fresh chunk gen as water starts flowing and blocks adjust to their environment.

- ``block-fade`` - Snow melt, grass/nylium blocks fading into dirt/netherrack, etc.
- ``block-form`` - Snow fall, obsidian formation, etc.
- ``block-spread`` - Vine, amethyst, mushroom, and other growth. Grass, mycelium, and mushrooms, spreading.

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
