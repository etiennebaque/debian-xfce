# Debian Xfce - Notes

Here's some help to troubleshoot a few issues that may occur after a fresh install of Debian Xfce
- [Videos shows horizontal tears, and the quality is not great](#video_tears)
- [Middle tap on touchpad is not working](#middle_tap)
- [How to make Qt apps match dark themes on Xfce?](#qt_dark)
- [Map Caps-lock key to Ctrl](#caps_ctrl)

### <a name='video_tears'></a>Videos show horizontal tears and their quality is not great

Create `/etc/X11/xorg.conf.d/20-intel.conf` (if your have an Intel graphic card) and add the following content in it:
```
Section "Device"
  Identifier  "Intel Graphics"
  Driver      "Intel"
  Option      "TearFree"    "true"
EndSection
```
You may need to turn off compositing ('Window manager tweaks' > 'Compositor').

### <a name="middle_tap"></a>Middle tap on touchpad is not working

Create `/etc/X11/xorg.conf.d/40-libinput.conf` and add the following content in it:
```
Section "InputClass"
        Identifier "libinput touchpad catchall"
        MatchIsTouchpad "on"
        MatchDevicePath "/dev/input/event*"
        Driver "libinput"
        Option "Tapping" "on"
EndSection
```

### <a name='qt_dark'></a>How to make Qt apps match dark themes on Xfce?

Open `~/.config/Trolltech.conf` and add the following lines
```
[Qt]
style=GTK+
```
Save and exit the file. Then run the following:
```
sudo apt-get install qt5-style-plugins
```
Finally, open `/etc/environment` and add this line:
```
QT_QPA_PLATFORMTHEME=gtk2
```   
(Source: https://www.youtube.com/watch?v=rP4DWu24ff0)
