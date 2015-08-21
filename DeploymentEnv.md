## Configuration change management (bots>=3.0) ##
Having different environments for at least test and production is a sound IT practice.<br>
But having different environments also brings problems:<br>
<ul><li>push changes in a controlled way to production-environment<br>
</li><li>are changes done right, and does the existing configuration still run right?<br>
</li><li>keep test-environment in line with production-environment<br>
To handle these problems bots has some features called <i>configuration change management</i>.</li></ul>

<br>
<h2>Bots configuration change management</h2>
Configuration change management in bots has 2 aspects:<br>
<ol><li>Use <a href='UsefulTools#Compare_and_merge.md'>tools</a> for:<br>
<ul><li>Comparing differences in configuration of environments<br>
</li><li>Pushing the changes from test->production environment in a controlled, automated way<br>
</li></ul></li><li>Use of <a href='DeploymentAcceptance.md'>isolated acceptance test</a> to:<br>
<ul><li>check if acceptance test runs OK in test<br>
</li><li>check if acceptance test runs OK in production<br>
</li><li>make the test-environment (very) equal to production-environment</li></ul></li></ol>

Configuration change management works best if both aspects are combined!<br>
<br>
<br>
See <a href='DeploymentAutopush.md'>receipe</a> for this!