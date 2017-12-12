<div class="markdown_content"><p><strong>Introduction</strong></p>
<p>*NOTE: This covers authentication within the phpVirtualBox application. If you are getting an error message that states "Error logging in to vboxwebsrv," please see the <a class="" href="https://github.com/phpvirtualbox/phpvirtualbox/wiki/Common-phpVirtualBox-Errors-and-Issues#error-logging-in-or-connecting-to-vboxwebsrv">Common Errors and Issues</a> wiki.</p>
<p>Authentication was introduced in phpVirtualBox 4.0-4. If you are using an older version, these features will not be available.</p>
<hr/>
<p><strong>Contents</strong></p>
<div class="toc">
<ul>
<li><a href="#logging-in-for-the-first-time">Logging in for the first time</a></li>
<li><a href="#configuring-users">Configuring Users</a><ul>
<li><a href="#access-levels">Access Levels</a></li>
</ul>
</li>
<li><a href="#password-recovery">Password Recovery</a></li>
<li><a href="#disabling-authentication">Disabling Authentication</a></li>
<li><a href="#multiple-server-considerations">Multiple Server Considerations</a></li>
</ul>
</div>
<hr/>
<h1 id="logging-in-for-the-first-time">Logging in for the first time</h1>
<p>When you navigate to phpVirtualBox, you may be presented with a Log in form.</p>
<p><img src="https://phpvirtualbox.github.io/images/authlogin.png"/></p>
<p>The default credentials are username: admin password: admin</p>
<p>Once logged in, you should change the default password through File -&gt; Change Password.</p>
<p><img src="https://phpvirtualbox.github.io/images/authchpassmenu.png"/></p>
<p>Using the change password form.</p>
<p><img src="https://phpvirtualbox.github.io/images/authchpass.png"/></p>
<h1 id="configuring-users">Configuring Users</h1>
<p>You may configure users in the File -&gt; Preferences -&gt; Users section of phpVirtualBox.</p>
<p><img src="https://phpvirtualbox.github.io/images/authusers.png"/></p>
<p>This section allows you to add, edit, and remove users. Access levels and authentication is very basic at the moment.</p>
<h2 id="access-levels">Access Levels</h2>
<p>phpVirtualBox essentially has two access levels. Admin users and non-admin users. Admin users have access to the Users section of phpVirtualBox and can add / edit / remove other users. They can also perform actions that change VM group memberships and manipulate VM groups (Rename / Group / Ungroup).</p>
<h1 id="password-recovery">Password Recovery</h1>
<p>You may reset the admin password by renaming the file <em>recovery.php-disabled</em> in phpVirtualBox's folder to <em>recovery.php</em> and navigating to it in your web browser. E.g. <a href="http://HOST-OR-IP/phpvirtualbox/recovery.php" rel="nofollow">http://HOST-OR-IP/phpvirtualbox/recovery.php</a></p>
<p>This page will present you with a simple form. Click on the <em>Recover</em> button to reset the admin user's password back to the default of <em>admin</em>. If you have removed the admin account, it will be recreated.</p>
<p>Once this is done, rename <em>recovery.php</em> back to <em>recovery.php-disabled</em>. phpVirtualBox will refuse to run while <em>recovery.php</em> exists. You may then log in with the default credentials of <em>admin</em> / <em>admin</em>.</p>
<h1 id="disabling-authentication">Disabling Authentication</h1>
<p>If you want to disable authentication in phpVirtualBox, add the following line to <em>config.php</em>:</p>
<div class="codehilite"><pre><span></span>var $noAuth = true;
</pre></div>


<p>Once this is done, no username / password will be required to access phpVirtualBox. Additionally, sections of phpVirtualBox pertaining to authentication (Change Password, Users, etc.) will not be visible.</p>
<h1 id="multiple-server-considerations">Multiple Server Considerations</h1>
<p>If you have phpVirtualBox configured to communicate with multiple !VirtualBox installations, please see the authentication notes provided in the <a class="" href="https://github.com/phpvirtualbox/phpvirtualbox/wiki/Multiple%20Server%20Configuration">Multiple Server Configuration wiki</a>.</p></div>
