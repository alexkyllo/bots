# Confirmations/acknowledgements #

## Introduction ##
In edi often a confirmation (or acknowledgement) is needed.<br>
Bots has a build-in confirmation framework that supports:<br>
<ul><li>997 (x12)<br>
</li><li>CONTRL (edifact)<br>
</li><li>MDN (email)<br>
Next to that Bots supports APERAK (edifact), see details below.<br>
<br>
<br>
<br>
Note that confirmations have 3 aspects:<br>
</li><li>Bots sends a confirmation for an incoming edi-file.<br>
</li><li>Bots asks a confirmation for an outgoing edi-file.<br>
</li><li>Bots processes an incoming confirmation.<br>
<br>
You can view the results of asked or send confirmations in <i>bots-monitor->All runs->Confirmations</i>.<br>
<br>
All send or asked confirmations are registered in bots if configured correct.<br>
<br>
<br>
<h2>Examples in plugins</h2>
</li><li>plugin <i>x12-850-856-810-997</i>
<ul><li>generates a 997 for incoming orders, and dispatches this via a composite route.<br>
</li><li>inbound route is configured to process 997's.<br>
</li></ul></li><li>plugin <i>demo_mdn_confirmations</i> sends and receives email-confirmations (MDN)<br>
</li><li>plugin <i>edifact_ordersdesadvinvoic</i> sends APERAK for incoming orders - if indicated in incoming order.</li></ul>

<br>
<h2>Send confirmation</h2>
<ol><li>first configure correct processing of incoming edi-files.<br>
</li><li>configure confirmrules in <i>bots-monitor->Configuration->Confirmrules</i>. You can use several confirmation rules, bots looks at all rules. Per rule:<br>
<ul><li>indicate the kind of confirmation to send (997, CONTRL, etc).<br>
</li><li>indicate how the rules works - per route, channel, messagetype, etc. (prior to bots 3.0, frompartner and topartner where swapped :-(<br>
</li><li>an option is to include first and than exclude using 'negativerule'. Bots first checks the positive rules, than the negative rules. Eg: send 997 for all incoming x12-files in a route, and exclude partner XXX.<br>
</li></ul></li><li>use a <a href='RoutesComposite.md'>composite route</a> to send the confirmations to the right destination.</li></ol>

<br>
<h2>Ask confirmation</h2>
<ol><li>first configure correct processing of outgoing edi-files.<br>
</li><li>than configure <i>bots-monitor->Configuration->Confirmrules</i> You can configure several confirmation rules, bots looks at all rules. Per rule:<br>
<ul><li>indicate the kind of confirmation to ask (997, CONTRL, etc).<br>
</li><li>indicate how the rules works - per route, channel, messagetype, etc. (prior to bots 3.0, frompartner and topartner where swapped :-(<br>
</li><li>an option is to include first and than exclude using 'negativerule'. Bots first checks the positive rules, than the negative rules. Eg: ask 997 for all outgoing x12-files in a route, and exclude partner XXX.<br>
</li></ul></li><li>you will need to process the incoming confirmation.</li></ol>

<br>
<h2>Process incoming confirmation</h2>
<ul><li>997 (x12): an additional translation and mapping script is needed.<br>
</li><li>CONTRL (edifact): an additional translation and mapping script is needed.<br>
</li><li>MDN-confirmations: no additional comfiguration is needed.</li></ul>

<br>
<h2>Send 997/acknowledgement for incoming x12 orders</h2>
Before attempting to configure confirmations create and test a route<br>
for a typical X12 message e.g. 850. Once that is working correctly, confirmations can be configured for the route.  Bots will now generate a 997 message for each 850 recipient. Notice that the 997 is in the same Route as the 850.  Probably you will want the 997 to go back out to the partner that sent the 850. Use a <a href='RoutesComposite.md'>composite route</a> for this.<br>
<br>
Tell bots to send confirmations (997 message) in <i>bots-monitor->Configuration->Confirmrules</i>. Note that in the route established for the 850, there is a sequence number next to the routeID. The 'seq' for the 850 is probably "1". A new route-part must now be created to handle the 997 that bots has generated. The new route-part has the same routeID but a higher 'seq' number (e.g. "2"). Now configure to route the 997 message that bots will generate. The 997 is an internally generated file.  The user will have very little to do with its creation but everything to do with where the file goes (i.e. its route).<br>
<br>
Route with seq 2 will have <code>&lt;none&gt;</code> as its incoming channel, and does not translate. Its outgoing channel will most likely be to FTP or a VAN. <b>The key to success</b> is in using the "Filtering for outchannel" at the bottom of the "Change Route" page. In "Filtering for outchannel" for 'seq' 1, set toeditype and tomessagetype so that only the translated 850 file will take this part of the Composite Route. Now for seq 2 set toeditype to X12.  This will cause only the X12 997 message to follow this part of the composite route.