# How to deal with fan speed control in arch

I saw a lot of posts talking about lm-sensors and pwdsomething. None of them worked for me.  
So here I'll be registering my steps with [nbfc-linux](https://github.com/nbfc-linux/nbfc-linux).

So, we first need to install it:

```bash
yay -S nbfc-linux
```

After that, I suggest looking for a preset config. Try filtering by the model of your laptop. In my case, I have an Acer Nitro 5 AN517-54 so one of the following would work:

```bash
# nbfc config --list | grep <laptop-model>
nbfc config --list | grep 'Acer Nitro'
```

Another option is to see what the utility recommends:

```bash
sudo nbfc config --recommend
```

Tip: if you are a nerd you can check the config file for each preset at `/usr/share/nbfc/configs/`.

So, for me, I picked the "Acer Nitro AN715-51" based on the specs of this laptop. After choosing a config set using:

```bash
# sudo nbfc config --set <model>
sudo nbfc config --set 'Acer Nitro AN715-51'
```

To start the process enter

```bash
sudo nbfc start
```

you can check that the service is running with `sudo nbfc status -a`. If you wish to enable the service at boot `sudo systemctl enable nbfc_service`.

And that's it, you are good to go.
