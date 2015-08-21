## What is a plugin? ##
  * A plugin is a file with predefined configuration for bots. It includes routes, channels, grammars, mappings etc.
  * Plugins are installed via _bots-monitor-Systasks->Read plugin_.
  * In order to run the routes in a plugin you first have to activate the routes.
  * There are useful plugins on [the bots sourceforge site](http://sourceforge.net/projects/bots/files/plugins/).
  * [Documentation](PluginList.md) for these plugins.


Note: grammars for edifact and x12 are NOT plugins, and can not be installed.

<br>
<h2>For what is a bots plugin useful?</h2>
<ul><li>An easy way to distribute and share edi configurations for bots.<br>
</li><li>Learn from existing configurations<br>
</li><li>backup your configuration.<br>
</li><li>share your configuration with others (It would be nice if you want to share your configuration; other can use and/or learn from what you have done!).<br>
</li><li>do another install of the same configuration.<br>
</li><li>transfer your environment from test to production.<br>
</li><li>Plugins are used to update to a new version of bots (only between minor versions).</li></ul>

<br>
Note that all bots 3.0.0 plugins are suited to use in <a href='http://code.google.com/p/bots/wiki/DeploymentAcceptance'>acceptance test mode</a>.