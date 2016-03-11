**`***`DRAFT`***`**


# Introduction #

# Install Manually #
> ## Dependencies ##
> Tint2 depends on **cairo**, **pango**, **glib2**, **imlib2**, **xinerama** and **libx11**.

> Debian/Ubuntu:
> On **Ubuntu**, you install these dependencies using aptitude, for **Debian** apt-get:
```
   sudo aptitude install libcairo2-dev libpango1.0-dev libglib2.0-dev libimlib2-dev libxinerama-dev libx11-dev
```

> Gentoo:
```
   emerge -av cairo pango glib:2 imlib2 libXinerama libX11
```

After these dependencies have been installed,
> ## Getting the sources ##
```
   wget 'http://tint2.googlecode.com/files/tint2-<LATEST-RELEASE>.tar.gz'
   tar xvf tint2-<LATEST-RELEASE>.tar.gz
   cd tint2-<LATEST-RELEASE>
```

> ## Building ##
```
   ./configure
   make
```

> NOTE: You might append the following arguments to configure: **--prefix=/usr** **--sysconfdir=/etc**, see **--help** for further informations.


> ## Install ##
```
   su
   make install
```
> NOTE: For Ubuntu users, that means you type `sudo make install`
  1. If no errors ensure, HURRAY! , tint2 has been installed

# Running tint2 #

  * Execute `tint2` to start tint2
  * Or execute `tint2  -c  path_to_config_file`
  * [Configuring your tint2 config file](Configure.md)

> ## Autorun tint2 at startup ##
    * **Openbox3 users** : Add `tint2 &` in Openbox config file `$HOME/.config/openbox/autostart.sh`
    * **Ubuntu users** : Go to System > Preferences > Sessions . Click on add.
> > ![http://farm4.static.flickr.com/3043/3287368393_57101eabfa.jpg](http://farm4.static.flickr.com/3043/3287368393_57101eabfa.jpg)



# Any Problems #

  * If you run into any problems, please check out the [FAQ](FAQ.md).
  * Compiz users should especially check the [Compiz section of the FAQ](http://code.google.com/p/tint2/wiki/FAQ#Tint2_doesn't_work_on_compiz_correctly?)