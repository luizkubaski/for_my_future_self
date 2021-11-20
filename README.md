# for_my_future_self
Since I've found myself again having too look for 'nvidia drivers', 'screen tearing', 'WHY?', I'm now registering most moves.


## First steps

First things I did after installing manjaro Xfce.


#### Kernels

Install the latest LTS kernel and remove the other I have no interest.

[About Kernel's](wiki.manjaro.org/index.php/Manjaro_Kernels)

#### Screen tearing

Screen tearing is reeeeally annoying, so check for xfwm solution  fisrt (then you blame nvidia, which will break lightdm and so on...)

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

### Getting an AUR Helper

Remember to install an AUR Helper  (usually YaY), base-devel (for building packages), git, chrome and code.

#### Git


It's usefull to change the .bashrc file in order to show the git branch in terminal.  [Take a look here](https://www.shellhacks.com/show-git-branch-terminal-command-prompt/https://www.shellhacks.com/show-git-branch-terminal-command-prompt/)

It's the following steps:

```bash

# Print the following variable
$ echo $PS1

# The <output> will be something like \[ ... \]

# Then you open the .bashrc file and add

git_branch() {
  git branch 2> /dev/null | sed -e '/^[^*]/d' -e 's/* \(.*\)/(\1)/'
}  

export PS1="<output>\$(git_branch)\$ "

# PS: The most error messages were related with wrong spacing and missing parenthesis

# PS2: You can change the colors of the 'gitbranch' by adding ANSI escape codes like
#  \[\033[00;32m\]\$(git_branch)\[\033[00m\]


```

#### Keyboard layout

Take a look at the `.bashrc` file.


#### Ranger

[Ranger](https://wiki.archlinux.org/title/ranger) is a text-based file manager written in Python.

```bash

# Install ranger and a lot of packages for handling highlights,
# extensions preview and other things.
sudo pacman -Syu ranger highlight atool w3m mediainfo

# Then start ranger to create a config file and close with Q
ranger
Q

# Create a copy of the configuration file
ranger --copy-config=all

# If you want to change the configurations change the files in ~/.config/ranger 

```


#### FUCK ME
I have an Acer Aspire 5 (A515-51G) and it have a single combined audio jack.

**The task:** use a mic (Boya M1) with a TRRS jack.

***Manjaro:*** "Nope, can't do it"

**The solution:** use an audio splitter jack. 

If you, different from me, are lucky, you can try the following:

```bash

# Open a terminal and enter
cat /proc/asound/card*/codec* | grep Codec

```

 
It should output the audio Codec, e.g., "Codec: Realtek ALC255"

Then you go  to [this link](https://www.kernel.org/doc/html/latest/sound/hd-audio/models.html) and look for your respective codec, open/create the file in `/etc/modprobe.d/alsa-base.conf ` and add the following line:

```bash

# my codec  is alc255-acer, you should put yours

options snd-hda-intel model=alc255-acer,dell-headset-multi


```

and pray.

Why am I mad about this? Windows just show you a pop-up asking *"dude, wtf did you just input here? a mic? a headphone? tell me!"* and it works perfectly (in a windows way). How do I expect to bring someone to Linux if I cannot even setup a mic? 

#### urxvt (rxvt-unicode)

There is an awesome blog about urxvt and configuring it [here](https://addy-dclxvi.github.io/post/configuring-urxvt/).

No `/.urxvt` folder? Create one.

No `~/.Xresources`? c.r.e.a.t.e

Or just use this: `urxvt --help 2>&1| sed -n '/:  /s/^ */! URxvt*/gp' >> ~/.Xresources `

Search for how to install fonts, it'll be useful. I've downloaded [Iosevka](https://typeof.net/Iosevka/)

Remember to use `xrdb ~/.Xresources` to reload after changes.


###### TO-DO

**INSTALL:** i3wm(-gaps), pywall, polybar  AND PUSH THE CONFIG FILES
