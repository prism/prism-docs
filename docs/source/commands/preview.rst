Preview Command
===============

Preview commands will allow you to view block changes without actually changing the world on the server.

It works by telling your game client the blocks changed, just not the server. 

.. note::

    Because of how Minecraft works, previews will **only** include block changes. Entities and items cannot be "faked".

.. _prb:

``/pr preview-rollback`` (alias: ``prb``)

The preview rollback command will preview any reversible changes based on your search parameters.

To understand the parameters available and their use, please see :doc:`parameters`.

.. _prs:

Preview support for restores is unfinished.

.. _pra:

``/pr preview-apply``

Applying a preview will perform the actual rollback/restore, altering the server world.

.. _prc:

``/pr preview-cancel``

Canceling a preview will send the "live" block data to your client and discard the queued modifications.
