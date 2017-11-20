<div class="markdown_content"><p>The following is user-contributed documentation on how to run vboxwebsrv as a service in Windows 7 / 2008 +. I am unable to verify the validity of these instructions.</p>
<p>1) install VirtualBox</p>
<p>2) menu start --&gt; administrative tools --&gt; task scheduler</p>
<p>3) create a new task</p>
<p>4) put name and description. Under security option, click on "change user or group", <em>if needed to select the user VirtualBox is supposed to run as</em>. Than select "run whatever the user is log on or not" and check the box "hidden"</p>
<p>5) tab triggers --&gt; new --&gt; begin the task: At startup</p>
<p>6) tab Actions --&gt; new --&gt; Action : start a program<br/>
   Program Script : browse to find an select vboxwebsrv (should be in C:\Program Files\Oracle\VirtualBox)</p>
<p>7) DO NOT ADD ARGUMENTS</p>
<p>8) check tabs conditions and settings for custom choices</p>
<p>9) Also don't forget to make a directory junction. If you don't do this, all your VMs will be inaccessible.</p>
<p>Directory junction has to be created using this command (replace <a class="alink notfound" href="../username">[username]</a> with your user profile name)</p>
<div class="codehilite"><pre><span></span> C:\Windows\System32\config\systemprofile&gt;mklink /j .Virtualbox C:\Users\[username]\.VirtualBox
</pre></div>


<p>10) have fun, test rebooting your machine</p></div>