Filters
=======

Filters allow you to customize rules for data recording. While you can completely disable events in ``prism.conf``, filters allow finer control. Filters tell prism to allow or ignore events that match specific criteria - worlds, actions, materials, players, and more.

For example, many servers have harvest-only "resource" worlds which could generate millions of useless activity logs. No one really cares who mined dirt and stone in a resource world, which is where filters come in.

Filters help you avoid recording data that you don't want. Reducing what gets saved to your database will improve performance and disk usage.

.. _writing:

Writing Filters
---------------

Prism does not generate any filters by default. In ``prism.conf``, look for the ``filters=[]`` config.

Every filter must have:

* A defined **behavior**
* At least one **condition**

The behavior determines if the filter will **ignore** or **allow** recording if the conditions are met.

.. code-block::

	filters=[
	    {
			behavior: IGNORE
	    }
	]

The ``behavior`` property must be set to one of these choices:

* **ALLOW** - Only actions matching all defined conditions will be recorded.
* **IGNORE** - Any actions matching all defined conditions will not be recorded.

Next, you need at least one **condition**.

Currently available conditions are:

* ``actions`` - A list of actions (see :doc:`actions`)
* ``block-tags`` - A list of block tags (see `Tags <https://minecraft.wiki/w/Tag>`_)
* ``item-tags`` - A list of item tags (see `Tags <https://minecraft.wiki/w/Tag>`_)
* ``materials`` - A list of block or item `Material <https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html>`_
* ``worlds`` - A list of world names

All defined condition properties must be met for a filter to apply - except variations like block-tags, item-tags, and materials - they're just different ways of definings materials.

A condition is considered a match if at least one value matches the activity.

To achieve our example of ignoring common blocks in a resource world, we could use this:

.. code-block::

	filters=[
	    {
	        behavior=IGNORE
			block-tags=[
				"minecraft:dirt",
				"minecraft:base_stone_overworld",
				"minecraft:sand"
			]
	        materials=[
	            gravel
	        ]
	        worlds=[
	            resource
	        ]
	    }
	]

This would match all activities that:

* Involve blocks included in those Minecraft tags
* Occur in the world named "resource". 

Because it's set to ignore, this will prevent prism from recording these events. 

Or you can reverse your approach and whitelist the blocks you want to record using ``ALLOW``:

.. code-block::

	filters=[
	    {
	        behavior=ALLOW
	        block-tag=[
	            prism:all_ores
	        ]
	        worlds=[
	            resource
	        ]
	    }
	]

.. note::

   The ``prism:all_ores`` tag is a custom tag included in our datapack, which must be installed. You can use any default or custom tag.

.. _logic:

Filter Logic
------------

It's important to understand how filters are applied.

**Filters are applied in the exact order they're defined in the config.**

The first filter defined in ``prism.conf`` will be the first filter an activity is checked against.

**The first matching filter will be the decider for recording an activity.**

If all filter conditions match, the filter will allow/ignore the activity and additional filters will **not** be checked.

**Missing conditions will automatically match.**

For example, if you don't define a list of ``worlds`` or leave it empty, the filter will match **any** world. In the examples above, I don't filter by any cause so every single cause will be considered a "match".
