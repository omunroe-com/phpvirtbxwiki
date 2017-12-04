<div class="markdown_content"><p><strong>Introduction</strong></p>
<p>phpVirtualBox comes with authentication that allow it to use custom authentication mechanisms. This page lists each authentication module, how to enable it, and its settings.</p>
<hr/>
<p>Contents</p>
<div class="toc">
<ul>
<li><a href="#webauth">WebAuth</a></li>
<li><a href="#ldap">LDAP</a></li>
<li><a href="#active-directory-42-x-only">Active Directory (&gt;= 4.2-x only)</a><ul>
<li><a href="#restricting-access">Restricting Access</a><ul>
<li><a href="#containers">Containers</a></li>
<li><a href="#summary">Summary</a></li>
</ul>
</li>
</ul>
</li>
</ul>
</div>
<hr/>
<h1 id="webauth">WebAuth</h1>
<p>The WebAuth authentication module automatically logs in the user when .htaccess style authentication is being utilized by your web server. To enable this authentication method, add the following to config.php:</p>
<div class="codehilite"><pre><span></span>var $authLib = 'WebAuth';
</pre></div>


<p>By default, all users are admins in phpVirtualBox. You can specify a specific user as being an admin by adding the following to config.php:</p>
<div class="codehilite"><pre><span></span>var $authConfig = array('adminUser' =&gt; 'bob');
</pre></div>


<p>In the above case, 'bob' would be an admin in phpVirtualBox, while all other users would not.</p>
<h1 id="ldap">LDAP</h1>
<p>The LDAP authentication module provides a simple mechanism to authenticate against an LDAP server. To enable this authentication method, add the following to config.php:</p>
<div class="codehilite"><pre><span></span>var $authLib = 'LDAP';
var $authConfig = array(
   'host' =&gt; '127.0.0.1', // LDAP server IP
   'bind_dn' =&gt; 'uid=%s, ou=admins, dc=internal, dc=local', // %s will be replaced with login username
   'adminUser' =&gt; '' // leave blank to let all users be admins in phpVirtualBox or specify a username
);
</pre></div>


<p>Where values in the $authConfig array are appropriately set according to your LDAP environment. Contact your LDAP administrator for help with setting these values.</p>
<h1 id="active-directory-42-x-only">Active Directory (&gt;= 4.2-x only)</h1>
<p>The Active Directory authentication module allows phpVirtualBox to authenticate users against an Active Directory domain controller. For a very basic setup, add the following to config.php:</p>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>This configuration allows everyone in your Active Directory environment to log in and makes them all administrators in phpVirtualBox.</p>
<p>Each Active Directory implementation can provide varying levels of complexity. This authentication module aims to be flexible enough for any environment, but its configuration can be equally complex.</p>
<h2 id="restricting-access">Restricting Access</h2>
<p>The $authConfig items 'user_group' and 'admin_group' allow one to restrict access to phpVirtualBox. If user_group is set, only users that are members of this group (or an admin_group) will be able to log in. This can be specified in $authConfig in config.php as:</p>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'user_group' =&gt; 'Development Lab',
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>In this scenario, only users that are a member of the 'Development Lab' group can log in. Since no admin information is specified, all users would be admins in phpVirtualBox.</p>
<p>There are 2 mechanisms to specify one or more users as admins in phpVirtualBox. You can explicitly set one user to be an admin by setting the 'adminUser' item:</p>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'adminUser' =&gt; 'bob',
   'user_group' =&gt; 'Development Lab',
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>In this scenario, only users that are a member of the 'Development Lab' group can log in. The user 'bob' can log in (regardless of his group membership) and is an admin in phpVirtualBox.</p>
<p>You can also specify an entire group as administrators by setting the 'admin_group' item:</p>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'admin_group' =&gt; 'Domain Admins',
   'user_group' =&gt; 'Development Lab',
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>In this scenario, only users that are a member of the 'Development Lab' or 'Domain Admins' groups can log in. Only users in the 'Domain Admins' group are admins in phpVirtualBox.</p>
<h3 id="containers">Containers</h3>
<p>The default container searched is <em>CN=Users</em>. This is the "Users" folder in your Active Directory domain. To change the default container searched, you can specify the 'container' item in your $authConfig array:</p>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'container' =&gt; 'OU=Admins, OU=Engineering',
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>In this scenario, the organization unit <em>Engineering\Admins</em> is searched for users.</p>
<p><img src="https://phpvirtualbox.github.io/images/adou.png"/></p>
<h3 id="summary">Summary</h3>
<p>You can mix-and-match the container, admin_group, adminUser, and user_group in your configuration. It is important to remember:</p>
<ul>
<li>If no admin information is specified (via adminUser or admin_group), all users that can log in to phpVirtualBox will be administrators</li>
<li>Users identified as admins (via adminUser or admin_group) will be able to log in regardless of the user_group setting</li>
<li>To be able to log in to phpVirtualBox, users must be in the organizational unit specified by 'container' (defaults to CN=Users)</li>
</ul>
<p>Consider the following configuration scenarios and their effects:</p>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'admin_user' =&gt; 'james',
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>Anyone with an AD account can log in. Only 'james' is an admin in phpvirtualbox.</p>
<hr/>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'user_group' =&gt; 'Dev Lab',
   'admin_user' =&gt; 'susan'
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>Anyone in the Dev Lab group can log in. 'susan' is an admin in phpVirtualBox, but does not have to be a member of the Dev Lab group to log in.</p>
<hr/>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'admin_group' =&gt; 'vbox admins',
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>Anyone with an AD account can log in. Users in the 'vbox admins' group are admins in phpVirtualBox.\</p>
<hr/>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'user_group' =&gt; 'Dev Lab Users',
   'admin_group' =&gt; 'Dev Lab Admins',
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>Anyone in the Dev Lab Users group can log in. Users in Dev Lab Admins are admins in phpVirtualBox, but do not have to be a member of 'Dev Lab Users' to log in.</p>
<hr/>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>Anyone with an AD account can log in, and everyone will be an admin in phpVirtualBox.</p>
<hr/>
<div class="codehilite"><pre><span></span>var $authLib = 'ActiveDirectory';
var $authConfig = array(
   'container' =&gt; 'OU=Admins, OU=Engineering',
   'adminUser' =&gt; 'jason',
   'host' =&gt; '192.168.1.100', // domain controller IP
   'domain' =&gt; 'adtest.local' // active directory domain
);
</pre></div>


<p>Only the <em>Engineering\Admins</em> organizational unit will be searched for users. Any user in this container can log in to phpVirtualBox. Only jason is an admin in phpVirtualBox, but must also be found in the <em>Engineering\Admins</em> organizational unit.</p></div>
