Out of the box bots does nothing. You have to configure bots for your specific edi requirements.<br>
Check out different ways to <a href='ConfigurationHow.md'>start your own configuration</a>.<br>
See <a href='Debug.md'>debug overview</a> for info how to debug while making a configuration.<br>
Bots also has nice features for <a href='DeploymentEnv.md'>configuration change management</a> (build test sets for you configuration, easier pushing of changes from test to production).<br>
<br>
<br>
<h3>Configuration explained in short</h3>
<ul><li>'routes' are edi-workflows.<br>
</li><li>'channels' do the communication (from file system, ftp, etc).<br>
</li><li>each route hs an 'inchannel' and an  'outchannel'<br>
</li><li>Translations rules determine: translate what to what.</li></ul>

<br>
<h3>Most asked configuration topics</h3>
<ul><li><a href='RoutesComposite.md'>composite routes</a>
</li><li><a href='RoutesPass.md'>passthrough route</a> (without translation)<br>
</li><li><a href='Filenames.md'>options for outgoing filenames</a>
</li><li><a href='ChannelsDatabase.md'>direct database communication</a>
</li><li><a href='TranslationperPartner.md'>partner specific translations</a>
</li><li><a href='MappingCcode.md'>code conversion</a>
</li><li>view <a href='ConfigurationBotskey.md'>business documents</a> instead of edi-files.<br>
</li><li><a href='Confirmations.md'>confirmations/acknowledgements</a>
</li><li><a href='ConfigurationMerge.md'>merging and enveloping outgoing edi files</a>
</li><li><a href='GrammarsPartnerSyntax.md'>partner specific syntax</a> (especially for x12 and edifact)