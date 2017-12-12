<div class="markdown_content"><p><strong>Introduction</strong></p>
<p>phpVirtualBox requires a web server with PHP &gt;= 5.1.0 installed in order to run. Moreover, some php extensions need to be enabled : php-xml, php-json and php-soap. The following may help you install these on the machine on which you intend to run phpVirtualBox.</p>
<hr/>
<p>Contents</p>
<div class="toc">
<ul>
<li><a href="#windows">Windows</a></li>
<li><a href="#linux">Linux</a></li>
<ul>
<li><a href="#debian">Debian/Ubuntu/Mint</a></li>
<li><a href="#fedora">Fedora</a></li>
<li><a href="#centos">CentOS</a></li>
<li><a href="#archlinux">Arch Linux</a></li>
</ul>
<li><a href="#os-x">OS X</a></li>
<li><a href="#solaris">Solaris</a></li>
</ul>
</div>
<hr/>
<h2 id="windows">Windows</h2>
<p>On Windows, instead of mucking around with IIS, you may install XAMPP or XAMPPLite from <a class="alink notfound" href="https://www.apachefriends.org">[www.apachefriends.org]</a>. The installation is very straight-forward and includes a recent version of PHP (certainly greater than 5.1.0).</p>
<p>After installation, launch the XAMPP control panel and click "Config" next to Apache, then "PHP (php.ini)". It will open the php configuration file "php.ini" in notepad.</p>
<p>Uncomment the following line (E.G. remove the ";") and close the file after having saved the changes.</p>
<div class="codehilite"><pre><span></span>;extension=php_soap.dll</pre></div>
<p>In the XAMPP control panel, click "Start" next to Apache.</p>
<p> You can copy phpVirtualBox to XAMPP's htdocs folder. Typically C:\xampp\htdocs or C:\xampplite\htdocs.</p>
<h2 id="linux">Linux</h2>
<p>The details of installing a web server and PHP differ greatly from distribution to distribution. In most cases, you simply have to install apache2 and the apache2 php module (&gt;=5.1.0) using your distribution's package management system. Please follow the instructions for your Linux distribution as provided by the distribution maintainer(s).</p>
<p>The following gives basic instructions for common Linux distributions, without any warranty. </p>

<p>Note : The following must be done as root user.</p>
 

<h3 id="debian">Debian based distributions </h3>
<p>The following has been tested with Debian 8 "Stretch", Ubuntu 17.10 "Artful" and Mint 18.3 "Sylvia".</p>
<ul><li>Install the required packages :</li>
<div class="codehilite"><pre><span></span>apt-get install apache2 libapache2-mod-php php php-soap php-xml</pre></div>


<li>The previous command should automatically enable apache php module. If it's not the case, you can run the following commands :</li>
<div class="codehilite"><pre><span></span>a2dismod mpm_event mpm_worker
a2enmod mpm_prefork php7.X</pre></div>
<p>You have to replace "X" in the last command depending on the php version provided with your Linux distribution (7.0, 7.1, 7.2, ...).</p>

</ul>

<p>Your web server should be ready for phpvirtualbox installation.</p>

<h3 id="fedora">Fedora</h3>
<p>The following has been tested with Fedora 27.</p>
<ul><li>Install the required packages :</li>
<div class="codehilite"><pre><span></span>dnf install httpd php php-soap php-xml</pre></div>
<li>To enable apache php module, you have to edit the file /etc/httpd/conf.modules.d/00-mpm.conf. Comment or uncomment the relevant lines so that this file contains : </li>
<div class="codehilite"><pre><span></span>LoadModule mpm_event_module modules/mod_mpm_event.so
#LoadModule mpm_prefork_module modules/mod_mpm_prefork.so</pre></div>
</ul>
<p>Your web server should be ready for phpvirtualbox installation.</p>

<h3 id="centos">CentOS</h3>
<p>The following has been tested with CentOS 7.4.</p>
<ul><li>Install the required packages :</li>
<div class="codehilite"><pre><span></span>yum install httpd php php-soap php-xml</pre></div>

<li>Apache php module should be enabled without any further configuration.</li>
</ul>
<p>Your web server should be ready for phpvirtualbox installation.</p>

<h3 id="archlinux">Arch Linux</h3>
<p>The following has been tested with up-to-date Arch Linux as of 2017 December.</p>
<ul><li>Install the required packages :</li>
<div class="codehilite"><pre><span></span>pacman -S  apache php php-apache</pre></div>
<li>Edit the file /etc/httpd/conf/httpd.conf in order to enable apache php module : </li>
<ul>
<li>Comment or uncomment the relevant lines so that this file contains : </p>
<div class="codehilite"><pre><span></span>LoadModule mpm_event_module modules/mod_mpm_event.so
#LoadModule mpm_prefork_module modules/mod_mpm_prefork.so</pre></div>
<li>Add the following line after the last "LoadModule" directive : </li>
<div class="codehilite"><pre><span></span>LoadModule php7_module modules/libphp7.so</pre></div>
<li>Add the following line after the last "Include" directive : </li>
<div class="codehilite"><pre><span></span>Include conf/extra/php7_module.conf</pre></div>
</ul>

<li>Uncomment the following line in /etc/php/php.ini in order to enable required php extension : </li>
<div class="codehilite"><pre><span></span>;extension=soap.so</pre></div>
</ul>

<p>Your web server should be ready for phpvirtualbox installation.</p>


<h2 id="os-x">OS X</h2>
<p>On OS X, you may install XAMPP or XAMPPLite from <a class="alink notfound" href="https://www.apachefriends.org">[www.apachefriends.org]</a>. The installation is very straight-forward and includes a recent version of PHP (certainly greater than 5.1.0).</p>
<p>After installation, launch the XAMPP control panel and click Start next to Apache. You can copy phpVirtualBox to XAMPP's htdocs folder. Typically /Applications/XAMPP/htdocs/.</p>
<h2 id="solaris">Solaris</h2>
<p>On Solaris, you may install XAMPP or XAMPPLite from <a class="alink notfound" href="https://www.apachefriends.org">[www.apachefriends.org]</a>. The installation is very straight-forward and includes a recent version of PHP (certainly greater than 5.1.0).</p>
<p>(Assuming you kept the default installation path) After installation, run the following command as root:</p>
<div class="codehilite"><pre><span></span>  /opt/xampp/xampp startapache
</pre></div>


<p>You can copy phpVirtualBox to XAMPP's htdocs folder. Typically /opt/xampp/htdocs/. </p></div>
