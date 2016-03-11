

The first time you run tint2, it will create the config file in `$HOME/.config/tint2/tint2rc` (This is true if you have done a clean install. Running tint2 in the source directory without doing 'make install' will not create the config file.)

You can also specify another file on the command line with the -c option.
e.g.: `tint2 -c $HOME/tint2.conf`

If you change the config file while tint2 is running, the command 'killall -SIGUSR1 tint2' will force tint2 to reload it.

All the configuration options supported in the config file are listed below. Please note that options marked as `SVN ONLY` are not yet supported in the stable version and might change until the next stable release.

Please try to respect as much as possible the order of the options as given below, as some are affected by it.

# Backgrounds and borders #

> The tint2 config file starts with the options defining background elements with borders:

  * `rounded = number_of_pixels` : the corner radius

  * `background_color = color opacity`
    * `color` is specified in hex RGB, e.g. #ff0000 is red
    * `opacity` varies from (0 to 100), where 0 is fully transparent, 100 is fully opaque

  * `border_width = width` : the border width in pixels

  * `border_color = color opacity`
    * `color` is specified in hex RGB, e.g. #ff0000 is red
    * `opacity` varies from (0 to 100), where 0 is fully transparent, 100 is fully opaque

> You can define as many backgrounds as you want. For example, the following config defines two backgrounds:
```
      rounded = 1
      border_width = 0
      background_color = #282828 100
      border_color = #000000 0

      rounded = 1
      border_width = 0
      background_color = #f6b655 90
      border_color = #cccccc 40
```
> tint2 automatically identifies each background with a number starting from 1 (1, 2, ...).
> Afterwards, you can apply a background to objects (panel, taskbar, task, clock, systray) using the background id, for example:
```
      panel_background_id = 1
      taskbar_background_id = 0
      task_background_id = 0
      task_active_background_id = 2
      systray_background_id = 0
      clock_background_id = 0
```
> Identifier 0 refers to a special background which is fully transparent, identifer 1 applied the first background defined in the config file etc.

# Panel #

  * `panel_items = LTSBC` (SVN ONLY) defines the items tint2 will show and the order of those items. Each letter refers to an item, defined as:
    * `L` shows the Launcher
    * `T` shows the Taskbar
    * `S` shows the Systray (also called notification area)
    * `B` shows the Battery status
    * `C` shows the Clock
> > For example, panel\_items = STC will show the systray, the taskbar and the clock (from left to right).

  * `panel_monitor = monitor (all, 1, 2, ...)` : Which monitor tint2 draws the panel on
    * The first monitor is `1`
    * Use `panel_monitor = all` to get a separate panel per monitor


> ![http://farm4.static.flickr.com/3425/3265475271_81e8ed56e0.jpg](http://farm4.static.flickr.com/3425/3265475271_81e8ed56e0.jpg)

  * `panel_position = vertical_position horizontal_position orientation`
    * `vertical_position` is one of: `bottom`, `top`, `center`
    * `horizontal_position` is one of: `left`, `right`, `center`
    * `orientation` is one of: `horizontal`, `vertical`

  * `panel_size = width height`
    * `width` and `height` can be specified without units (e.g. `123`) to mean pixels, or with `%` signs to mean percentages of the monitor size (e.g. `50%`). Use `100%` for full monitor width.

> Example:
```
      # The panel's width is 94% the size of the monitor, the height is 30 pixels:
      panel_size = 94% 30
```

  * `panel_margin = horizontal_margin vertical_margin` : The margins define the distance between the panel and the horizontal/vertical monitor edge. Use `0` to obtain a panel with the same size as the edge of the monitor (no margin).

> ![http://farm4.static.flickr.com/3438/3266303192_476a188196.jpg](http://farm4.static.flickr.com/3438/3266303192_476a188196.jpg)

  * `panel_padding = horizontal_padding vertical_padding spacing` : Please refer to the image below.

> ![http://farm4.static.flickr.com/3425/3265475271_81e8ed56e0.jpg](http://farm4.static.flickr.com/3425/3265475271_81e8ed56e0.jpg)

  * `font_shadow = boolean (0 or 1)`

  * `panel_background_id = integer` : Which background to use for the panel.

  * `wm_menu = boolean (0 or 1)` : Defines if tint2 forwards unhandled mouse events to your window manager. Useful for window managers such as openbox, which display the start menu if you right click on the desktop.

  * `panel_dock = boolean (0 or 1)` : Defines if tint2 is placed into the window manager's dock. For the openbox window manager it is advised to also use a modifier for the moveButton option, otherwise the mouse click is not forwarded to tint2 (in ~/.config/openbox/rc.xml).

  * `panel_layer = bottom/normal/top` : Places tint2 into the bottom/normal/top layer. This is helpful for specifying if the panel can be covered by other windows or not. The default is the bottom layer, but with real transparency normal or top layer may be a nice alternative.

  * `strut_policy = follow_size/minimum/none` : STRUTs are used by the window manager to decide the size of maximized windows.
    * `follow_size` means that the maximized windows always resize to have a common edge with tint2.
    * `minimum` means that the maximized windows always expand to have a common edge with the hidden panel. This is useful if the `autohide` option is enabled.
    * `none` means that the maximized windows use the full screen size.

  * `panel_window_name = string` : (SVN ONLY) Defines the name of the panel's window. Default: 'tint2'.

  * `disable_transparency = boolean (0 or 1)` : (SVN ONLY) Whether to disable transparency instead of detecting if it is supported. Useful on broken graphics stacks.

  * `autohide = boolean (0 or 1)` : Whether to enable panel hiding when the mouse cursor exists the panel.

  * `autohide_show_timeout = float` : Show timeout in seconds after the mouse cursor enters the panel. Use '.' as decimal separator.

  * `autohide_hide_timeout = float` : Hide timeout in seconds after the mouse cursor exits the panel. Use '.' as decimal separator.

  * `autohide_height = integer` : panel height (width for vertical panels) in hidden mode.

# Launcher (SVN Only) #
  * `launcher_icon_theme = name_of_theme` : Normally, tint2 will detect and use the icon theme of your desktop when you have an XSETTINGS manager running. Otherwise, the theme specified by this option is used.

  * `launcher_padding = horizontal_padding vertical_padding spacing`

  * `launcher_background_id = integer` : Defines which background to use.

  * `launcher_icon_size = integer` : The launcher icon size, in pixels.

  * `launcher_item_app = path_to_application` : Each launcher\_item\_app must be a full path to a .desktop file following the freedesktop.org [specification](http://standards.freedesktop.org/desktop-entry-spec/desktop-entry-spec-latest.html).

  * `launcher_icon_asb = alpha (0 to 100) saturation (-100 to 100) brightness (-100 to 100)` : Adjusts the icon color and transparency.

  * `launcher_tooltip = boolean (0 or 1)` : Whether to show tooltips for the launcher icons.


# Taskbar / Pager #

  * `taskbar_mode = single_desktop/multi_desktop`
    * `single_desktop` : Shows a normal taskbar listing the tasks running on the current virtual desktop (also known as 'workspace');
    * `multi_desktop` : Pager like capability. Shows multiple taskbars, one per virtual desktop, with which:
      * You can drag-and-drop tasks between virtual desktops;
      * You can switch between virtual desktops.

  * `taskbar_distribute_size = boolean (0 or 1)` : (SVN ONLY) If enabled, in multi-desktop mode distributes between taskbars the available size proportionally to the number of tasks. Default: disabled.

  * `taskbar_padding = horizontal_padding vertical_padding spacing`

> ![http://farm4.static.flickr.com/3521/3266303292_14d9b6b623.jpg](http://farm4.static.flickr.com/3521/3266303292_14d9b6b623.jpg)

  * `taskbar_background_id = integer` : Which background to use

  * `taskbar_active_background_id = integer` : Which background to use for the taskbar of the current virtual desktop.

  * `taskbar_name = boolean (0 or 1)` : (SVN ONLY) Whether to show the virtual desktop name in the taskbar.

  * `taskbar_name_padding = padding` : (SVN ONLY) Padding for the virtual desktop name.

  * `taskbar_name_background_id = integer` : (SVN ONLY) Which background to use for the desktop name.

  * `taskbar_name_font = [FAMILY-LIST] [STYLE-OPTIONS] [SIZE]` : (SVN ONLY) Font configuration for the desktop name.

  * `taskbar_name_font_color = color opacity (0 to 100)` : (SVN ONLY) (SVN ONLY) Font color for the desktop name.

  * `taskbar_name_active_background_id = integer` : (SVN ONLY) Which background to use for the name of the current desktop.

  * `taskbar_name_active_font_color = color opacity (0 to 100)` : (SVN ONLY) Font color for the name of the current desktop.

# Task #

The following options configure the task buttons in the taskbar:

  * `urgent_nb_of_blink = integer` : Number of blinks on 'get attention' events.

  * `task_icon = boolean (0 or 1)` : Whether to display the task icon.

  * `task_text = boolean (0 or 1)` : Whether to display the task text.

  * `task_centered = boolean (0 or 1)` : Whether the task text is centered.

  * `task_tooltip = boolean (0 or 1)` : Whether to show tooltips for tasks.

  * `task_maximum_size = width height`
    * `width` is used with horizontal panels to limit the size of the tasks. Use `width = 0` to get full taskbar width.
    * `height` is used with vertical panels.

  * `task_padding = horizontal_padding vertical_padding`

> ![http://farm4.static.flickr.com/3086/3265475337_262799ded3.jpg](http://farm4.static.flickr.com/3086/3265475337_262799ded3.jpg)

  * `task_font = [FAMILY-LIST] [STYLE-OPTIONS] [SIZE]`

  * `task_font_color = color opacity (0 to 100)`

  * `task_icon_asb = alpha (0 to 100) saturation (-100 to 100) brightness (-100 to 100)` : Adjust the task icon's color and transparency.

  * `task_background_id = integer` : Which background to use for non selected tasks

> For the next 3 options STATUS can be `active` / `iconified`  / `urgent`:
  * `task_STATUS_font_color = color opacity (0 to 100)`

  * `task_STATUS_icon_asb = alpha (0 to 100) saturation (-100 to 100) brightness (-100 to 100)` : Adjusts the task icon's color and transparency.

  * `task_STATUS_background_id = integer` : Which background to use for the task.

# Mouse actions for tasks #

> The possible mouse events are: `left, middle, right, scroll_up, scroll_down`.

> The possible mouse actions are: `none, close, toggle, iconify, shade, toggle_iconify, maximize_restore, desktop_left, desktop_right, next_task, prev_task`.

> Use `mouse_event = action` to customize mouse actions. Example:
```
  mouse_middle = none
  mouse_right = close
  mouse_scroll_up = toggle
  mouse_scroll_down = iconify
```

> The action semantics:
  * `close` : close the task
  * `toggle` : toggle the task
  * `iconify` : iconify (minimize) the task
  * `toggle_iconify` : toggle or iconify the task
  * `maximize_restore` : maximized or minimized the task
  * `shade` : shades (collapses) the task
  * `desktop_left` : send the task to the desktop on the left
  * `desktop_right` : send the task to the desktop on the right
  * `next_task` : send the focus to next task
  * `prev_task` : send the focus to previous task

If a mouse action is set to `none` and `wm_menu = 1` is set, the mouse event is forwarded to the window manager.

# System Tray #

  * `systray = boolean (0 or 1)` : Whether to show the system tray.

  * `systray_padding = horizontal_padding vertical_padding spacing`

  * `systray_background_id = integer` : Which background to use.

  * `systray_sort = ascending/descending/left2right/right2left` : Specifies the sorting order for the icons in the systray (note that with `left2right` or `right2left` the order can be different on panel restart).

  * `systray_icon_size = max_icon_size` : Set the maximum system tray icon size to `number`. Set to `0` for automatic icon sizing.

  * `systray_icon_asb = alpha (0 to 100) saturation (-100 to 100) brightness (-100 to 100)` : Adjust the systray icons color and transparency.

  * `systray_monitor = integer (1, 2, ...)` : (SVN ONLY) On which monitor to draw the systray. The first monitor is `1`.

# Clock #

  * `time1_format = %H:%M` : The format used by the first line of the clock.
    * `time1_format`, `time2_format` and `clock_tooltip` use the 'strftime' syntax. More info can be found here: http://www.manpagez.com/man/3/strftime/
    * To hide the clock, comment `time1_format` and `time2_format`.

  * `time1_timezone = :US/Hawaii`
    * `time1_timezone`, `time2_timezone` and `clock_tooltip_timezone` can be used to specify a timezone. If you do not specify a value the system-wide timezone is used. The timezones can usually be found in `/usr/share/zoneinfo`. If your timezones are in a different directory, you need to specify the absolute path, e.g. `time1_timezone = :/different/zoneinfo/dir/US/Hawaii` Always prepend the timezone with a ':'

  * `time1_font = [FAMILY-LIST] [STYLE-OPTIONS] [SIZE]`

  * `time2_format = %A %d %B`

  * `time2_timezone = :Europe/Berlin`

  * `time2_font = [FAMILY-LIST] [STYLE-OPTIONS] [SIZE]`

  * `clock_font_color = color opacity (0 to 100)`

  * `clock_padding = horizontal_padding vertical_padding`

  * `clock_background_id = integer` : Which background to use

  * `clock_tooltip = %a, %d. %b %Y` : Format for the clock's tooltip.

  * `clock_tooltip_timezone = :UTC`

  * `clock_lclick_command = text` : Command to execute on left click.

  * `clock_rclick_command = text` : Command to execute on right click.

# Tooltip #

  * `tooltip_padding = horizontal_padding vertical_padding`

  * `tooltip_show_timeout = float` : Delay to show the tooltip in seconds. Use '.' as decimal separator.

  * `tooltip_hide_timeout = float` : Delay to hide the tooltip in seconds. Use '.' as decimal separator.

  * `tooltip_background_id = integer` : Which background to use for tooltips. Note that with fake transparency the alpha channel and corner radius options are not respected.

  * `tooltip_font_color = color opacity  (0 to 100)`

  * `tooltip_font = [FAMILY-LIST] [STYLE-OPTIONS] [SIZE]`

# Battery #

  * `battery = boolean (0 or 1)` : Whether to enable the battery item.

  * `battery_hide = never/integer (0 to 100)` : At what battery percentage the battery item is hidden.

  * `battery_low_status = integer`: At what battery percentage the low command is executed.

  * `battery_low_cmd = notify-send "battery low"` : Command to execute when the battery is low.

  * `bat1_font = [FAMILY-LIST] [STYLE-OPTIONS] [SIZE]`

  * `bat2_font = [FAMILY-LIST] [STYLE-OPTIONS] [SIZE]`

  * `battery_font_color = color opacity (0 to 100)`

  * `battery_padding = horizontal_padding vertical_padding`

  * `battery_background_id = integer` : Which background to use for the battery.


# An example tint2rc #
```
#---------------------------------------------
# TINT2 CONFIG FILE
#---------------------------------------------

#---------------------------------------------
# BACKGROUND AND BORDER
#---------------------------------------------
rounded = 7
border_width = 2
background_color = #000000 60
border_color = #ffffff 18

rounded = 5
border_width = 0
background_color = #ffffff 40
border_color = #ffffff 50

rounded = 5
border_width = 0
background_color = #ffffff 18
border_color = #ffffff 70

#---------------------------------------------
# PANEL
#---------------------------------------------
panel_monitor = all
panel_position = bottom center
panel_size = 94% 30
panel_margin = 0 0
panel_padding = 7 0
font_shadow = 0
panel_background_id = 1
wm_menu = 0
panel_dock = 0
panel_layer = bottom

#---------------------------------------------
# TASKBAR
#---------------------------------------------
#taskbar_mode = multi_desktop
taskbar_mode = single_desktop
taskbar_padding = 2 3 2
taskbar_background_id = 0
#taskbar_active_background_id = 0

#---------------------------------------------
# TASKS
#---------------------------------------------
task_icon = 1
task_text = 1
task_maximum_size = 140 35
task_centered = 1
task_padding = 6 3
task_font = sans 7
task_font_color = #ffffff 70
task_background_id = 3
task_icon_asb = 100 0 0
# replace STATUS by 'urgent', 'active' or 'iconfied'
#task_STATUS_background_id = 2
#task_STATUS_font_color = #ffffff 85
#task_STATUS_icon_asb = 100 0 0
# example:
task_active_background_id = 2
task_active_font_color = #ffffff 85
task_active_icon_asb = 100 0 0
urgent_nb_of_blink = 8

#---------------------------------------------
# SYSTRAYBAR
#---------------------------------------------
systray = 1
systray_padding = 0 4 5
systray_background_id = 0
systray_sort = left2right
systray_icon_size = 0
systray_icon_asb = 100 0 0

#---------------------------------------------
# CLOCK
#---------------------------------------------
time1_format = %H:%M
time1_font = sans 8
time2_format = %A %d %B
time2_font = sans 6
clock_font_color = #ffffff 76
clock_padding = 1 0
clock_background_id = 0
#clock_lclick_command = xclock
clock_rclick_command = orage
#clock_tooltip = %A %d %B
#time1_timezone = :US/Hawaii
#time2_timezone = :Europe/Berlin
#clock_tooltip_timezone = :/usr/share/zoneinfo/Europe/Paris

#---------------------------------------------
# BATTERY
#---------------------------------------------
battery = 0
battery_hide = 98
battery_low_status = 10
battery_low_cmd = notify-send "battery low"
bat1_font = sans 8
bat2_font = sans 6
battery_font_color = #ffffff 76
battery_padding = 1 0
battery_background_id = 0

#---------------------------------------------
# TOOLTIP
#---------------------------------------------
tooltip = 0
tooltip_padding = 2 2
tooltip_show_timeout = 0.7
tooltip_hide_timeout = 0.3
tooltip_background_id = 1
tooltip_font_color = #OOOOOO 80
tooltip_font = sans 10

#---------------------------------------------
# MOUSE ACTION ON TASK
#---------------------------------------------
mouse_middle = none
mouse_right = close
mouse_scroll_up = toggle
mouse_scroll_down = iconify

#---------------------------------------------
# AUTOHIDE OPTIONS
#---------------------------------------------
autohide = 0
autohide_show_timeout = 0.3
autohide_hide_timeout = 2
autohide_height = 4
strut_policy = minimum
```