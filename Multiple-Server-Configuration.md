<div class="markdown_content"><h1 id="basic-multiple-server-configuration-of-phpvirtualbox">Basic Multiple server configuration of phpVirtualBox</h1>
<p>Starting with phpVirtualBox 4-0, phpVirtualBox can be configured to interact with multiple VirtualBox installations. Provided that each is running its own vboxwebsrv instance. To do this, edit config.php in phpVirtualBox's folder and locate the following code:</p>
<div class="codehilite"><pre><span></span><span class="cm">/*</span>
<span class="cm">var $servers = array(</span>
<span class="cm">    array(</span>
<span class="cm">        'name' =&gt; 'London',</span>
<span class="cm">        'username' =&gt; 'user',</span>
<span class="cm">        'password' =&gt; 'pass',</span>
<span class="cm">        'location' =&gt; 'http://192.168.1.1:18083/'</span>
<span class="cm">    ),</span>
<span class="cm">    array(</span>
<span class="cm">        'name' =&gt; 'New York',</span>
<span class="cm">        'username' =&gt; 'user2',</span>
<span class="cm">        'password' =&gt; 'pass2',</span>
<span class="cm">        'location' =&gt; 'http://192.168.1.2:18083/'</span>
<span class="cm">    ),</span>
<span class="cm">);</span>
<span class="cm">*/</span><span class="w"></span>
</pre></div>


<p>Uncomment the code (remove the /<code>*</code> and <code>*</code>/) and edit the server values. An example config may look like this:</p>
<div class="codehilite"><pre><span></span>var $servers = array(
    array(
        'name' =&gt; 'London',
        'username' =&gt; 'vbox',
        'password' =&gt; 'secret1',
        'location' =&gt; 'http://10.32.32.4:18083/'
    ),
    array(
        'name' =&gt; 'New York',
        'username' =&gt; 'vboxadmin',
        'password' =&gt; 'secret2',
        'location' =&gt; 'http://10.32.45.2:18083/'
    ),
);
</pre></div>


<p>Note that the server names may be anything you wish. These should be descriptive to you.</p>
<p>Once this is done, you may change servers by clicking on the server name in the top item of the virtual machine list. The resulting menu will allow you to specify which server phpVirtualBox will communicate with.</p>
<p><img src="https://phpvirtualbox.github.io/images/phpvbmulti.png"/></p>
<h1 id="multiple-servers-and-authentication">Multiple servers and Authentication</h1>
<p>Basic user authentication was introduced in phpVirtualBox 4.0-4. phpVirtualBox stores its usernames and passwords in the VirtualBox server. This can only use ONE VirtualBox server for authentication. By default, it will use the first server in the $servers list. If you would like to change this, you can add an 'authMaster' property set to true to one of the servers. An example my look like:</p>
<div class="codehilite"><pre><span></span>var $servers = array(
    array(
        'name' =&gt; 'London',
        'username' =&gt; 'vbox',
        'password' =&gt; 'secret1',
        'location' =&gt; 'http://10.32.32.4:18083/'
    ),
    array(
        'name' =&gt; 'New York',
        'username' =&gt; 'vboxadmin',
        'password' =&gt; 'secret2',
        'location' =&gt; 'http://10.32.45.2:18083/',
                'authMaster' =&gt; true
    ),
);
</pre></div>


<p>One important implication of this is that phpVirtualBox will only be accessible if the authentication server is up - either the fist one in the list, or the one with the authMaster property. In a bind, you may turn off authentication by adding the following line to config.php:</p>
<div class="codehilite"><pre><span></span>var $noAuth = true;
</pre></div>


<h1 id="advanced-multiple-server-configuration">Advanced Multiple Server Configuration</h1>
<p>Any settings available in phpVirtualBox's config.php can be also be added to a server configuration. E.g.</p>
<div class="codehilite"><pre><span></span>var $servers = array(
    array(
        'name' =&gt; 'London',
        'username' =&gt; 'vbox',
        'password' =&gt; 'secret1',
        'location' =&gt; 'http://10.32.32.4:18083/',
                'consoleHost' =&gt; '10.32.32.4',
                'noPreview' =&gt; true,
                'browserRestrictFolders' =&gt; array('/home/vbox','/mnt/media')
    ),
    array(
        'name' =&gt; 'New York',
        'username' =&gt; 'vboxadmin',
        'password' =&gt; 'secret2',
        'location' =&gt; 'http://10.32.45.2:18083/',
                'consoleHost' =&gt; '10.32.45.2',
                'browserRestrictFolders' =&gt; array('/home/vboxadmin','/var/isos')
    ),
);
</pre></div>