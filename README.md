# Houw-to-Add-GUI-on-Ubuntu-Server
<p>Deploy Ubuntu server from DigitalOcean dashboard, AWS Or GCloud...</p>
<p><img decoding="async" loading="lazy" class="size-full wp-image-136 aligncenter" src="https://technicalsahil.com/wp-content/uploads/2022/11/Create-Droplet.png" alt="" width="1100" height="531" srcset="https://technicalsahil.com/wp-content/uploads/2022/11/Create-Droplet.png 1100w, https://technicalsahil.com/wp-content/uploads/2022/11/Create-Droplet-600x290.png 600w, https://technicalsahil.com/wp-content/uploads/2022/11/Create-Droplet-300x145.png 300w, https://technicalsahil.com/wp-content/uploads/2022/11/Create-Droplet-1024x494.png 1024w, https://technicalsahil.com/wp-content/uploads/2022/11/Create-Droplet-768x371.png 768w" sizes="(max-width: 1100px) 100vw, 1100px" /></p>
<h3>Step 2</h3>
<p>Login via SSH. You can find the login detain when you click on the deployed sever as it showed in the image.</p>
<p><img decoding="async" loading="lazy" class="size-full wp-image-137 aligncenter" src="https://technicalsahil.com/wp-content/uploads/2022/11/Putty.png" alt="" width="667" height="665" srcset="https://technicalsahil.com/wp-content/uploads/2022/11/Putty.png 667w, https://technicalsahil.com/wp-content/uploads/2022/11/Putty-300x300.png 300w, https://technicalsahil.com/wp-content/uploads/2022/11/Putty-100x100.png 100w, https://technicalsahil.com/wp-content/uploads/2022/11/Putty-600x598.png 600w, https://technicalsahil.com/wp-content/uploads/2022/11/Putty-150x150.png 150w" sizes="(max-width: 667px) 100vw, 667px" /></p>
<h3>Step 3</h3>
<p>Update system packages</p>
<pre>sudo apt-get update &amp;&amp; sudo apt-get dist-upgrade -y</pre>
<h3>Step 4</h3>
<p>Install MATE desktop</p>
<pre>sudo apt-get install --no-install-recommends ubuntu-mate-core ubuntu-mate-desktop -y</pre>
<h3>Step 5</h3>
<p>Install XRDP</p>
<pre>sudo apt-get install mate-core mate-desktop-environment mate-notification-daemon xrdp -y</pre>
<h3>Step 6</h3>
<p>Add user</p>
<pre>adduser {yourusername}</pre>
<h3>Step 7</h3>
<p>Make that user admin</p>
<pre>usermod -aG admin {yourusername}</pre>
<h3>Step 8</h3>
<p>Make that user sudo</p>
<pre>usermod -aG sudo {yourusername}</pre>
<h3>Step 9</h3>
<p>Switch as new user</p>
<pre>su - {yourusername}</pre>
<h3>Step 10</h3>
<p>Connect to MATE desktop environment via XRDP</p>
<pre>echo mate-session&gt; ~/.xsession</pre>
<h3>Step 11</h3>
<p>Manually clone /etc/skel/ to /home/user directory.</p>
<pre>sudo cp /home/{yourusername}/.xsession /etc/skel</pre>
<h3>Step 12</h3>
<p>Restart XRDP service</p>
<pre>sudo service xrdp restart</pre>
<h3>Step 13</h3>
<p>Connect to remote desktop connection</p>
