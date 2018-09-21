<div class="markdown_content"><p><em>NOTE: If your problem is not fixed or mentioned on this Wiki page, please see <a class="" href="https://github.com/phpvirtualbox/phpvirtualbox/wiki/Common%20phpVirtualBox%20Errors%20and%20Issues/#my-error-message-or-issue-is-not-covered-here">this</a>.</em></p>
<hr/>
<p>Contents</p>
<div class="toc">
<ul>
<li><a href="#error-messages">Error Messages</a><ul>
<li><a href="#invalid-username-or-password">Invalid username or password</a></li>
<li><a href="#error-logging-in-or-connecting-to-vboxwebsrv">Error logging in or connecting to vboxwebsrv</a></li>
<li><a href="#could-not-connect-to-host">Could not connect to host</a></li>
<li><a href="#looks-like-we-got-no-xml-document">looks like we got no XML document</a></li>
<li><a href="#http-get-method-not-implemented">HTTP GET method not implemented</a></li>
<li><a href="#the-virtual-machine-vm-name-has-terminated-unexpectedly-during-startup">The virtual machine 'vm name' has terminated unexpectedly during startup</a></li>
<li><a href="#method-ns1xxxxxxxxxxx-not-implemented-method-name-or-namespace-not-recognized">Method 'ns1:xxxxxxxxxxx' not implemented: method name or namespace not recognized</a></li>
<li><a href="#function-xxxxxxxxxxxxxxxxx-is-not-a-valid-method-for-this-service">Function ("xxxxxxxxxxxxxxxxx") is not a valid method for this service</a></li>
<li><a href="#undefined-method-xxxxxxxxx">Undefined method: xxxxxxxxx</a></li>
</ul>
</li>
<li><a href="#issues">Issues</a><ul>
<li><a href="#empty-virtual-machine-list">Empty virtual machine list</a></li>
<li><a href="#preview-box-only-shows-vm-name-even-when-the-vm-is-running">Preview Box only shows VM name. Even when the VM is running.</a></li>
<li><a href="#console-tab-is-always-disabled">Console Tab is ALWAYS disabled</a></li>
<li><a href="#right-click-menu-is-displayed-under-context-menu-on-vm-details-tab-when-using-firefox">Right click menu is displayed under context menu on VM Details tab when using Firefox</a></li>
<li><a href="#vboxwebsrv-stops-after-some-time">vboxwebsrv stops after some time</a></li>
<li><a href="#memory-usage-of-vboxwebsrv-grows-constantly">memory usage of vboxwebsrv grows constantly</a></li>
<li><a href="#preview-box-is-black-and-vm-is-running-saved">Preview Box is Black and VM is running / saved</a></li>
<li><a href="#2d-3d-acceleration-options-do-not-exist">2D / 3D acceleration options do not exist</a></li>
</ul>
</li>
<li><a href="#my-error-message-or-issue-is-not-covered-here">My error message or issue is not covered here</a></li>
</ul>
</div>
<hr/>
<h1 id="error-messages">Error Messages</h1>
<h2 id="invalid-username-or-password">Invalid username or password</h2>
<p>The default username / password to use when logging in to phpVirtualBox is admin / admin. <br/>
See: <a href="https://github.com/phpvirtualbox/phpvirtualbox/wiki/Authentication-in-phpVirtualBox/">https://github.com/phpvirtualbox/phpvirtualbox/wiki/Authentication-in-phpVirtualBox</a></p>
<p>Some users have reported issues logging in if the PHP engine can't write to its session folder. It is impossible to cover all the possible PHP configurations here, so difficult to give direct guidance. I suggest you google <code>"php failed to write session data"</code> adding your operating system to the search.</p>
<h2 id="error-logging-in-or-connecting-to-vboxwebsrv">Error logging in or connecting to vboxwebsrv</h2>
<p><strong>NOTE: This is different than an Invalid username or password error.</strong></p>
<p>This typically indicates that the username and / or password is incorrect in config.php. These must be set to the system username / password of the user that administers your VirtualBox virtual machines.</p>
<p>Also, check to make sure that your vboxwebsrv is running and taking requests:<p>
<div class="codehilite"><pre><span></span>sudo netstat -tulpena | grep 18083</div>
<p><strong>If you have upgraded from VirtualBox 3.2.x and this was working before</strong>, you may have to run the following commands on your VirtualBox host:</p>
<div class="codehilite"><pre><span></span>VBoxManage setproperty vrdeauthlibrary default

VBoxManage setproperty websrvauthlibrary default
</pre></div>


<h2 id="could-not-connect-to-host">Could not connect to host</h2>
<p>This indicates that phpVirtualBox could not connect to the vboxwebsrv server. Either the <em>location</em> setting in config.php is wrong, <em>vboxwebsrv</em> is not running on the VirtualBox host, or SELinux is blocking access to vboxwebsrv. If you have SELinux enabled, see:</p>
<p><a href="https://github.com/phpvirtualbox/phpvirtualbox/wiki#selinux-considerations/">https://github.com/phpvirtualbox/phpvirtualbox/wiki#selinux-considerations</a></p>
<h2 id="looks-like-we-got-no-xml-document">looks like we got no XML document</h2>
<p>This message occurs when the $location setting in config.php is incorrect. The most common cause is that it is set to the location of phpVirtualBox rather than the SOAP URL of vboxwebsrv.</p>
<p>There are 2 locations involved. One is the URL that phpVirtualBox is accessible through, and the other is the URL through which phpVirtualBox communicates with vboxwebsrv. The $location setting in config.php needs to be set to the URL to vboxwebsrv.</p>
<p>The setting probably looks something like this:</p>
<div class="codehilite"><pre><span></span><span class="nt">var</span> <span class="o">$</span><span class="nt">location</span> <span class="o">=</span> <span class="s1">'http://localhost/phpvirtualbox/'</span><span class="o">;</span>
</pre></div>


<p>but needs to look like this:</p>
<div class="codehilite"><pre><span></span><span class="nt">var</span> <span class="o">$</span><span class="nt">location</span> <span class="o">=</span> <span class="s1">'http://127.0.0.1:18083/'</span><span class="o">;</span>
</pre></div>


<p>The URL through which phpVirtualBox is accessible does not need to be specified.</p>
<h2 id="http-get-method-not-implemented">HTTP GET method not implemented</h2>
<p>You are navigating to the $location setting in config.php. This is the URL through which phpVirtualBox communicates with VirtualBox's vboxwebsrv. Instead you need to navigate to phpVirtualBox's folder on your web server. Probably something like: <a href="http://localhost/phpvirtualbox" rel="nofollow">http://localhost/phpvirtualbox</a></p>
<h2 id="the-virtual-machine-vm-name-has-terminated-unexpectedly-during-startup">The virtual machine 'vm name' has terminated unexpectedly during startup</h2>
<p>This is usually an indication of some sort of misconfiguration of the VM. For instance you may have enabled "Enable VT-x/AMD-V" in the VM's configuration, but your processor does not support it (just an example). Unfortunately the only way to get the correct error message is to start the VM using another VirtualBox interface such as the VirtualBox GUI, VBoxManage, or VBoxHeadless. These should print a more descriptive error.</p>
<p>If the cause is not apparent through the error message, post the issue on the forums over at <a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a></p>
<h2 id="method-ns1xxxxxxxxxxx-not-implemented-method-name-or-namespace-not-recognized">Method 'ns1:xxxxxxxxxxx' not implemented: method name or namespace not recognized</h2>
<p>You are probably using a version of phpVirtualBox that is incompatible with your version of VirtualBox. </p>
<p>phpVirtualBox versioning is aligned with VirtualBox versioning in that the major and minor release numbers will maintain compatibility. phpVirtualBox 4.0-x will only be compatible with !VirtualBox 4.0.x. Regardless of what the latest x revision is. phpVirtualBox 4.1-x will only be compatible with VirtualBox 4.1.x. ..etc..</p>
<p>Download and install the correct version of phpVirtualBox, restart apache, and clear your web browser's cache.</p>
<h2 id="function-xxxxxxxxxxxxxxxxx-is-not-a-valid-method-for-this-service">Function ("xxxxxxxxxxxxxxxxx") is not a valid method for this service</h2>
<p>The short answer is to restart apache.</p>
<p>PHP caches the WSDL file for vboxwebsrv and is still using an older version. The default cache timeout set in php.ini is 1 day. Restarting apache should force PHP to refresh this file.</p>
<h2 id="undefined-method-xxxxxxxxx">Undefined method: xxxxxxxxx</h2>
<p>You have probably upgraded phpVirtualBox and not cleared your web browser's cache. The version in your web browser's cache does not match the version on the server. Clear your browser's cache and refresh the page.</p>
<h1 id="issues">Issues</h1>
<h2 id="empty-virtual-machine-list">Empty virtual machine list</h2>
<p>This is usually an indication that the username / password entered in config.php is not that of the user that administers your VirtualBox virtual machines.</p>
<h2 id="preview-box-only-shows-vm-name-even-when-the-vm-is-running">Preview Box only shows VM name. Even when the VM is running.</h2>
<p><strong><em>- or -</em></strong></p>
<h2 id="console-tab-is-always-disabled">Console Tab is ALWAYS disabled</h2>
<p>To enable screen shots and the Console tab, please install a VirtualBox extension pack that supports VRDE such as the Oracle VM VirtualBox Extension Pack found in the Downloads section of <a href="http://www.virtualbox.org" rel="nofollow">http://www.virtualbox.org</a></p>
<h2 id="right-click-menu-is-displayed-under-context-menu-on-vm-details-tab-when-using-firefox">Right click menu is displayed under context menu on VM Details tab when using Firefox</h2>
<p>In Firefox, click on the Tools menu -&gt; Options -&gt; Content -&gt; Advanced (next to Enable JavaScript), and enable the Disable or replace context menus option.</p>
<h2 id="vboxwebsrv-stops-after-some-time">vboxwebsrv stops after some time</h2>
<p><strong><em>- or -</em></strong> </p>
<h2 id="memory-usage-of-vboxwebsrv-grows-constantly">memory usage of vboxwebsrv grows constantly</h2>
<p>The fixes are easy, but the explanations around the fixes are long. The short answer is that this is a memory leak in pam_smbpass.so - a file used to sync samba passwords with system passwords. You have 2 options:</p>
<p><em>Disable authentication in vboxwebsrv.</em></p>
<p><em>-or-</em></p>
<p><em>Remove PAM references to this file so that it is not called for authentication</em></p>
<p>Each have their own gotchas. </p>
<ul>
<li>
<p>Disable authentication in vboxwebsrv - The end-result of this is that a username / password is no longer required to interact with VirtualBox through vboxwebsrv. If you are running vboxwebsrv bound to localhost or 127.0.0.1, and you are not worried about other people on your system mucking with vboxwebsrv, or you are on a protected network, then this is probably not an issue. To disable authentication in vboxwebsrv, run:</p>
<p>VBoxManage setproperty websrvauthlibrary null</p>
</li>
</ul>
<p>as the user that runs VirtualBox on your system. <em><em>NOTE: a username / password will still be required to log into phpVirtualBox.</em></em> If you don't like that option, read on..</p>
<ul>
<li>Remove pam_smbpass.so or PAM references to it - pam_smbpass is a PAM module that can be used on conforming systems to keep the smbpasswd (Samba password) database in sync with the UNIX password file. If you do not use samba (a software suite used to integrate <code>*</code>nix with Windows), removing the samba package from your system is the easiest choice. If you do use samba, but don't care to keep your your samba user database in sync with system passwords, you can comment out any references to pam_smbpass in /etc/pam.d/<code>*</code>. If you use samba AND want to keep your samba user database in sync with system passwords, your only choice is to disable vboxwebsrv authentication.</li>
</ul>
<h2 id="preview-box-is-black-and-vm-is-running-saved">Preview Box is Black and VM is running / saved</h2>
<p>The power or screen saver settings of the guest OS in the virtual machine is probably set to turn off the monitor or display a blank screen after a period of inactivity. Change this setting in the guest operating system of the virtual machine.</p>

<h2 id="phpvirtualbox-and-systemd-for-vm-manage-at-boot-and-shutdown">Use of systemd to start and stop vm and phpvirtualbox coexistence</h2>
<p>If you use systemd script to start and stop vm, in your script_name.service you need to use </p>
<div class="codehilite"><pre><span>sudo -u vboxuser /usr/bin/VBoxHeadless ...</span></div>
<p>instead to specify user and group as follow</p>
<div class="codehilite"><pre><span>[Service]
User=vboxuser
Group=vboxuser
</span></div>
<p>otherwise you risk to receive connection error.</p>
<h2 id="2d-3d-acceleration-options-do-not-exist">2D / 3D acceleration options do not exist</h2>
<p>These options have no effect in a headless environment (console via VRDE) and so are not displayed.</p>
<h1 id="my-error-message-or-issue-is-not-covered-here">My error message or issue is not covered here</h1>
<p>Chances are, you are not the first person to encounter a particular error message. Please search the forums at <a href="https://sourceforge.net/p/phpvirtualbox/discussion/">https://sourceforge.net/p/phpvirtualbox/discussion/</a> for your issue. If none is found, please post a new topic to the Help forum.</p></div>