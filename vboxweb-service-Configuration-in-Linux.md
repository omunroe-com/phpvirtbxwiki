<div class="markdown_content"><p>On Linux systems, VirtualBox creates the init script <em>/etc/init.d/vboxweb-service</em> when it is installed. This can be used to start and stop vboxwebsrv. While there may be numerous ways to configure this script, this document aims to keep it simple.</p>
<p>In order for vboxweb-service start vboxwebsrv, the file <em>/etc/default/virtualbox</em> must exist with correct settings. If this file does not exist on your system, create it now. This file has the format:</p>
<div class="codehilite"><pre><span></span>SETTING1=value
SETTING2=value
</pre></div>


<p>The following settings are available for use in this file:</p>
<table>
<thead>
<tr>
<th>Setting</th>
<th>Description</th>
</tr>
</thead>
<tbody>
<tr>
<td>VBOXWEB_USER</td>
<td>The user as which vboxwebsrv will run.</td>
</tr>
<tr>
<td>VBOXWEB_HOST</td>
<td>The host to bind to (localhost).</td>
</tr>
<tr>
<td>VBOXWEB_PORT</td>
<td>The port to bind to (18083).</td>
</tr>
<tr>
<td>VBOXWEB_TIMEOUT</td>
<td>Session timeout in seconds; 0 = disable timeouts (300).</td>
</tr>
<tr>
<td>VBOXWEB_CHECK_INTERVAL</td>
<td>Frequency of timeout checks in seconds (5).</td>
</tr>
<tr>
<td>VBOXWEB_THREADS</td>
<td>Maximum number of worker threads to run in parallel (100).</td>
</tr>
<tr>
<td>VBOXWEB_KEEPALIVE</td>
<td>Maximum number of requests before a socket will be closed (100).</td>
</tr>
<tr>
<td>VBOXWEB_LOGFILE</td>
<td>Name of file to write log to (no file).</td>
</tr>
<tr>
<td>INSTALL_DIR</td>
<td>The location of the vboxwebsrv binary (/usr/lib/virtualbox).</td>
</tr>
</tbody>
</table>
<p>At a minimum, <em>VBOXWEB_USER</em> and <em>VBOXWEB_HOST</em> must be set.</p>
<p>VBOXWEB_USER should be set to the user that runs VirtualBox virtual machines on your system. If more than one user runs virtual machines, you will have to pick one (multiple instances are possible, but beyond the scope of this document).</p>
<p>VBOXWEB_HOST should, in most cases, be set to <em>127.0.0.1</em>. If phpVirtualBox (your web server) is not running on the same host as vboxwebsrv and phpVirtualBox must communicate with vboxwebsrv over a network, this must be set to the external IP address of the host runing vboxwebsrv.</p>
<p>Your <em>/etc/default/virtualbox</em> may look like this:</p>
<div class="codehilite"><pre><span></span>VBOXWEB_USER=vbox
VBOXWEB_HOST=127.0.0.1
</pre></div>


<p>.. or <em>if your web server and vboxwebsrv are on NOT the same host</em>:</p>
<div class="codehilite"><pre><span></span>VBOXWEB_USER=remote_vbox
VBOXWEB_HOST=192.168.0.4
</pre></div>


<p>Note that these values are just examples. The user that runs virtual machines on your system may not be named "vbox."</p>
<p>Once this is done, you may start and stop vboxwebsrv by running:</p>
<p><em>/etc/init.d/vboxweb-service start</em> <br/>
-or-<br/>
<em>/etc/init.d/vboxweb-service stop</em> </p>
<p>as the root user on your system.</p></div>