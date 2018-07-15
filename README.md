# Click macros for using an Xbox 360 controller with the Citra 3DS emulator

This is a set of macros I wrote to click an emulated 3DS touchpad with Xbox 360 controller button presses. I used them while playing through Ocarina of Time 3D and Majora's Mask 3D. These worked well with the Zelda games on the 3DS, and I imagine they will carry over nicely to other 3DS games, too.

## Setup

To use these macros you're going to need to run your Xbox 360 controller with `xboxdrv`. If you don't have it, and you're on Ubuntu, do

```
sudo apt install xboxdrv
```

The macros are performed using `xdotool`. If you don't have it, and your on Ubuntu, do

```
sudo apt install xdotool
```

These macros might work out of the box, but likely you'll need to do some slight modifications to get them working on your end, as the settings will vary with how you like displaying your 3DS touchscreen relative to the 3DS main screen, what resolution your display runs at, and possibly other factors.

In the [click-scripts](click-scripts) directory are a bunch of shell scripts, each of which click a specific pixel on the screen. I have them configured to work with a screen resolution of 1920x1080 for the 3DS Zelda games, using the Citra "Large Screen" screen layout (shown below).

![](https://i.imgur.com/yDAOTfg.png)

If you're deviating from this setup at all you're going to need to modify these scripts. That's easy though. All you need to do is to get the pixel coordinates that you want to click with

```
xdotool getmouselocation
```

and then put these coordinates in the appropriate shell script.

To modify what click presses on the Xbox controller map to which click scripts, change [xboxdrv.config](xboxdrv.config). To see a list of available buttons to map to type

```
xboxdrv --help-button
```

## Usage

You need root privileges to run this. Here's the command:

```
sudo xboxdrv --detach-kernel-driver -c /path/to/xboxdrv.config --silent
```

## Improvements

- How the click presses work is that each shell script clicks *in* at a pixel coordinate, waits 50ms, then clicks *out*. I played around a bit to find what waiting period is most responsive. It's not perfect at 50ms (sometimes a button press won't register), but it failed so infrequently that it didn't bother me.

- Ideally this would have different scripts running for button *presses* and button *releases*: when a button is pressed in a 'click in' is registered at a pixel coordinate; when the button is released—and only then—does the 'click out' occur. This is nice with, for example, bow aiming in Zelda: hold the button to aim, release it to fire. This is apparently very difficult to set up with `xboxdrv`, however, so I gave up after awhile, and the scripts only run on button presses.
