<div class="markdown_content"><p><strong>Introduction</strong></p>
<p>Advanced settings that do not appear in the !VirtualBox GUI have been added to phpVirtualBox. These can be enabled by setting or adding:</p>
<div class="codehilite"><pre><span></span>var $enableAdvancedConfig = true;
</pre></div>


<p>in config.php.</p>
<p><em>NOTE: though the following sections reference VBoxManage (a command line tool distributed with !VirtualBox), phpVirtualBox does not use VBoxManage to perform these actions. VBoxManage equivalent commands are provided for documentation reference only.</em></p>
<hr/>
<p><strong>Contents</strong></p>
<div class="toc">
<ul>
<li><a href="#input-tab">Input Tab</a></li>
<li><a href="#hpet-and-host-time-sync">HPET and Host time sync</a></li>
<li><a href="#acceleration">Acceleration</a></li>
<li><a href="#vrde-net-address">VRDE Net Address</a></li>
<li><a href="#additional-nat-settings">Additional NAT Settings</a></li>
<li><a href="#media-selection-has-a-virtual-media-manager-button">Media Selection has a Virtual Media Manager button</a></li>
<li><a href="#virtual-media-manager-additional-buttons">Virtual Media Manager additional buttons</a><ul>
<li><a href="#new">New</a></li>
<li><a href="#add">Add</a></li>
<li><a href="#add-iscsi">Add iSCSI</a></li>
</ul>
</li>
</ul>
</div>
<hr/>
<h2 id="input-tab">Input Tab</h2>
<p>An Input tab is available in the General section of Virtual Machines' settings windows.</p>
<p><img src="https://phpvirtualbox.github.io/images/advinput.png"/></p>
<table>
<thead>
<tr>
<th>Label</th>
<th>VBoxManage equivalent</th>
</tr>
</thead>
<tbody>
<tr>
<td>Keyboard</td>
<td>VBoxManage modifyvm --keyboard</td>
</tr>
<tr>
<td>Mouse</td>
<td>VBoxManage modifyvm --mouse</td>
</tr>
</tbody>
</table>
<p>See the VBoxManage documentation at <a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a> for more information on these settings.</p>
<h2 id="hpet-and-host-time-sync">HPET and Host time sync</h2>
<p>An HPET (High Precision Event Timer) setting is available in the System section on the Motherboard tab of Virtual Machines' settings windows.</p>
<p>A Disable host time sync option is available to disable time synchronization between the !VirtualBox host and the virtual machine.</p>
<p><img src="https://phpvirtualbox.github.io/images/advhpet.png"/></p>
<table>
<thead>
<tr>
<th>Label</th>
<th>VBoxManage equivalent</th>
</tr>
</thead>
<tbody>
<tr>
<td>HPET (high precision event timer)</td>
<td>VBoxManage modifyvm --hpet</td>
</tr>
<tr>
<td>Disable host time sync</td>
<td>VBoxManage setextradata "VBoxInternal/Devices/VMMDev/0/Config/GetHostTimeDisabled" "1"</td>
</tr>
</tbody>
</table>
<p>See the VBoxManage documentation at <a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a> for more information on these settings.</p>
<h2 id="acceleration">Acceleration</h2>
<p>Acceleration settings are available in the System section on the Acceleration tab of Virtual Machines' settings windows.</p>
<p><img src="https://phpvirtualbox.github.io/images/advaccel.png"/></p>
<table>
<thead>
<tr>
<th>Label</th>
<th>VBoxManage equivalent</th>
</tr>
</thead>
<tbody>
<tr>
<td>Enable VT-x/AMD-V</td>
<td>VBoxManage modifyvm --hwvirtex</td>
</tr>
<tr>
<td>Enable Nested Paging</td>
<td>VBoxManage modifyvm --nestedpaging</td>
</tr>
<tr>
<td>Enable Large Pages</td>
<td>VBoxManage modifyvm --largepages</td>
</tr>
<tr>
<td>Enable exclusive use of the hardware virtualization extensions</td>
<td>VBoxManage modifyvm --hwvirtexexcl</td>
</tr>
<tr>
<td>Enable VT-x VPID (Intel only)</td>
<td>VBoxManage modifyvm --vtxvpid</td>
</tr>
</tbody>
</table>
<p>See the VBoxManage documentation at <a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a> for more information on these settings.</p>
<h2 id="vrde-net-address">VRDE Net Address</h2>
<p>A Net Address setting is available in the Display section on the Remote Display tab of Virtual Machines' settings windows.</p>
<p><img src="https://phpvirtualbox.github.io/images/advnetaddress.png"/></p>
<table>
<thead>
<tr>
<th>Label</th>
<th>VBoxManage equivalent</th>
</tr>
</thead>
<tbody>
<tr>
<td>Net Address</td>
<td>VBoxManage modifyvm --vrdeaddress</td>
</tr>
</tbody>
</table>
<p>See the VBoxManage documentation at <a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a> for more information on these settings.</p>
<h2 id="additional-nat-settings">Additional NAT Settings</h2>
<p>Additional NAT settings are available in the Network section of Virtual Machines' settings windows when a network adapter's Attached To setting is configured as NAT.</p>
<p><img src="https://phpvirtualbox.github.io/images/advnat.png"/></p>
<table>
<thead>
<tr>
<th>Label</th>
<th>VBoxManage equivalent</th>
</tr>
</thead>
<tbody>
<tr>
<td>Proxy Only</td>
<td>VBoxManage modifyvm --nataliasmode</td>
</tr>
<tr>
<td>Same Ports</td>
<td>VBoxManage modifyvm --nataliasmode</td>
</tr>
<tr>
<td>Pass DNS Domain</td>
<td>VBoxManage modifyvm --natdnspassdomain</td>
</tr>
<tr>
<td>DNS Proxy</td>
<td>VBoxManage modifyvm --natdnsproxy</td>
</tr>
<tr>
<td>Use Host Resolver</td>
<td>VBoxManage modifyvm --natdnshostresolver</td>
</tr>
<tr>
<td>Bind to IP</td>
<td>VBoxManage modifyvm --natbindip</td>
</tr>
</tbody>
</table>
<p>See the VBoxManage documentation at <a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a> for more information on these settings.</p>
<h2 id="media-selection-has-a-virtual-media-manager-button">Media Selection has a Virtual Media Manager button</h2>
<p>All media selection buttons have a Virtual Media Manager button that will allow direct access to the Virtual Media Manager.</p>
<p><img src="https://phpvirtualbox.github.io/images/advvmmmenu.png"/></p>
<h2 id="virtual-media-manager-additional-buttons">Virtual Media Manager additional buttons</h2>
<p>The Virtual Media Manager has additional buttons that will allow you to perform additional actions.</p>
<p><img src="https://phpvirtualbox.github.io/images/advvmmbuttons.png"/></p>
<h3 id="new">New</h3>
<p>Opens the New Hard Disk wizard</p>
<h3 id="add">Add</h3>
<p>Allows you to add existing media to the global media registry</p>
<h3 id="add-iscsi">Add iSCSI</h3>
<p>Allows you to add an iSCSI disk to the global media registry</p>
<p><img src="https://phpvirtualbox.github.io/images/advvmmiscsi.png"/></p>
<p>The following options are available when adding an iSCSI disk:</p>
<table>
<thead>
<tr>
<th>Label</th>
<th>VBoxManage equivalent</th>
</tr>
</thead>
<tbody>
<tr>
<td>Server</td>
<td>VBoxManage storageattach --server</td>
</tr>
<tr>
<td>Port</td>
<td>VBoxManage storageattach --port</td>
</tr>
<tr>
<td>Internal Networking</td>
<td>VBoxManage storageattach --intnet</td>
</tr>
<tr>
<td>Target</td>
<td>VBoxManage storageattach --target</td>
</tr>
<tr>
<td>LUN</td>
<td>VBoxManage storageattach --lun</td>
</tr>
<tr>
<td>Encoded</td>
<td>VBoxManage storageattach --encodedlun</td>
</tr>
<tr>
<td>Username</td>
<td>VBoxManage storageattach --username</td>
</tr>
<tr>
<td>Password</td>
<td>VBoxManage storageattach --password</td>
</tr>
</tbody>
</table>
<p>See the VBoxManage documentation at <a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a> for more information on these settings.</p></div>
