Actions
=======

"Actions" are specific in-game events that Prism monitors, like ``block-break`` or ``item-drop``. They are always two lower-case words with a hyphen.

"Action Families" are related actions. They're related in that they share the second word, like ``block-break`` and ``hanging-break``. They're both "break" events.

Prism records most actions by default but they can be disabled in the config.

The following is a list of all actions Prism v4 can monitor.

+-----------------+----------------------------------+----------+-------------+
| Action          | Monitors                         | Default? | Reversible? |
+=================+==================================+==========+=============+
| block-break     | blocks broken                    | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| block-place     | blocks placed                    | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| entity-kill     | mobs killed                      | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| hanging-break   | frames/paintings broken          | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| item-drop       | items dropped by mob/block       | Yes      | Yes         |
+-----------------+----------------------------------+----------+-------------+
| vehicle-enter   | mob/player enters boat/minecart  | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| vehicle-exit    | mob/player exits boat/minecart   | Yes      | No          |
+-----------------+----------------------------------+----------+-------------+
| vehicle-place   | player/block places boat/minecart| Yes      | No          |
+-----------------+----------------------------------+----------+-------------+