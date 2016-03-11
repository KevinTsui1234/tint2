**NOTE: tint2conf is still in development and not fully functional at the moment.**

#summary How to use theme switcher
#sidebar TOCArticles



The theme switcher makes it easier to manage different config files for tint2.

It'll give a preview of each config file with your current setting (backgroud, size of monitor, ...), and allow you to switch between tint2 configs.

For now, the theme switcher does not work if tint2 is running with the -c parameter.



# Running #

> Start the theme switcher with command `tint2conf`.

> On startup, the theme switcher show your current config file.

> ![http://img405.imageshack.us/img405/9373/ecran1.jpg](http://img405.imageshack.us/img405/9373/ecran1.jpg)


# Adding theme #

> The theme switcher uses an extension `.tint2rc` to identify config files.
  * Rename tint2 config file to have a `.tint2rc` extension
  * Open menu Theme > Add, select the config file and Add

> ![http://img52.imageshack.us/img52/4148/ecran2j.jpg](http://img52.imageshack.us/img52/4148/ecran2j.jpg)


# Switching theme #

> Double clicking on a panel will change to that tint2 config file and restart the panel.


# Editing theme #

> The `properties` button opens current theme in `tintwizard` config tool.

> When a config file is changed, you can update panel's preview with menu Edit > Refresh.
> When the background is changed, you can update panel's preview with menu Edit > Refresh all.

> if you want to edit theme with another program, open the file ~/.config/tint2/tint2confrc and changed the line 'cmd\_property'
```
 #---------------------------------------------
 # TINT2CONF CONFIG FILE
 default_theme = /home/thil77/.config/tint2/text_only_1.tint2rc
 cmd_property = gedit
 width = 746
 height = 587
```