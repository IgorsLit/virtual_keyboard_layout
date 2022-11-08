# Virtual Keyboard Layout

This repository contents is the virtual keyboard layout file and the buttons' images. The layout is program matchbox-keyboard configuration file. The data is in XML format. It is the 85 keys keyboard (Main, Functional Keys and NumPad) layout with 4 languages symbols (see image #1).

![img#1 85 keys keyboard](img/keyboard_85keys_small.png)


## Program

The **matchbox-keyboard** is the virtual (on screen) keyboard program for the Raspberry Pi.

The original program's repository is https://github.com/mwilliams03/matchbox-keyboard

## Virtual Keyboard setting up

Info: https://pimylifeup.com/raspberry-pi-on-screen-keyboard/


### Install

Launch the Terminal and input commands:

```
sudo apt-get update
sudo apt-get upgrade
sudo apt-get install matchbox-keyboard
```

Additional info: *how to run a command without hitting enter key*
https://unix.stackexchange.com/questions/52055/how-to-run-a-command-without-hitting-enter-key/52110#52110

y and Enter combination, copy and paste to the Terminal:
```
y-> "

"
```

### Lauch

1. Once you are on the desktop of your Raspberry Pi, click the icon in the top-left hand corner of the screen.
2. Hover over “Accessories”, this will bring up an additional menu.
3. Within this new menu, click “Keyboard” to launch the program (see image #2)

![img#2 Launch Virtual Keyboard](img/keyboard_launch.png)

### Keyboard launcher

1. Create new shell file. Input command in the Terminal:

```
sudo nano /usr/bin/toggle-keyboard.sh
```

Type text in text editor nano:

```
#!/bin/bash
PID="$(pidof matchbox-keyboard)"
if [  "$PID" != ""  ]; then
  kill $PID
else
  matchbox-keyboard &
fi
```

2. Change execution permisions. Input command in the Terminal:

```
sudo chmod +x /usr/bin/toggle-keyboard.sh
```

3. Create new desktop file in application directory. Input command in the Terminal:

```
sudo nano /usr/share/raspi-ui-overrides/applications/toggle-keyboard.desktop
```

Type text in text editor nano:

```
[Desktop Entry]
Name=Toggle Virtual Keyboard
Comment=Toggle Virtual Keyboard
Exec=/usr/bin/toggle-keyboard.sh
Type=Application
Icon=matchbox-keyboard.png
Categories=Panel;Utility;MB
X-MB-INPUT-MECHANISM=True
```

4. Copy the panel file to user configuration. Input command in the Terminal:
```
cp /etc/xdg/lxpanel/LXDE-pi/panels/panel /home/pi/.config/lxpanel/LXDE-pi/panels/panel
```

Edit this file. Input command in the Terminal: 

```
nano /home/pi/.config/lxpanel/LXDE-pi/panels/panel
```

Add text in the end of file. Type text in text editor nano:

```
Plugin {
  type=space
  Config {
    Size=2
  }
}
Plugin {
  type=launchbar
  Config {
    Button {
      id=toggle-keyboard.desktop
    }
  }
}
Plugin {
  type=space
  Config {
    Size=2
  }
}
```

5. Reboot system.
Input command in the Terminal: 

```
sudo reboot
```

After reboot you will see the Toggle Virtual Keyboard icon near the Clock (see image #3).

![img#3 Toggle Virtual Keyboard icon](img/keyboard_panel_icon.png) 

## Virtual Keyboard Layouts

### Change Layout

Info: https://stackoverflow.com/questions/70574505/how-to-change-the-default-matchbox-keyboard-layout

https://forums.raspberrypi.com/viewtopic.php?t=325579

https://forum.openmarine.net/showthread.php?tid=4070

https://forums.raspberrypi.com/viewtopic.php?t=113526

## Layot description

85 keys keyboard layout with 4 languages symbols
Main, Functional Keys and NumPad

Main
Latvian language symbols (mod2):

qwertyuiop

ŪūĒēČčŽžĶķ

asdfghjkl

ŠšĢģŅņĪī¸

zxcvbnm

ĀāĻļˆˋˇ

based on base-fragment-lv_LV.xml layout file
full path /usr/share/matchbox-keyboard/base-fragment-lv_LV.xml

Russian language symbols (mod3):

qwertyuiop{

йцукенгшщзх

asdfghjkl;'

фывапролджэ

zxcvbnm,.

ячсмитьбю

1234567890-

ЙЦУКЕНГШЩЗХ

BkspHomePgUp789÷

Ф   Ы   В   АПРО

\EndPgDn4

ЛД  Ж   Э

6×EnterDel123-Shift

ЯЧС    М  ИТЬБЮ

based on base-fragment-ru_RU.xml layout file
full path /usr/share/matchbox-keyboard/base-fragment-ru_RU.xml

Greek language symbols fragment is in NumPad keyboard (mod2)

NumPad:

01 23 4567 89 ÷×+=.   num pad mode

⁰1 23 4567 89 ρ×¯⁺~.  fn mode (mod1)

₀α βγ δΔθλ μω Ωπ₋₊→∫  lang1 mode (mod2)

∞en↓pd←5→ho↑pu≤≥_±≠√  Shift(Caps lock) mode en-end, pd-page down, ho-home, pu-page up

## Change locale
Info: https://forums.raspberrypi.com/viewtopic.php?t=49468

https://wiki.debian.org/Locale

1. sudo raspi-config
2. select Localisation options
3. select Locale 
4. in Package configuration check your country language and english packages
5. select your country as default
6. change /etc/locale/default to:
LANG=lv_LV.UTF-8
LANGUAGE=en_US.UTF-8
LC_ALL=lv_LV.UTF-8
or if you want to choose other settings run command:
locale
and copy other options to /etc/locale/default 
7. sudo locale-gen
8. sudo reboot 