Modifications
=============

Prism can modify the world in a variety of ways. It's important to understand these and how prism can affect your world.

.. note::

    Modifications are inherently dangerous and should be used by server staff. We highly recommend practicing on a test server or using preview modes when possible. One mis-used command could rollback days worth of changes, memory crashes, or other unwanted results.

.. _rollbacks:

Rollbacks
---------

A rollback, the most commonly used modification, is a **reversal** of activities. Reversing an action usually just means doing the opposite of the final result.

For example, say `player viveleroi broke a diamond block at x/y/z 1,2,3`. A rollback would `place a diamond block at x/y/z 1,2,3`.

"Rolling-back" a `place` event will result in the block being removed. Rolling-back a `break` event will result in the block being placed. 

Because of how complex Minecraft is, there's no reasonable/reliable way to also take that exact diamond block back from the player. Punishing the player and auditing their stolen items will be up to you and your staff.

.. _restores:

Restores
--------

A restore is a modification that will "repeat" the original activity.

For example, say `player viveleroi broke a diamond block at x/y/z 1,2,3`. A restore would again `break a diamond block at x/y/z 1,2,3`.

These modifications are less useful generally, they're typically used to re-apply changes that were somehow lost.