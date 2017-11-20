<div class="markdown_content"><p><strong>Contents</strong></p>
<div class="toc">
<ul>
<li><a href="#what-is-virtualbox">What is VirtualBox?</a></li>
<li><a href="#what-is-phpvirtualbox">What is phpVirtualBox?</a></li>
<li><a href="#getting-started">Getting started</a><ul>
<li><a href="#installing-virtualbox">Installing VirtualBox</a><ul>
<li><a href="#virtualbox-40-remote-console-access-note">VirtualBox &gt;= 4.0 - Remote Console Access Note</a></li>
</ul>
</li>
<li><a href="#setting-up-virtualbox">Setting up VirtualBox</a><ul>
<li><a href="#virtualbox-3x-ose-note">VirtualBox 3.x OSE Note</a></li>
<li><a href="#linux">Linux</a></li>
<li><a href="#solaris">Solaris</a></li>
<li><a href="#windows">Windows</a></li>
<li><a href="#os-x">OS X</a></li>
</ul>
</li>
<li><a href="#installing-phpvirtualbox">Installing phpVirtualBox</a><ul>
<li><a href="#download-and-installation">Download and Installation</a><ul>
<li><a href="#freebsd-note">FreeBSD Note</a></li>
<li><a href="#other-oss">Other OSs</a></li>
<li><a href="#selinux-considerations">SELinux Considerations</a></li>
<li><a href="#arch-linux-considerations">Arch Linux Considerations</a></li>
</ul>
</li>
<li><a href="#basic-configuration">Basic configuration</a></li>
<li><a href="#advanced-configuration">Advanced configuration</a></li>
</ul>
</li>
</ul>
</li>
<li><a href="#getting-help">Getting Help</a></li>
<li><a href="#upgrading-phpvirtualbox">Upgrading phpVirtualBox</a><ul>
<li><a href="#upgrading-from-virtualbox-3x-to-4x">Upgrading from VirtualBox 3.x to 4.x</a></li>
<li><a href="#vboxwebsrv">vboxwebsrv</a></li>
<li><a href="#post-upgrade">Post Upgrade</a></li>
</ul>
</li>
<li><a href="#translating-phpvirtualbox">Translating phpVirtualBox</a><ul>
<li><a href="#character-encoding-note">Character Encoding Note</a></li>
</ul>
</li>
</ul>
</div>
<hr/>
<h1 id="what-is-virtualbox">What is VirtualBox?</h1>
<p>If you are new to VirtualBox, simply put - it is virtualization software that allows one to run multiple virtual machine instances (guests) on a single physical machine (host).</p>
<p><em>"VirtualBox is a powerful x86 and AMD64/Intel64 virtualization product for enterprise as well as home use. Not only is VirtualBox an extremely feature rich, high performance product for enterprise customers, it is also the only professional solution that is freely available as Open Source Software under the terms of the GNU General Public License (GPL) version 2."</em></p>
<p><a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a></p>
<h1 id="what-is-phpvirtualbox">What is phpVirtualBox?</h1>
<p>phpVirtualBox is a web-based front-end to VirtualBox that allows you to control your VirtualBox environment.</p>
<h1 id="getting-started">Getting started</h1>
<p>phpVirtualBox is a PHP application, so like all PHP applications, it needs to be run under a PHP-capable web server. It manages your VirtualBox installation by communicating with VirtualBox's API server (vboxwebsrv - distributed with VirtualBox) over a network connection.</p>
<div class="codehilite"><pre><span></span> -----------------------------------------------------
 | Web Server                                        |
 |    phpVirtualBox (config.php contains VirtualBox  |
 |     |              access information)            |
 ------|----------------------------------------------
       |
   Authentication and VirtualBox communication
       |
       |  -----------------------------------------------
       |  | VirtualBox Installation                     |
       |  |                                             |
       '---- vboxwebsrv (running as user X)             |
          |    |                                        |
          |    '--- User X's VirtualBox configuration   |
          |         and virtual machines                |
          |                                             |
          -----------------------------------------------
</pre></div>


<p>Since communication is performed over the network, phpVirtualBox and VirtualBox do not <strong>HAVE</strong> to reside on the same physical machine. Though, in most cases, they do. phpVirtualBox can even control multiple VirtualBox installations running on multiple hosts.</p>
<h2 id="installing-virtualbox">Installing VirtualBox</h2>
<p>First you will need to install VirtualBox from <a href="http://www.virtualbox.org." rel="nofollow">http://www.virtualbox.org.</a> Any questions regarding VirtualBox or its installation should be raised at the support forums on the VirtualBox web site.</p>
<h3 id="virtualbox-40-remote-console-access-note">VirtualBox &gt;= 4.0 - Remote Console Access Note</h3>
<p>In order to access a VM's console over RDP (via phpVirtualBox's console tab, or other RDP client) you must install the <em>Oracle VM VirtualBox Extension Pack</em> from: <a href="http://www.virtualbox.org/wiki/Downloads" rel="nofollow">http://www.virtualbox.org/wiki/Downloads</a></p>
<p>Please refer to VirtualBox's documentation for instructions on installing extension packs.</p>
<h2 id="setting-up-virtualbox">Setting up VirtualBox</h2>
<p>phpVirtualBox requires that vboxwebsrv (a program distributed with VirtualBox) is running on your VirtualBox host. On <code>*</code>nix hosts, this is typically found in /usr/bin. On Windows, it is typically found in C:\Program Files\Oracle\VirtualBox. This program MUST be run as the same user that administers your VirtualBox virtual machines. On Windows and OS X, this simply means the same user that you log into your machine as when you run VirtualBox.</p>
<p><strong><em>NOTE</em></strong></p>
<p>If your web server and your VirtualBox installation are on 2 different hosts, you may need to add:</p>
<p>-H IP.ADDRESS.OF.HOST</p>
<p>to the command line of vboxwebsrv. Where IP.ADDRESS.OF.HOST is the IP address of your VirtualBox host, accessible by your web server. If this is not specified, vboxwebsrv will listen on localhost, which is not accessible outside of itself.</p>
<h3 id="virtualbox-3x-ose-note">VirtualBox 3.x OSE Note</h3>
<p>For <em>VirtualBox 3.x OSE</em> users, you must execute the following command:</p>
<div class="codehilite"><pre><span></span>   VBoxManage setproperty websrvauthlibrary null
</pre></div>


<p>This disables authentication for vboxwebsrv. At the moment, this is the only way for an application to communicate with the OSE version of vboxwebsrv. Taking security into consideration, only run vboxwebsrv OSE on a non-public network. </p>
<p>If you are not sure whether or not you are running the OSE version of VirtualBox, you can run:</p>
<div class="codehilite"><pre><span></span>vboxwebsrv -h
</pre></div>


<p>If the first line contains "OSE" (e.g. Oracle VM VirtualBox web service version x.x.x_OSE), you are running the OSE version of VirtualBox.</p>
<h3 id="linux">Linux</h3>
<p>Linux users should use the instructions for vboxweb-service found at <a href="https://github.com/phpvirtualbox/phpvirtualbox/wiki/vboxweb-service-Configuration-in-Linux">vboxweb-service Configuration in Linux</a></p>
<h3 id="solaris">Solaris</h3>
<p>Assuming your VirtualBox installation is run by the user <em>vbox</em> and vboxwebsrv is located in /opt/VirtualBox, you may start vboxwebsrv by running the following command as <em>vbox</em>:</p>
<div class="codehilite"><pre><span></span> /opt/VirtualBox/vboxwebsrv -H 127.0.0.1 -b --logfile /dev/null &gt;/dev/null
</pre></div>


<p>Solaris users will also have to follow the same instructions outlined in the VirtualBox OSE section above, or vboxwebsrv will fail to authenticate.</p>
<h3 id="windows">Windows</h3>
<p>On Windows (assuming your VirtualBox installation is located in C:\Program Files\Oracle\VirtualBox), the following command will start vboxwebsrv:</p>
<div class="codehilite"><pre><span></span>   "%ProgramFiles%\Oracle\VirtualBox\vboxwebsrv.exe" -H 127.0.0.1 &gt;nul
</pre></div>


<p>Note that <em>&gt;nul</em> is needed so that vboxwebsrv does not send its output to the command prompt window. Without it, performance will be severely degraded.</p>
<p>User-contributed documentation on setting up vboxwebsrv.exe to start when your computer boots can be found <a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Windows%207%20-%202008%20%2B%20Service/">here</a>.</p>
<h3 id="os-x">OS X</h3>
<p>In OS X, start Terminal (usually located in Applications -&gt; Utilities) and enter the following commands:</p>
<div class="codehilite"><pre><span></span>  cd /Applications/VirtualBox.app/Contents/MacOS

  ./vboxwebsrv -H 127.0.0.1 &gt;/dev/null
</pre></div>


<p>Running /usr/bin/vboxwebsrv or not running the command from within /Applications/VirtualBox.app/Contents/MacOS seems to crash vboxwebsrv</p>
<h2 id="installing-phpvirtualbox">Installing phpVirtualBox</h2>
<p>phpVirtualBox requires a web server with PHP &gt;= 5.1.0 installed in order to run. If you do not already have a PHP-capable web server running, <a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Web%20server%20and%20PHP%20installation/">this</a> may help you get started.</p>
<hr/>
<h3 id="download-and-installation">Download and Installation</h3>
<h4 id="freebsd-note">FreeBSD Note</h4>
<p>Thanks to Bernhard Fröhlich for his time and effort in creating the FreeBSD port.</p>
<p>To install the port:</p>
<div class="codehilite"><pre><span></span>cd /usr/ports/www/phpvirtualbox/ &amp;&amp; make install clean
</pre></div>


<p>To add the package:</p>
<div class="codehilite"><pre><span></span>pkg_add -r phpvirtualbox
</pre></div>


<hr/>
<h4 id="other-oss">Other OSs</h4>
<ul>
<li>Download the latest version of phpVirtualBox from the Files tab</li>
<li>Unzip the downloaded file and copy the resulting files / folders to a folder accessible by your <a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Web%20server%20and%20PHP%20installation/">web server</a></li>
</ul>
<h4 id="selinux-considerations">SELinux Considerations</h4>
<p>If SELinux is installed and you would like to keep it enabled, you may have to add a rule for vboxwebsrv.</p>
<p>Install semanage (yum install policycoreutils-python) and run the command below:</p>
<div class="codehilite"><pre><span></span>semanage port -a -t http_port_t -p tcp 18083
</pre></div>


<p>This will add the VirtualBox's web service port (18083) to be accessible by a service running in an http context (eg. apache).</p>
<h4 id="arch-linux-considerations">Arch Linux Considerations</h4>
<p>In Arch Linux, be sure to edit /etc/php/php.ini, and uncomment the following lines:</p>
<div class="codehilite"><pre><span></span>;extension=json.so
;extension=soap.so
</pre></div>


<p>by removing the ';' at the beginning of each. Then restart apache.</p>
<h3 id="basic-configuration">Basic configuration</h3>
<p><strong><em>config.php</em></strong> in phpVirtualBox's folder on your web server tells phpVirtualBox how to communicate with your VirtualBox installation. To get started, rename config.php-example to config.php and edit it to reflect your settings. The minimal amount of configuration you will need is to specify the username and password needed, as well as the location of vboxwebsrv.</p>
<div class="codehilite"><pre><span></span><span class="c">/* Username / Password for system user that runs VirtualBox */</span>
<span class="nt">var</span> <span class="o">$</span><span class="nt">username</span> <span class="o">=</span> <span class="s1">'vbox'</span><span class="o">;</span>
<span class="nt">var</span> <span class="o">$</span><span class="nt">password</span> <span class="o">=</span> <span class="s1">'pass'</span><span class="o">;</span>

<span class="c">/* SOAP URL of vboxwebsrv (not phpVirtualBox's URL) */</span>
<span class="nt">var</span> <span class="o">$</span><span class="nt">location</span> <span class="o">=</span> <span class="s1">'http://127.0.0.1:18083/'</span><span class="o">;</span>
</pre></div>


<p>The username and password must be the username and password of the user that vboxwebsrv is running as. If VirtualBox and phpVirtualBox are on the same physical host, you may leave the $location setting alone. Once this is configured:</p>
<ul>
<li>Navigate to the resulting folder in your web browser. Typically <a href="http://your.web.server.ip/phpvirtualbox" rel="nofollow">http://your.web.server.ip/phpvirtualbox</a></li>
<li>Default login is admin / admin. See <a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Authentication%20in%20phpVirtualBox/">Authentication in phpVirtualBox</a> for more information on controlling users and passwords within phpVirtualBox.</li>
</ul>
<p>If you have any trouble, see the <a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Common%20phpVirtualBox%20Errors%20and%20Issues/">Common Errors and Issues</a> wiki page.</p>
<h3 id="advanced-configuration">Advanced configuration</h3>
<p>Other configuration options and settings are well documented in config.php itself. More help can be found at:</p>
<ul>
<li><a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Authentication%20Modules/">Using External Authentication</a></li>
<li><a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Custom%20VM%20Icons/">Enabling Custom VM Icons</a></li>
<li><a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Advanced%20Settings/">Enabling Advanced Settings in phpVirtualBox</a></li>
<li><a class="" href="http://sourceforge.net/p/phpvirtualbox/wiki/Multiple%20Server%20Configuration/">Multiple Server Configuration</a></li>
</ul>
<h1 id="getting-help">Getting Help</h1>
<p>Please see the <a class="" href="https://sourceforge.net/p/phpvirtualbox/wiki/Common%20phpVirtualBox%20Errors%20and%20Issues/">Common Errors and Issues</a> wiki page first!</p>
<p>If your error or issue is not listed, please use the <a class="" href="https://sourceforge.net/p/phpvirtualbox/discussion/">Forums</a>.</p>
<p>Please do not open a Bug report unless it is identified as a bug by a project member.</p>
<h1 id="upgrading-phpvirtualbox">Upgrading phpVirtualBox</h1>
<p>phpVirtualBox can be "upgraded" by copying the downloaded files over your existing phpVirtualBox installation. Choose to overwrite existing files if prompted.</p>
<p>You may wish to create an entirely new folder for a new version of phpVirtualBox and that is fine too.</p>
<h2 id="upgrading-from-virtualbox-3x-to-4x">Upgrading from VirtualBox 3.x to 4.x</h2>
<p>If you have upgraded from VirtualBox 3.2.x, you will have to run the following commands on your VirtualBox host <em>as the same user that runs vboxwebsrv</em>:<br/>
        VBoxManage setproperty vrdeauthlibrary default </p>
<div class="codehilite"><pre><span></span>    VBoxManage setproperty websrvauthlibrary default
</pre></div>


<p><strong><em>NOTE: On windows, start a command prompt and type:</em></strong></p>
<div class="codehilite"><pre><span></span>    cd "%ProgramFiles%\Oracle\VirtualBox"
</pre></div>


<p>Before entering the VBoxManage commands.</p>
<h2 id="vboxwebsrv">vboxwebsrv</h2>
<p>After upgrading, it is a good idea to stop vboxwebsrv for the time being. If you are using the startup script distributed on this site, you may run the following command:</p>
<div class="codehilite"><pre><span></span>/etc/init.d/vboxwebsrv stop
</pre></div>


<p>If your VirtualBox host is running Linux, please see: <a href="http://sourceforge.net/p/phpvirtualbox/wiki/vboxweb-service%20Configuration%20in%20Linux/">http://sourceforge.net/p/phpvirtualbox/wiki/vboxweb-service%20Configuration%20in%20Linux/</a> for a new-and-improved startup script configuration.</p>
<p>Then, start vboxwebsrv. If you are now using the vboxweb-service script described in the above link, you may run:</p>
<div class="codehilite"><pre><span></span>/etc/init.d/vboxweb-service start
</pre></div>


<p>If you are not, you may start vboxwebsrv using the same method you had been using for VirtualBox 3.x.</p>
<h2 id="post-upgrade">Post Upgrade</h2>
<p>It is always a good idea to clear your web browser's cache after upgrading.</p>
<h1 id="translating-phpvirtualbox">Translating phpVirtualBox</h1>
<p>phpVirtualBox uses VirtualBox's translations for most of its text. This reduces the amount of text one must translate for phpVirtualBox to less than 60 items. As a result, only languages available to VirtualBox may be translated for phpVirtualBox:</p>
<ul>
<li>ﺎﻠﻋﺮﺒﻳﺓ    ar</li>
<li>Български (България)        bg</li>
<li>Català      ca</li>
<li>Català (valencià)   ca_VA</li>
<li>Čeština     cs</li>
<li>Dansk       da</li>
<li><s>Deutsch     de</s></li>
<li>Ελληνικά    el</li>
<li><s>Español     es</s></li>
<li>Euskara     eu</li>
<li>Suomi (Suomi)       fi</li>
<li><s>Français    fr</s></li>
<li>Galego (España)     gl_ES</li>
<li>Magyar      hu</li>
<li>Bahasa Indonesia    id</li>
<li><s>Italiano    it</s></li>
<li><s>日本語      ja</s></li>
<li>ខ្មែរ km_KH</li>
<li>한국어      ko</li>
<li>Lietuvių    lt</li>
<li>Nederlands  nl</li>
<li><s>Polski      pl</s></li>
<li><s>Português (Brasil)  pt_BR</s></li>
<li>Português   pt</li>
<li>Română      ro</li>
<li><s>Русский     ru</s></li>
<li>Slovenčina  sk</li>
<li>Српски      sr</li>
<li>Svenska     sv</li>
<li>Türkçe      tr</li>
<li>Українська  uk</li>
<li><s>简体中文 (中国)     zh_CN</s></li>
<li><s>正體中文 (臺灣)     zh_TW</s></li>
</ul>
<p>Languages <s>crossed out</s> above have already been translated for phpVirtualBox.</p>
<p>To translate phpVirtualBox, locate a language XML file in phpVirtualBox's languages folder. For instance, de.xml. The file will have entries that look similar to:</p>
<div class="codehilite"><pre><span></span><span class="cp">&lt;?xml version="1.0" encoding="utf-8"?&gt;</span>
<span class="nt">&lt;language&gt;</span>
    <span class="nt">&lt;context&gt;</span>
        <span class="nt">&lt;name&gt;</span>phpVirtualBox<span class="nt">&lt;/name&gt;</span>
        <span class="nt">&lt;message&gt;</span>
            <span class="nt">&lt;source&gt;</span>Warning: A VirtualBox internal operation is in progress. Closing this window or navigating away from this web page may cause unexpected and undesirable results. Please wait for the operation to complete.<span class="nt">&lt;/source&gt;</span>
            <span class="nt">&lt;translation&gt;</span>Warnung: Interne Aktion läuft. Wenn Sie dieses Fenster schließen oder diese Seite verlassen, kann das zu unerwünschten oder unbeabsichtigten Effekten führen. Bitte warten Sie bis die Aktion abgeschlossen ist.<span class="nt">&lt;/translation&gt;</span>
        <span class="nt">&lt;/message&gt;</span>
        <span class="nt">&lt;message&gt;</span>
            <span class="nt">&lt;source&gt;</span>Operation Canceled<span class="nt">&lt;/source&gt;</span>
            <span class="nt">&lt;translation&gt;</span>Aktion abgebrochen<span class="nt">&lt;/translation&gt;</span>
        <span class="nt">&lt;/message&gt;</span>
                 ......
</pre></div>


<p>You will see translation messages such as: </p>
<div class="codehilite"><pre><span></span>    <span class="nt">&lt;message&gt;</span>
       <span class="nt">&lt;source&gt;</span>Operation Canceled<span class="nt">&lt;/source&gt;</span>
       <span class="nt">&lt;translation&gt;</span>Aktion abgebrochen<span class="nt">&lt;/translation&gt;</span>
    <span class="nt">&lt;/message&gt;</span>
</pre></div>


<p>Text within the <code>&lt;source&gt;</code> tag is the text that is to be translated. The translated text goes in the <code>&lt;translation&gt;</code> tag. E.g.</p>
<div class="codehilite"><pre><span></span><span class="nt">&lt;message&gt;</span>
   <span class="nt">&lt;source&gt;</span>Operation Canceled<span class="nt">&lt;/source&gt;</span>
   <span class="nt">&lt;translation&gt;</span>Your translation of "Operation Canceled" goes here...<span class="nt">&lt;/translation&gt;</span>
<span class="nt">&lt;/message&gt;</span>
</pre></div>


<p>Translate the file, then send it to the mailing list. It should appear in the next version of phpVirtualBox.</p>
<h2 id="character-encoding-note">Character Encoding Note</h2>
<p>All translations should use UTF-8 encoding.</p>
<ul>
<li>Using Notepad in Windows, you may select UTF-8 encoding in the Save as... dialog.</li>
<li>Using vi, you may enter the command <em>:set enc=utf-8</em></li>
</ul>
<p>Other text editors should have some way to change / set the encoding used.</p></div>

  <div id="create_wiki_page_holder" title="Create New Page" style="display:none">
    <form>
        <label class="grid-2">Name</label>
        <div class="grid-7"><input type="text" name="name"/></div>
    </form>
  </div>
