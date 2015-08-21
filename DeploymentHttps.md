# Bots-monitor over HTTPS Introduction #

This feature is introduced in bots 2.1.0.<br>
This works with cherrypy > 3.2.0 in combination with python 2.6 or 2.7. In python 2.5 this works (using extra dependency pyOpenssl) but gives problems with reading plugins.<br>
<br>
Procedure:<br>
<ol><li>you will need an SSL certificate. You can use self-signed certificates.<br>
</li><li>in <i>bots/config/bots.ini</i> uncomment options ssl_certificate and ssl_private_key (in section webserver), and set these to the right value, eg:<br>
<pre><code>ssl_certificate = /mysafeplace/mycert.pem <br>
ssl_private_key = /mysafeplace/mycert.pem<br>
#In this example certificate and private key are in the same pem-file.<br>
</code></pre>
</li><li>restart bots-webserver<br>
</li><li>point your browser to the right https-address, eg: <i>https://localhost:8080</i></li></ol>

<h3>Tips</h3>
If you are using cherrypy and receive an error "ssl_error_rx_record_too_long" try the 2-line fix at <a href='https://bitbucket.org/cherrypy/cherrypy/issue/1293/ssl-broken-under-pypy-221'>https://bitbucket.org/cherrypy/cherrypy/issue/1293/ssl-broken-under-pypy-221</a>

You can create self-signed certificates at <a href='http://www.selfsignedcertificate.com/'>http://www.selfsignedcertificate.com/</a>

You can configure port=443 in bots.ini then just point your browser to <i>https://localhost</i>