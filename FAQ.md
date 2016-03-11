

Frequently asked questions. Please add any extra tips to the comments.

# What is tint2? #
  * Tint2 is a panel/taskbar for modern X window managers like GNOME, KDE, XFCE, Openbox etc.

# Who is the developer of tint2 ? #
  * Main developers of tint2 are Thierry Lorthiois and Andreas Fink.

# tint2 does not show the systray/notification area #
  * Check your tint2rc to see if you have the systray enabled (`systray = 1` in tint2 0.11 or 'S' in `panel_items` in SVN ONLY)
  * Only one systray can run at a time. Run tint2 in a terminal. If you see 'tint2 : another systray is running', you have another systray running and tint2 cannot display its own.
    * Under Gnome 2, you can remove the Gnome systray with a right click on the separator before your systray in the panel -> remove.

# Why did some systray icons disappear from the panel? #
  * tint2 stops/restarts the systray on some events (such as switching the theme, or changing monitor resolution). Some systray icons do not implement the stop/restart of the systray and so disappear from the panel. You should report the problem to us and also to the developers of the applications that misbehave.

# Why don't some systray icons appear when you run tint2 in a KDE session? #
  * Some KDE applications use the KDE status notifier service to show system tray icons. If you disable this service (systemsettings -> Startup and Shutdown -> Service Manager -> uncheck "Status Notifier Manager") all the icons should appear normally in tint2.

# I want to disable the tint2 systray #
  * To disable the systray, just use `systray = 0` in your tint2rc.

# How to configure real transparency for xcompmgr #
  * tint2 autodetects your compositing manager and uses real transparency when possible. However, xcompmgr has a bug which prevents tint2 from detecting it.
  * If you want transparency with xcompmgr, download and apply to xcompmgr the patch from this bug report: [xcompmgr patch](http://bugs.freedesktop.org/show_bug.cgi?id=26090)

# Tint2 does not work on compiz correctly? #
  * All my tasks are on one desktop in compiz?
    * This is a known issue in compiz. Compiz does not support the 'virtual desktop' specification. In compiz, the 'desktop number' actually refers to a viewport instead of a 'virtual desktop'. So pager capabilities are not supported. See https://bugs.launchpad.net/ubuntu/+source/compiz/+bug/153322 or http://forum.compiz.org/viewtopic.php?f=86&t=11943 or  https://bugs.launchpad.net/ubuntu/+source/compiz/+bug/150690
  * Tint2 is being decorated with a window/ has a shadow /is not fully transparent
    * Open CompizConfig Settings manager -> Window Decorations Plugin
      * In the box for Decoration windows, put  `any & !type=dock`
      * In the box for Shadow windows, put  `any & !type=dock`
> > ![http://farm4.static.flickr.com/3311/3284967834_51f4d5cd22.jpg](http://farm4.static.flickr.com/3311/3284967834_51f4d5cd22.jpg)
  * Tint has ugly white streaks
    * Set a background for your desktop.

# I want to disable compiz shadow on Tint2 #
  * Run ccsm the compiz configuration tool. Go to Window Decorations. For both decoration and shadow windows, replace 'any' with 'any & !name=tint2'.

# Adding a 'show desktop' button #
  * tint2 does not implement a 'show desktop' button. But here is a way to get it. <br>
Create a file with following text<br>
<pre><code>#!/bin/sh<br>
if wmctrl -m | grep "mode: ON"; then<br>
exec wmctrl -k off<br>
else<br>
exec wmctrl -k on<br>
fi<br>
</code></pre>
Save it in /usr/bin/show_desktop.sh and make it executable.<br>
Install the package 'wmctrl'. And call the script in tint2rc config file.<br>
<pre><code>time1_format = %H:%M<br>
time1_font = sans 8<br>
time2_format = %A %d %B<br>
time2_font = sans 6<br>
clock_font_color = #ffffff 76<br>
clock_padding = 4 4<br>
clock_background_id = 0<br>
clock_lclick_command = show_desktop.sh<br>
</code></pre>
Then left click on the clock will do it.</li></ul>

Alternative (SVN ONLY): create a .desktop file with the above command and add it to the launcher.

# Task list is limited #
  * In your tint2rc file, check the value of `taskbar_mode`. If it is `multi_desktop`, tint2 shows multiple taskbars, one per desktop. Change the value to `single_desktop` if you want just one taskbar.

# How can I get 'pager like capability' ? #
  * In your tint2rc file, change the value of `taskbar_mode` to `multi_desktop`. This option will show one taskbar per desktop. So you can detect on which desktop an application is and which desktops are empty (or full). You can close an application whithout switching to the desktop. You can also drag and drop applications between desktops.

# I want to hide some tasks from the panel #
  * In the Openbox config file 'rc.xml' you can assign the property 'skip\_taskbar' to your window.

# The tint2 panel is blank #
  * A new option, called  `panel_items` has been added to the config file. This option defines the items tint2 will show and the order of those items(from left to right). Please define that in your tint2rc file. The format is shown below. The options are `L` for `Launcher`, `S` for the `Systray`, `T` for the `taskbar`, `C` for the `clock` and `B` for the `battery`.
```
panel_items = LTSBC 
```

# How to maximize windows over tint2 #
  * You can manage interaction between tint2 and windows with :
```
panel_layer = bottom/normal/top
strut_policy = follow_size/minimum/none
autohide_height = integer
```

> If you want maximized windows to never cover tint2:
```
panel_layer = top
strut_policy = follow_size
```
> If you want maximized windows to appear behind tint2:
```
panel_layer = top
strut_policy = none
```
> If you want maximized windows to appear behind tint2, but have 2 pixels free so you can use desktop action (right click, ...):
```
panel_layer = top
strut_policy = minimum
autohide_height = 2
```

# I get errors when I try to compile tint2 on my own #
  * Do you have all the dependencies installed? Please check [here](Install#Dependencies.md)

# I upgraded from tint to tint2 and I still have the old panel with its bugs #
  * The tint binary was renamed tint2 to avoid a conflict with another package. So your new tint2 startup command is **tint2**

# Tint2 doesn't show in Pekwm #
  * The problem is that pekwm defines by default edge borders, and does not allow a panel to get inside these edge borders. The config option is in `~/.pekwm/config` under `Screen/EdgeSize`. You can either disable the edge borders or set tint2 to a size where it does not enter these borders (i.e. play with `panel_size` and `panel_margin`).
  * Setting the margin to one pixel made it appear on my screen. With horizontal panel:
```
panel_size = 95% height
panel_margin = 0 1
```
  * With vertical panel:
```
panel_size = width 95%
panel_margin = 1 0
```

# Is there an IRC channel? #
  * Yes. There is now an irc channel, **#tint2** on [irc.freenode.net](irc://irc.freenode.net).
  * Just ask your question and stay there, because we are not always watching the channel ;)