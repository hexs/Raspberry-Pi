https://www.raspberrypi.com/documentation/accessories/display.html

```
sudo nano /boot/firmware/config.txt
```

```
[all]
display_auto_detect=1
dtoverlay=vc4-kms-dsi-7inch
ignore_lcd=0
```

Use an on-screen keyboard
```
sudo apt install wvkbd
```

Using On-Screen Keyboard in Raspberry Pi OS
https://itsfoss.com/raspberry-pi-os-onscreen-keyboard/
```
sudo apt install matchbox-keyboard
```
