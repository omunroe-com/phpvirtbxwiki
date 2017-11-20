<div class="markdown_content"><h1 id="enabling-custom-icons">Enabling Custom Icons</h1>
<p>You can enable custom icons per virtual machine in phpVirtualBox by adding:</p>
<div class="codehilite"><pre><span></span>var $enableCustomIcons = true;
</pre></div>


<p>to config.php.</p>
<h1 id="configuring-custom-icons">Configuring Custom Icons</h1>
<p>Once custom icons are enabled, you may edit a VM's icon by bringing up its settings.</p>
<p><img src="https://phpvirtualbox.github.io/images/customicon.png"/></p>
<p>The <em>Icon URL</em> setting may either bet set to a full URL such as:</p>
<div class="codehilite"><pre><span></span>http://www.virtualbox.org/graphics/vbox_logo2_gradient.png
</pre></div>


<p>or a relative URL like:</p>
<div class="codehilite"><pre><span></span>images/spinner.gif
</pre></div>