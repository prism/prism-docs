Messaging
=========

Localization
------------

Prism supports expanding the languages used in-game through a ``Prism/locale/messages/message-(lang).properties``.

Create a new language file by copying an existing one and edit the ``defautLocale`` config in the prism configuration file.

Prism will also try to use the language file that a user's Minecraft client is set to, if it's available.

Formatting
----------

Prism uses `Kyori MiniMessage <https://docs.adventure.kyori.net/minimessage/>`_ for message formatting. This gives you robust control over the look of Prism's in-game messaging.

In addition to control over the language used, you can change the layout and formatting through the language files.