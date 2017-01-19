---
layout: post
title: Solarized + tmux + ls + bold text
---

How I got,
<i style="background:#002b36;padding-left:4px;padding-right:2px;margin-right:2px;">
<span style="color:#eee8d5;">S</span>
<span style="color:#b58900;">o</span>
<span style="color:#cb4b16;">l</span>
<span style="color:#dc322f;">a</span>
<span style="color:#d33682;">r</span>
<span style="color:#6c71c4;">i</span>
<span style="color:#268bd2;">z</span>
<span style="color:#2aa198;">e</span>
<span style="color:#859900;">d</span>
</i>, `tmux`, `ls`, and **bold text** to work together.

Running `ls` from a Solarized tmux session returns a bunch of gray directories and files,
instead of the distinguishable colors we would expect.

!["Bright" blue](http://i.imgur.com/FqQwFpK.png)

This is because `ls` uses ["bright"](https://en.wikipedia.org/wiki/ANSI_escape_code#Colors) colors for directories and certain files, but Solarized
has overriden these "bright" colors with its base colors.

But I don't want "bright" colors, I want **bold** text.  So I spent some time googling and
hacking on config files, and I eventually got what I wanted!  `ls` to print colored
directories and files with **bold text** 😀

As a preface, I honestly have no idea why this worked 😕

# My Setup

I've only tested this with my setup, so if it doesn't work for you, sorry ☹️ 

![Setup](http://i.imgur.com/g1nSihX.png)

# Solarized

No changes here, thankfully.

Just set my terminal's colors to the beautiful Solarized colors as instructed by [Ethan](http://ethanschoonover.com/solarized).

# tmux

You must be using tmux 2.2 or above.  I noticed this did not work on tmux 2.1.

```
$ tmux -V
tmux 2.2
```

My `TERM` environment variable is set to `xterm-256color` by default.  I'm unsure if that is
something terminator is doing or Fedora, but it is what it is.

In my `.tmux.conf` file, I've set the `default-terminal` option to `screen-256color`.

```
set -g default-terminal screen-256color
```

Finally, use the `-2` option when opening tmux to force tmux to assume the terminal uses 256 colors.

I created an alias for tmux which includes this

```
alias tm='tmux -2'
```

# Bold text

I created a `.dir_colors` file in my home directory using dircolors.

```
dircolors -p > ~/.dir_colors
```

This file defines all the colors codes `ls` should use when printing files and directories.

I then used the [ANSI SGR parameter code 38](https://en.wikipedia.org/wiki/ANSI_escape_code#CSI_codes) to specify colors from the extended foreground colors.

For example: From dircolors, the config to set directory colors, `DIR`, was set to `1;34`, which results in a bright(1) blue(34) color.

```
DIR 1;34
```

But, as I've mentioned, the Solarized "bright blue" is not actually blue, but a gray hue.

Using the `38;5` ANSI code, I was able to specify the ANSI 256(38) foreground(5) color blue(4), and set the font text to **bold**(1), NOT bright!

```
DIR 1;38;5;4
```

![Bold blue](http://i.imgur.com/kxQ6tcC.png)

And there you go!

You can find my `.dir_colors`, along with all my home directory config files on [GitHub](https://github.com/zachwhaley/dotfiles/).
