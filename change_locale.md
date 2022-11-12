# Change locale
Info: *How to set local locale with english text?* https://forums.raspberrypi.com/viewtopic.php?t=49468

Run terminal. Input commands.

1. sudo raspi-config
2. select Localisation options

image #1
![img#1 Localisation options](img/chg_locale_01_localisation_options.png)

3. select Locale

image #2
![img#2 Locale](img/chg_locale_02_locale.png)


4. in Package configuration check english and your country language packages (e.g. lv_LV.)

image #3
![img#3 Package configuration en](img/chg_locale_03_english_package.png)


and

image #4
![img#4 Package configuration lv](img/chg_locale_04_latvian_package.png)


5. select your country as default

image #5
![img#5 Default locale](img/chg_locale_05_default_locale.png)

6. press Finish button

image #6
![img#6 Finish button](img/chg_locale_06_finish.png)


7. change /etc/default/locale to:

```
LANG=lv_LV.UTF-8
LANGUAGE=en_US.UTF-8
LC_ALL=lv_LV.UTF-8
```

image #7
![img#7 nano default locale](img/chg_locale_08_cmd_nano_default_locale.png)

image #8
![img#8 nano editor](img/chg_locale_09_nano_editor.png)

or if you want to choose other settings replace LC_ALL row with other rows. Run command:

```
locale
```

and copy other options into /etc/default/locale

image #9
![img#9 Command locale](img/chg_locale_07_cmd_locale.png)

Info: *Locale* https://wiki.debian.org/Locale

8. sudo locale-gen

image #10
![img#10 Command locale-gen](img/chg_locale_10_cmd_locale_gen.png)

image #11
![img#11 Generation complete](img/chg_locale_11_complete.png)

9. sudo reboot

image #12
![img#12 reboot](img/chg_locale_12_cmd_reboot.png)

EOF