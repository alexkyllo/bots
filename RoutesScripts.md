## Route scripting ##

When the standard routing of bots does not fit your needs, use routescripts.<br>
Routescripts are python programs.<br>


There are 2 types of routescripts:<br>
<ol><li>User exits: at certain points in a route, bots calls your user exit. See <a href='RouteScriptsOverviewExits.md'>overview of exit points</a>. Most common usage is 'pre-processing' an edi file, see <a href='RouteScriptsExample.md'>recipes</a>.<br>
</li><li>Your script takes over the whole route. This is done by using function <i>main()</i> in your routescript. See <a href='RouteScriptsExampleWholeRoute.md'>Example</a>.</li></ol>

<br>

<b>How to set up a route-script:</b>
<ol><li>use bots-monitor to add a new route.<br>
</li><li>make a routescript with the same name as the routeID in <i>bots/usersys/routescripts/<code>&lt;routeid&gt;</code>.py</i>