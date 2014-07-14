---
layout: default
title: "I'm documenting what i've done"
description: ""
category: 
tags: []
---
{% include JB/setup %}

### I'm Documenting what i've done

With that said, this time it's xmonad again. yeah, i'm doing xmonad all over my free time. it's not like i have much free time, but, it is. i've a lot of free time and i don't know what to do. I hang around my monad over and over again, and you can see, below is my current xmonad setting. probably not the best but i'm not really dissapointed with this one.

![screen](/img/nganggur11.png)

if, by any chance, you want to make your monad looks like this, i will give some tuts, a step-by-step tuts to build a dissapointing-monad just like in picture above. Okay, here are the ingredients to make monad like that, and everything in this cooking-like tutorial is optional, you can change anything to suits your taste except the important part. 

	First, we need xmonad. I use both xmonad and xmonad-contrib.
	for terminal client, i use urxvt. you can use anything.
	panel, dzen2. those panel, in pink, is dzen2. i don't know how to do it besides using dzen2.
	music player, mpc + ncmpcpp. weechat, irc client. and so on.
	dmenu, for a launcher. so i can launch an app without much keybinding.
	
	summary:
	xmonad (xmonad-contrib) | dzen2 | urxvt | weechat | mpc + ncmpcpp (mpd) | dmenu
<br>
I will begin on costumizing some xmonad code. I have to code, in xmonad way, haskell. I don't know haskell that much, but with a little understanding, everything will be fine. First, make a monad directory at `~/.xmonad`. There, i will store my `xmonad.hs` and do `--recompile` to produce xmonad. From here, are we good?

Okay, move to the next point. I will work inside `~/.xmonad` directory for a while. I will make `xmonad.hs` for the base dough to make this monad-cake. First thing, i will add some `import` to the `xmonad.hs`.

{% highlight hs %}
import XMonad
import Control.Monad
import XMonad.Hooks.DynamicLog
import XMonad.Hooks.ManageDocks
import XMonad.Hooks.SetWMName

import XMonad.Util.Run (spawnPipe)
import XMonad.Util.EZConfig (additionalKeys, additionalMouseBindings)
import XMonad.Util.SpawnOnce
import XMonad.Util.Loggers

import qualified XMonad.StackSet as W
import qualified Data.Map as M
import GHC.IO.Handle.Types as H

import XMonad.Layout.Spacing
import XMonad.Layout.Fullscreen
import XMonad.Layout.NoBorders
import XMonad.Layout.ResizableTile

import XMonad.Actions.CycleWS (prevWS, nextWS)

import System.IO

{% endhighlight %}

Put those `import` inside the dough we just made. Just input them. I don't really know what those code means myself. So we're good, kay..? After make some imports, I will set the workspace names. Like you can see below, that was the workspace names, and in that name display, i will include some icon.

![monad workspace](/img/monad-ws.png)

see? there are some icons included in workspace name. I use dzen2 as panel, so i will input some `^i(...)` into the workspace name. My icons are stored in `/home/yotsuba/.xmonad/xbm/` so i will make a shortcut to call them. It will be a pain in the ass if i input them literally for each name on the workspaces.

{% highlight hs %}
-- lets just call the shortcut with 'i' kay --
i = " ^i(/home/yotsuba/.xmonad/xbm/"

myws :: [String]
myws = clickable $ [ i ++ "term.xbm) TERM"
		           , i ++ "cat.xbm) WEB"
		           , i ++ "edit2.xbm) INFO"
		           , i ++ "pacman2.xbm) FILE"
		           , i ++ "diskette.xbm) WORK"
		           ]
       where clickable l = [ "^ca(1,xdotool key super+" ++ show (n) ++ ")" ++ ws ++ "^ca()" |
			               (i,ws) <- zip [1..] l, let n = i ]

{% endhighlight %}
<br>
Okay? <br>
<br>
So that's how we make some workspace. Next, i will make some keybindings to make my life easier. In this keybinds, is like adding some spoon or fork to the cake. So we can eat the cake easily without dirtying our hands. But, adding spoon or fork is at the end of making a cake, right? Fuck you, this ain't no cake. This is `monad`.
{% highlight hs %}
-- lets just call this mkeys --
mkeys =	[ ((mod4Mask, xK_Return), spawn "urxvt")
	       , ((mod4Mask, xK_Left), prevWS)
	       , ((mod4Mask, xK_Right), nextWS)
	       , ((mod4Mask, xK_Up), sendMessage MirrorExpand)
	       , ((mod4Mask, xK_Down), sendMessage MirrorShrink)
	       , ((mod4Mask, xK_r), spawn "dmenu_run -b")
	       , ((mod4Mask .|. shiftMask, xK_r), spawn "killall dzen2 && xmonad --restart")
	       -- sound and others --
	       , ((mod4Mask .|. mod1Mask, xK_Up), spawn "amixer set Master 5%+")
	       , ((mod4Mask .|. mod1Mask, xK_Down), spawn "amixer set Master 5%-")
	       , ((0, xK_F9), spawn "mpc toggle")
	       , ((0, xK_F11), spawn "mpc prev")
	       , ((0, xK_F12), spawn "mpc next")
	       ]

{% endhighlight %}
<br>
I'm done with keybinds. I think that's all i need to make my life easier. If you look at the keybinds, there is `dmenu_run` amongs those code. Yes. it's `dmenu`. I included `dmenu` in those keybinds to make a good app launcher, because xmonad doesn't really have an embedded-launcher like awesome. Hmm, maybe.. because i don't really know myself.

i dont know whats wrong but this jekyll engine take a foolish act again. fuck
