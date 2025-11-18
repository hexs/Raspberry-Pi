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
