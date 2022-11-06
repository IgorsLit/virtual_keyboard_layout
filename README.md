# Virtual Keyboard Layout

This repository contents is the virtual keyboard layout file and the buttons' images. The layout is program matchbox-keyboard configuration file. The data is in XML format. It is the 85 keys keyboard (Main, Functional Keys and NumPad) layout with 4 languages symbols (img.#1).


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

###Lauch

1. Once you are on the desktop of your Raspberry Pi, click the icon in the top-left hand corner of the screen.
2. Hover over “Accessories”, this will bring up an additional menu.
3. Within this new menu, click “Keyboard” to launch the program (img.#2)

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

