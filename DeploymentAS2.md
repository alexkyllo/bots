# Using AS2 with Bots #

## What is AS2 ##
AS2 (Applicability Statement 2) is a specification about how to transport data securely and reliably over the Internet. Security is achieved by using digital certificates and encryption.<br>
There are multiple forms of AS2, most used is AS2 over HTTP(S).<br>
AS2 (over HTTP) is a server protocol: to use AS2 you will need an AS2-server. Each partner requires their own AS2 communications gateway. All AS2 software is designed to be interoperable. There are several open source implementations, as well as commercial software and hosted services.<br>

See also <a href='http://en.wikipedia.org/wiki/AS2'>wikipedia</a>

<blockquote><img src='http://www.as2basics.co.uk/images/as2-b2b-implementation.gif' /></blockquote>


<br>
<h2>How to use AS2 with Bots</h2>

Several threads in the mailing list about this. To be condensed into a good how-to article...<br>
<ul><li><a href='http://groups.google.com/group/botsmail/browse_thread/thread/b98c49f9ec9c4e8a/15e9ed6dbae987f5'>http://groups.google.com/group/botsmail/browse_thread/thread/b98c49f9ec9c4e8a/15e9ed6dbae987f5</a>
</li><li><a href='http://groups.google.com/group/botsmail/browse_thread/thread/54c7462a32fb9741/c594d71fb214b8c1'>http://groups.google.com/group/botsmail/browse_thread/thread/54c7462a32fb9741/c594d71fb214b8c1</a>
</li><li><a href='http://groups.google.com/group/botsmail/browse_thread/thread/9bd0cc65461478b/0bbc729349392a1f'>http://groups.google.com/group/botsmail/browse_thread/thread/9bd0cc65461478b/0bbc729349392a1f</a></li></ul>

<br>
<h2>AS2 Software</h2>
<ul><li><a href='http://sourceforge.net/projects/mec-as2/'>http://sourceforge.net/projects/mec-as2/</a>
</li><li><a href='http://sourceforge.net/projects/openas2/'>http://sourceforge.net/projects/openas2/</a>
</li><li><a href='http://www.cecid.hku.hk/hermes.php'>http://www.cecid.hku.hk/hermes.php</a>
</li><li><a href='http://stackoverflow.com/questions/7426951/is-anyone-using-python-for-gs1-xml-and-as2-edi'>http://stackoverflow.com/questions/7426951/is-anyone-using-python-for-gs1-xml-and-as2-edi</a>
<a href='Hidden comment: 
hje: checked this, but as2 server skips checks; checks are available in commercial edition (private conversation with patrice). This is not good, as2 is supposed to be secure. will check this better.
http://code.google.com/p/babelas2/
'></a>