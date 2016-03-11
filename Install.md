

# Introduction #

Tint2 is very easy to install. For several distributions, including Ubuntu and Debian, prebuilt packages are available.


# Install manually #
> ## Requirements ##
> Tint2 requires an [EWMH](http://en.wikipedia.org/wiki/Extended_Window_Manager_Hints) compatible Window manager and an UTF-8 system.

> ## Dependencies ##
> Tint2 depends on **cairo**, **pango**, **glib2**, **>=imlib2-1.4.2**, **libgtk2.0-dev**, **xinerama**, **libXrender**, **libXcomposite**, **libXdamage**, **libx11**, **>=libXrandr-1.3**.

> On **Ubuntu**, use this command :
```
   sudo aptitude install libcairo2-dev libpango1.0-dev libglib2.0-dev libimlib2-dev libgtk2.0-dev libxinerama-dev libx11-dev libxdamage-dev libxcomposite-dev libxrender-dev libxrandr-dev
```

> On **Debian**, use this command:
```
   apt-get install libcairo2-dev libpango1.0-dev libglib2.0-dev libimlib2-dev libgtk2.0-dev libxinerama-dev libx11-dev libxdamage-dev libxcomposite-dev libxrender-dev libxrandr-dev
```

> On **Gentoo**, use this command:
```
   emerge -av cairo pango glib:2 imlib2 gtk+ libXinerama libX11 libXdamage libXcomposite libXrender libXrandr
```

> After these dependencies have been installed, you must download the latest release and unpack the archive.

> ## Getting the sources ##
```
   wget 'http://tint2.googlecode.com/files/tint2-<LATEST-RELEASE>.tar.gz'
   tar xvf tint2-<LATEST-RELEASE>.tar.gz
```

> Open a terminal in the tint2 directory.

> ## Building (from version 0.11 upwards) ##
> Version 0.11 and the latest SVN version use cmake as build tool.
```
   cd tint2-<LATEST-RELEASE>
   mkdir build
   cd build
   cmake -DCMAKE_INSTALL_PREFIX=/usr ../
   make
```
> NOTE: See **cmake -L** for a list of possible variables which change building behaviour.<br>
<blockquote>NOTE: If you have errors in the cmake step, it can be helpful to delete the file CMakeCache.txt in your build directory. <br><br>
For better integration with xcompmgr, see <a href='http://code.google.com/p/tint2/wiki/FAQ#How_to_configure_real_transparency'>xcompmgr patch</a></blockquote>

<blockquote><h2>Building (version 0.10 and older)</h2>
<pre><code>   cd tint2-&lt;LATEST-RELEASE&gt;<br>
   ./configure --prefix=/usr --sysconfdir=/etc<br>
   make<br>
</code></pre>
NOTE: see <b>./configure --help</b> for further informations.<br> <br></blockquote>

<blockquote><h2>Install</h2>
On <b>Ubuntu/Debian</b>,<br>
<pre><code>   sudo make install<br>
</code></pre></blockquote>

<blockquote>On <b>other systems</b>,<br>
<pre><code>   su<br>
   make install<br>
</code></pre></blockquote>

<blockquote>If no errors ensure, HURRAY! tint2 has been installed.</blockquote>


<h1>Install from pre-built tint2 packages</h1>

<blockquote><h2>For Debian or Ubuntu</h2>
<blockquote>Run:<br>
<pre><code>    sudo apt-get install tint2<br>
</code></pre></blockquote></blockquote>

<blockquote><h2>For Gentoo</h2>
<blockquote>Run:<br>
<pre><code>    su<br>
    emerge -av tint2<br>
</code></pre></blockquote></blockquote>

<blockquote><h2>For Arch Linux</h2>
<blockquote>Run:<br>
<pre><code>    sudo pacman -S tint2<br>
</code></pre></blockquote></blockquote>


<h1>Running</h1>

Tint2 provides two executables: the panel (named tint2) and a configurator (named tint2conf).<br>
<br>
<ul><li>Execute <code>tint2</code> to start the panel and <code>tint2conf</code> to start the configurator<br>
</li><li>Or execute <code>tint2  -c  path_to_config_file</code>
</li><li><a href='Configure.md'>Configuring your tint2 config file</a></li></ul>

On startup, tint2 detects if you have a composite manager to decide whether to uses real transparency or fake transparency.<br>
<br>
<br>
<blockquote><h2>Autorun tint2 in Openbox</h2>
<blockquote>Add the following command in config file <code>$HOME/.config/openbox/autostart.sh</code>
<pre><code>(sleep 2s &amp;&amp; tint2) &amp;<br>
</code></pre>
Restart Openbox.<br>
If you run a composite manager (xcompmgr, compiz, compton, ...), increase sleep time so that it finishes loading before tint2.</blockquote></blockquote>

<blockquote><h2>Autorun tint2 in Fluxbox</h2>
<blockquote>Remove fluxbox pannel and systray in ~/.fluxbox/init.<br>
Remove systemtray from the list of items in the line session.screen0.toolbar.tools.<br>
On the line session.screen0.toolbar.visible: true. Change true to false.<br>
Add (sleep 2s && tint2) & in ~/.fluxbox/startup<br>
Restart Fluxbox.<br></blockquote></blockquote>

<blockquote><h2>Autorun tint2 in Gnome 2</h2>
<blockquote>Go to System > Preferences > Sessions.<br>
Click on add.<br>
<img src='http://farm4.static.flickr.com/3043/3287368393_57101eabfa.jpg' /></blockquote></blockquote>



<h1>Any Problems</h1>

<ul><li>If you run into any problems, please check out the <a href='FAQ.md'>FAQ</a>.<br>
</li><li>Compiz users should especially check the <a href="http://code.google.com/p/tint2/wiki/FAQ#Tint2_doesn't_work_on_compiz_correctly?">Compiz section of the FAQ</a>