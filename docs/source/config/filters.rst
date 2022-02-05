Filters
=======

Filters allow you customize rules for data recording. While you can completely disable events in ``prism.conf``, filters allow much greater control. Filters tell prism to allow or ignore events that match specific criteria - worlds, actions, materials, players, and more.

For example, you can ignore recording specific blocks like dirt and stone in a resource world. Resource worlds are meant to be destroyed and harvests so this cuts down on millions of rows of useless information, yet still allows you to record important information like who mined diamond.

.. _writing:

Writing Filters
---------------

Prism does not generate any filters by default. In ``prism.conf`` look for the ``filters=[]`` config.

Every filter must start with a **behavior**. Behavior determines if the filter will **ignore** or **allow** recording.

.. code-block::

	filters=[
		{
			behavior: IGNORE
		}
	]

The ``behavior`` property must be set to one of these choices:

* **ALLOW** - Only actions matching these conditions will be recorded.
* **IGNORE** - Any actions matching these conditions will not be recorded.

Next, you need at least one **condition**. Conditions are how a filter matches activities.

Available conditions are:

* ``worlds`` - A list of world names
* ``materials`` - A list of block or item `Material <https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html>`_
* ``actions`` - A list of action types

To achieve our example of ignoring common blocks in a resource world, we could use this:

.. code-block::

	filters=[
	    {
	        behavior=IGNORE
	        materials=[
	            dirt,
	            grass_block,
	            stone,
	            diorite,
	            granite,
	            sand,
	            red_sand,
	            gravel
	        ]
	        worlds=[
	            resource
	        ]
	    }
	]

This would match all actions (block-break, item-drop, etc) that involve dirt, grass_block, etc, only in the world "resource". Because it's set to ignore, this will prevent prism from recording these events. 