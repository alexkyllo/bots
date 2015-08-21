# Deployment #

This part of the wiki is about using bots in production.<br>

There are extra points to consider when deploying bots in a 24x7 production environment:<br>

<ol><li>Consider the best way of <a href='DeploymentEngineOverview.md'>running bots-engine</a>.<br>
</li><li>When errors in edi-files occur, <a href='DeploymentErrorReports.md'>receive a notification by email</a>.<br>
</li><li><a href='DeploymentMultipleEnvironments.md'>Use multiple environments</a>; having different environments for at least test and production is standard IT practice.<br>
</li><li>Consider if edi files need <a href='Archiving.md'>extra archiving</a>
</li><li>Out of the box bots does not run as a <a href='DaemonProcesses.md'>service/daemon</a>. In a production enviroment this is what you'll probably want.