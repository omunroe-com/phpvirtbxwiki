<div class="markdown_content"><p><strong>Introduction</strong></p>
<p>phpVirtualBox requires a web server with PHP &gt;= 5.1.0 installed in order to run. The following may help you install these on the machine on which you intend to run phpVirtualBox. If you already have a web server with PHP installed, you may simply copy phpVirtualBox to the document root folder of that web server.</p>
<hr/>
<p>Contents</p>
<div class="toc">
<ul>
<li><a href="#windows">Windows</a></li>
<li><a href="#linux">Linux</a></li>
<li><a href="#os-x">OS X</a></li>
<li><a href="#solaris">Solaris</a></li>
</ul>
</div>
<hr/>
<h2 id="windows">Windows</h2>
<p>On Windows, instead of mucking around with IIS, you may install XAMPP or XAMPPLite from <a class="alink notfound" href="../http%3A//www.apachefriends.org/">[http://www.apachefriends.org/]</a>. The installation is very straight-forward and includes a recent version of PHP (certainly greater than 5.1.0).</p>
<p>After installation, launch the XAMPP control panel and click Start next to Apache. You can copy phpVirtualBox to XAMPP's htdocs folder. Typically C:\xampp\htdocs or C:\xampplite\htdocs.</p>
<h2 id="linux">Linux</h2>
<p>The details of installing a web server and PHP differ greatly from distribution to distribution. <em>Please follow the instructions for your Linux distribution as provided by the distribution maintainer(s).</em> In most cases, you simply install apache2 and the apache2 php5 module using your distribution's package management system. E.g.</p>
<div class="codehilite"><pre><span></span>  apt-get install apache2

  apt-get install libapache2-mod-php5
</pre></div>


<p>After installation, copy phpVirtualBox to the document root of your web server. This is typically /var/www or /usr/local/apache2/htdocs.</p>
<h2 id="os-x">OS X</h2>
<p>On OS X, you may install XAMPP or XAMPPLite from <a class="alink notfound" href="../http%3A//www.apachefriends.org/">[http://www.apachefriends.org/]</a>. The installation is very straight-forward and includes a recent version of PHP (certainly greater than 5.1.0).</p>
<p>After installation, launch the XAMPP control panel and click Start next to Apache. You can copy phpVirtualBox to XAMPP's htdocs folder. Typically /Applications/XAMPP/htdocs/.</p>
<h2 id="solaris">Solaris</h2>
<p>On Solaris, you may install XAMPP or XAMPPLite from <a class="alink notfound" href="../http%3A//www.apachefriends.org/">[http://www.apachefriends.org/]</a>. The installation is very straight-forward and includes a recent version of PHP (certainly greater than 5.1.0).</p>
<p>(Assuming you kept the default installation path) After installation, run the following command as root:</p>
<div class="codehilite"><pre><span></span>  /opt/xampp/xampp startapache
</pre></div>


<p>You can copy phpVirtualBox to XAMPP's htdocs folder. Typically /opt/xampp/htdocs/. </p></div>
