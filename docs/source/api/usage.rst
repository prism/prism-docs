API Usage (Bukkit)
==================

In your main plugin class' ``onEnable`` method, look for and hook Prism.

.. note::

    Add "Prism" to your plugin.yml's ``depend`` array.

.. code-block:: java

    @Override
    public void onEnable() {
        // Get the plugin instance from bukkit
        Plugin plugin = Bukkit.getPluginManager().getPlugin("Prism");

        // If plugin found and enabled, get the api instance
        if (plugin != null && plugin.isEnabled() && plugin instanceof IPrism prismApi) {
            // Build a new activity query. We'll look for placed blocks at a specific coordinate
            final ActivityQuery query = ActivityQuery.builder()
                .actionTypeKey("block-place")
                .location(worldUuid, worldName, x, y, z)
                .build();

            // Storage query calls should always be async so they don't block the main game thread
            Bukkit.getScheduler().runTaskAsynchronously(this, () -> {
                try {
                    // Ask the storage adapter to actually execute our query and return any results
                    List<IActivity> results = prismApi.storageAdapter().queryActivities(query);
                    // do what you wish with results
                } catch (Exception e) {
                    // handle storage exception
                }
            });
        }
    }
