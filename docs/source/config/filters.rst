Filters
=======

Filters allow you to customize rules for data recording. While you can completely disable events in ``prism.conf``, filters allow finer control. Filters tell prism to allow or ignore events that match specific criteria - worlds, actions, materials, players, and more.

For example, many servers have harvest-only "resource" worlds which could generate millions of useless activity logs. No one really cares who mined dirt and stone in a resource world, which is where filters come in.

Filters help you avoid recording data that you don't want. Reducing what gets saved to your database will improve performance and disk usage.

.. _writing:

Writing Filters
---------------

Prism does not generate any filters by default. In ``prism.conf``, look for the ``filters=[]`` config.

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

Currently available conditions are:

* ``worlds`` - A list of world names
* ``materials`` - A list of block or item `Material <https://hub.spigotmc.org/javadocs/bukkit/org/bukkit/Material.html>`_
* ``actions`` - A list of actions (see :doc:`actions`)

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

This would match all actions that involve dirt, grass_block, etc, only in the world "resource". Because it's set to ignore, this will prevent prism from recording these events. 

The list of blocks to ignore might get very long in this scenario. Instead, we could write this to specifically allow blocks:

.. code-block::

	filters=[
	    {
	        behavior=ALLOW
	        materials=[
	            diamond_ore,
	            deepslate_diamond_ore
	        ]
	        worlds=[
	            resource
	        ]
	    }
	]


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


.. _conflicting:

Conflicting Filters
-------------------

Be careful to avoid writing conflicting filters. Prism currently has limited validation and relies on the above logic when deciding what to apply. Nothing should explode but you're going to confuse yourself as to why filters aren't working.

For example if you write a filter that **ignores** dirt breaks server-side, and a filter that **allows** dirt breaks in a world named "towny", per the logic described above, only the first filter will apply.

To fix this scenario, the first filter can be removed entirely. A filter that allows dirt breaks in a specific world will automatically ignore dirt breaks in other worlds.