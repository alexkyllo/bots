## Partner specific translation ##

### Explain by example ###
You receive edifact ORDERSD96AUNEAN008 from several partners.
Partner 'retailer-abroad' fills the orders in a different way; the difference is so big that it is better to have a separate mapping script.<br>
Configure this like:<br>
<ul><li>one grammar for incoming edifact ORDERSD96AUNEAN008 message. (It is a standard message, isn't it?)<br>
</li><li>one grammar for the inhouse import format. (We definitely want one import for all orders!)<br>
</li><li>note that the incoming edifact grammar uses QUERIES to determine the from-partner and to-partner before the translation.<br>
</li><li>make the 2 mapping scripts:<br>
<ul><li>mapping script 'ordersedi2inhouse_for_retailerabroad.py' (specific for partner 'retailer-abroad') .<br>
</li><li>mapping script 'fixed-myinhouseorder' (for all other retailers).<br>
</li></ul></li><li>add 'retailer-abroad' to partners (via <i>bots-monitor->Configuration->Partners & groups</i>).<br>
</li><li>Use 2 translations rules:<br>
<ul><li>edifact-ORDERSD96AUNEAN008 to fixed-myinhouseorder using mapping script ordersedi2inhouse.py<br>
</li><li>edifact-ORDERSD96AUNEAN008 to fixed-myinhouseorder using mapping script ordersedi2inhouse_for_retailerabroad.py for from-partner 'retailer-abroad'</li></ul></li></ul>

Often there are lots of similarities between the mappings - the 'many similar yet different mappings' problems. This can be <a href='http://code.google.com/p/bots/wiki/TranslationperPartnerExtended'>handled in bots</a> in a nice way.<br>
<br>
<br>
<h3>Plugin</h3>
Plugin 'demo_partnerdependent' at <a href='http://sourceforge.net/projects/bots/files/plugins/'>the bots sourceforge site</a> demonstrates partner specific translations.