<div class="markdown_content"><p>On Linux systems, if you installed the official VirtualBox package (e.g. <a href="https://www.virtualbox.org/wiki/Linux_Downloads">from here</a>), it created the init script<em> /etc/init.d/vboxweb-service</em> or a systemd service file<em> /lib/systemd/system/vboxweb-service.service</em>, depending on your service manager (init or systemd). These can be used to start and stop vboxwebsrv.</p>

<p>In order to start vboxwebsrv, the file <em>/etc/default/virtualbox</em> must exist with correct settings.</p>

<p><B>Note :</B> If you have installed the VirtualBox package provided with your Linux distribution, the init script or the systemd service file may have a different name or a different location. Moreover, if your Linux distribution use systemd as service manager, your vboxwebsrv systemd service file may ignore the file <em>/etc/default/virtualbox</em>. This is the case with the default systemd service file provided with Arch Linux or Ubuntu.</p>

<p>While there may be numerous ways to configure vboxwebsrv, this document aims to keep it simple and suppose you installed the official VirtualBox package.
If the file <em>/etc/default/virtualbox</em> does not exist on your system, create it now. This file has the format:</p>
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
<p>VBOXWEB_USER should be set to the user that runs VirtualBox virtual machines on your system. If more than one user runs virtual machines, you will have to pick one (multiple instances are possible, but beyond the scope of this document). <B>DON'T USE THE ROOT USER, vboxwebsrv WON'T ACCEPT ANY CONNECTION</B>.</p>
<p>VBOXWEB_HOST should, in most cases, be set to <em>127.0.0.1</em>. If phpVirtualBox (your web server) is not running on the same host as vboxwebsrv and phpVirtualBox must communicate with vboxwebsrv over a network, this must be set to the external IP address of the host runing vboxwebsrv.</p>
<p>Your <em>/etc/default/virtualbox</em> may look like this:</p>
<div class="codehilite"><pre><span></span>VBOXWEB_USER=vbox
VBOXWEB_HOST=127.0.0.1
</pre></div>


<p>.. or if your web server and vboxwebsrv are NOT on the same host:</p>
<div class="codehilite"><pre><span></span>VBOXWEB_USER=remote_vbox
VBOXWEB_HOST=<em>192.168.0.4</em>
</pre></div>


<p>Note that these values are just examples. The user that runs virtual machines on your system may not be named "vbox."</p>
<p>Once this is done, you may start and stop vboxwebsrv by running as root user:</p>

<ul><li>If you use init scripts :</li>
<div class="codehilite"><pre><span></span>/etc/init.d/vboxweb-service start
/etc/init.d/vboxweb-service stop</pre></div>
<li>If you use systemd :</li>
<div class="codehilite"><pre><span></span>systemctl start vboxweb-service.service
systemctl stop vboxweb-service.service</pre></div>
</ul>
</div>