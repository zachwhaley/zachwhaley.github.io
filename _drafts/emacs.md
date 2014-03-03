---
layout: post
title: Emacs
---

I've been using Vim for the past year and I've finally configured everything to my liking, so naturally I'm switching to Emacs.

A friend at work is a long time Emacs user and has been preaching to me the wonders of coding, compiling, and debugging your code all in one program (You know, like a real IDE).  So here I go.

## First, Get Emacs 24
```bash
sudo yum install emacs-24
```

## Second, download [Prelude](http://batsov.com/prelude/)
Prelude is the move-in-ready version of Emacs.  It comes with tons of stuff you'd want in a coding environment, and makes learning Emacs by using it much easier.

## Third, M-x
<kbd>M-x</kbd> means press <kbd>Alt</kbd>+<kbd>x</kbd> at the same time.

If there is anything you want to do in Emacs, like delete a character, but don't know the key mapping, press <kbd>M-x</kbd>.

<kbd>M-x</kbd> lets you find and run any Emacs command and then tells you the key combo.

## Fourth, C-g
<kbd>C-g</kbd> is <kbd>Ctrl</kbd>+<kbd>g</kbd>.  <kbd>C-g</kbd> is Emacs' cancel.

So if you're stuck in some fourth dimension of Emacs with no way out, start spamming <kbd>C-g</kbd> and you'll eventually return to normality.

## Finally, don't close Emacs

Emacs does take a long time to load, but luckily once you've opened it you don't really need to close it.  Emacs wraps just about everything from the compiler to your own shell (<kbd>C-x m</kbd>), and when used well can be your all-in-one programming tool.

## Oh yeah, Vim

As I said before I've been using Vim for about a year and I've come to appreciate the home row navigation, and honestly I think it's better than the Emacs navigation.  But if you're learning Emacs without a Vim bias, try to use Emacs as is.

Otherwise, make sure to get [evil](https://gitorious.org/evil/pages/Home).  Evil makes Emacs feel like Vim;  <kbd>h</kbd><kbd>j</kbd><kbd>k</kbd><kbd>l</kbd> works like Vim, <kbd>:</kbd> works like Vim, <kbd>Esc</kbd> works mostly like Vim, etc...

To install Evil: `M-x package-install RET evil RET`

If you didn't catch that:

1. Press <kbd>M-x</kbd>
2. Type *package-install* and hit enter
3. Type *evil* and hit enter

[done](http://xkcd.com/378/)
