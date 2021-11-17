# for_my_future_self
Since I've found myself again having too look for 'nvidia drivers', 'screen tearing', 'WHY?', I'm now registering most moves.

## Day one

First things I did after installing manjaro Xfce.

1 - Install the latest LTS kernel and remove the other I have no interest.

[About Kernel's](wiki.manjaro.org/index.php/Manjaro_Kernels)

2 - Screen tearing is reeeeally annoying, so check for xfwm solution  fisrt (then you blame nvidia, which will break lightdm and so on...)

For references take a look at:
[Xfwm](wiki.archlinux.org/title/Xfwm)

But basically:

```bash

#First try  to see if it solves the problem, if not, try another solution (good luck!)

$ xfwm4 --replace --vblank=glx &

#If it solves, do the following in order to save it

$  xfconf-query -c xfwm4 -p /general/vblank_mode -s glx

#PS: If it doesn't solve you should consider trying another composite manager

```

3 - Remember to install an AUR Helper  (usually YaY), base-devel (for building packages), git, chrome and code.


TO DO: INSTALL i3wm(-gaps), pywall, polybar, urxvt, ranger  AND PUSH THE CONFIG FILES
