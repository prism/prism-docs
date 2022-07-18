API Usage (Bukkit)
==================

In your main plugin class' ``onEnable`` method, look for and hook Prism.

.. note::

    Add "Prism" to your plugin.yml's ``depend`` array.

.. code-block:: java

    @Override
    public void onEnable() {
        Plugin plugin = Bukkit.getPluginManager().getPlugin("Prism");
        if (plugin != null & plugin.isEnabled() && plugin instanceof IPrism prismApi) {
            // act on prismApi here
        }
    }
