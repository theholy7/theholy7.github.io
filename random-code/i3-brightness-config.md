# Configuring brightness keys in i3wm

I have a Dell XPS 13 9360, and I have just started using i3wm.
Installing Ubuntu and i3 was easy enough following the tutorial on i3wm's website.
One of the hard parts was getting the brightness keys to work.

Going around the web, most of the solutions offered involve using `xbacklight` to control the brightness
and binding it with the correct keys by copying the following snippet into the config file
(located in `~/.config/i3/config`):

```bash
# Screen brightness controls
# increase screen brightness
bindsym XF86MonBrightnessUp exec xbacklight -inc 20
# decrease screen brightness
bindsym XF86MonBrightnessDown exec xbacklight -dec 20
```

Initially, I didn't have `xbacklight` installed, and when I installed it running `xbacklight -dec 20` did nothing.
The only message I got was that `No outputs have backlight property`.

I found [this Stackoverflow question](https://askubuntu.com/questions/715306/xbacklight-no-outputs-have-backlight-property-no-sys-class-backlight-folder)
that detailed my problem, but the accepted answer of making a symbolic link just didn't work.
I was always getting `ln: failed to create symbolic link '/sys/class/backlight/brightness': Operation not permitted`.

Thankfully I found the answer in [this blogpost](https://cialu.net/brightness-control-not-work-i3wm/).

I installed `light` into `~/.light` and 
