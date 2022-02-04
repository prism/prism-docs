Parameters
==========

.. _parameters:

.. _actions:

Actions Parameter
-----------------

* ``a:[actions]``
* ``a:[action families]``

Supports multiple: Yes

"Actions" are standardized names for "events" prism listens to. For example, ``block-break`` and ``item-drop``.

Use the ``a:`` parameter to list one or more actions. The query results will only include records for those actions.

The "action family" is the word following the hyphen in the action key. So, ``break`` for ``block-break``. Sometimes, actions are similar and you may want to query multiple without listing them individually. Example: ``hanging-break`` and ``block-break`` are both in the ``break`` family.

To lookup all "break" actions, use: ``/pr l a:break``

To lookup multiple specific actions, use ``/pr l a:block-break,block-place``
