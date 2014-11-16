---
layout: default
title: "I'm documenting what i've done (WIP)"
category: 
tags: []
---

With that said, this time it's xmonad again. yeah, i'm doing xmonad all over my free time. it's not like i have much free time, but, it is. i've a lot of free time and i don't know what to do. I hang around my monad over and over again, and you can see, below is my current xmonad setting. probably not the best but i'm not really dissapointed with this one.

<br><br>
![screen](/img/nganggur11.png)
<br><br>
{% include JB/setup %}
if, by any chance, you want to make your monad looks like this, i will give some tuts, a step-by-step tuts to build a dissapointing-monad just like in picture above. Okay, here are the ingredients to make monad like that, and everything in this cooking-like tutorial is optional, you can change anything to suits your taste except the important part. 

	First, we need xmonad. I use both xmonad and xmonad-contrib.
	for terminal client, i use urxvt. you can use anything.
	panel, dzen2. those panel, in pink, is dzen2. i don't know how to do it besides using dzen2.
	music player, mpc + ncmpcpp. weechat, irc client. and so on.
	dmenu, for a launcher. so i can launch an app without much keybinding.
	compton, for compositing.
	
	summary:
	xmonad (xmonad-contrib) | dzen2 | urxvt | weechat | mpc + ncmpcpp (mpd) | dmenu | compton
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
<br><br>
![monad workspace](/img/monad-ws.png)
<br><br>
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
I'm done with keybinds. I think that's all i need to make my life easier. If you look at the keybinds, there is `dmenu_run` amongs those code. Yes. it's `dmenu`. I included `dmenu` in those keybinds to make a good app launcher, because xmonad doesn't really have an embedded-launcher like awesome. Hmm, maybe.. because i don't really know it myself.
<br><br>
The next thing is, to set the color in that workspace. I'll adjust the color. We can add as many colors to this section, maybe i'll add some, in case i want to change the color-theme. But in this case i'll go with white, black, grey, and pink.
{% highlight hs %}
-- color shortcut --
black = "#333333"
grey3 = "#EEEEEE"
white = "#FFFFFF"
pink1 = "#E38179"

{% endhighlight %} 
<br>
Done. Now we have some nice color set. Why grey3 and pink1? Because i like them 3 in 1. And what's left is to put that color set into the workspace. I'll make this section as clear as possible. So you can define your own color theme to suits your taste.
{% highlight hs %}
logBar h = do
	dynamicLogWithPP $ tryPP h
tryPP :: Handle -> PP
tryPP h = defaultPP
	{ ppOutput			= hPutStrLn h
	, ppCurrent			= dzenColor (white) (pink1) . pad
	, ppVisible			= dzenColor (black) (grey3) . pad
	, ppHidden			= dzenColor (black) (grey3) . pad
	, ppHiddenNoWindows	= dzenColor (grey1) (grey3) . pad
	, ppUrgent			= dzenColor (blue1) (grey3) . pad
	, ppWsSep				= ""
	, ppOrder				= \(ws:l:t:_) -> [ws]
	, ppSep				= "   ^r(4x4)   "
	, ppLayout			= dzenColor (black) (grey3) .
						  ( \t -> case t of
						  	  "Spacing 2 Tall"	-> " " ++ k ++ "tile.xbm)  tile 4"
						  )
	}
	where k = "^i(/home/yotsuba/.xmonad/ws/"


{% endhighlight %}
<br>
How to color, is simple. When you define `dzenColor (a) (b) . pad`, `a` means the foreground color alias the font and the icon color. And `b` means the background color, so it will be like the picture earlier which is pink.

`ppCurrent` = It's the color of current workspace we're on. If you select the workspace, it will be pink-colored.

`ppVisible` = It's the color of visible workspace. Actually we can hide the workspace, but i didn't.

`ppHidden` = It's the workspaces other than current.

`ppHiddenNoWindows` = Like `ppHidden` with no active window in that workspace, or i can say a blank workspace.

`ppUrgent` = Workspace that have urgency. 

`ppWsSep` = We can set the workspace separator, but i didn't set it and left it blank.

`ppOrder` = It's the order of this log. Actually we have 3 component which is `ws` as workspace, `l` as layouts, and `t` as title. Layouts is the layout of current workspace. And title is the title of current window. Like you can see, i only use the `ws`, so we can leave `l` and `t` alone for now. 

`ppSep` = It's for the separator between `ws`, `l`, and `t`. 

`ppLayout` = How the layouts should be displayed on screen. We can leave it just like that for now..
<br><br>

I'm almost done. What's left for `xmonad` dough is the main class. In xmonad main class, i will set some layouts so i can change my current workspace's layout to suits the needs. In the import section, i included some layouts that i will use here. That's enough for layouts, so i will begin.

{% highlight hs %}
myfn = "M+ 1m-9:Bold" -- this where i set the font for panel. --
-- layout --
res = ResizableTall 1 (2/100) (1/2) [] -- part of layouts --
ful = noBorders (fullscreenFull Full)
-- for the main class --
main = do
	panel  <- spawnPipe top -- this is the panel --
	panel2 <- spawnPipe "sh /home/yotsuba/.xmonad/script/kananatas.sh" -- "second" panel--
	xmonad $ defaultConfig
		{ manageHook = manageDocks <+> manageHook defaultConfig
		, layoutHook = avoidStruts (spacing 2 $ layoutHook defaultConfig ||| res ) ||| ful
		, modMask = mod4Mask
		, focusedBorderColor = "#ffffff"
		, normalBorderColor = "#ffffff"
		, borderWidth = 4
		, workspaces = myws
		, terminal = "urxvt"
		, startupHook = setWMName "LG3D" -- for netbeans sake, i change the name --
		, logHook = logBar panel
		} `additionalKeys` mkeys
		where top = "dzen2 -p -ta l -e 'button3=' -fn '" 
			        ++ myfn ++ "' -fg '" ++ black ++ "' -bg '" ++ grey3 ++ "' -w 400"
			        ++ " -h 22 "
{% endhighlight %}
<br>
I use dzen2 for the panel. And maybe you notice "second" panel in my config. That's the right-side panel. It looks like there's only one panel, actually there are two panels side by side. The left one is the `log` panel to show workspace and others from xmonad system, and the right one is the `complimentary` panel that can be used for anything. We actually can input anything, any information, or just some random text to that `complimentary` panel. In my screenshot above, i put `date` and my up-down speed. Interesting, eh..?

The main dish is ready to serve. Monad-cake can be used now, i hope it's delish. 
<br>
<br>
<br>
#### So we're done?


Nope. There's still a lot to make. Next we will proceed to the topping. By topping, i mean the `complimentary` panel. So, what do we have here..? Hmm.. let me see.. i have.. hmmm... Oh, i have `conky`. I don't use it often but i think i'm gonna use it here, for the topping. I think i can make something from this `conky`. Hmmm... maybe `upspeedf` and `downspeedf` from `conky` will do the trick. And `date` too, i think it will be great just for this two functions.

Okay, let's move to conky. What i'm trying to do is make an output from `conky` and pipe it to `dzen2`. Now, i will set the dzen2-script first. I'll move to `~/.xmonad/script/` and make the script for `complimentary` panel. It will be `kananatas.sh` because i've already set it like that in my monad config. Let's cook.

{% highlight sh %}
fn="M+ 1m-9:Bold"   #i set the same font like the main panel from xmonad
obg="#eeeeee"       #yay for background
ofg="#333333"       #yay for foreground

conky -c /home/yotsuba/.xmonad/script/okanan.conkyrc 
| dzen2 -p -ta r -x 400 -h 22 -w 966 -fn "$fn" -bg "$obg" -fg "$ofg"

{% endhighlight %}
<br>
`dzen2` have some functions, like `-x` to adjust the x axis position of `dzen2` and `-y` for the y axis. `-w` is for the width, `-h` for the height, `-fn` font, `-bg` background color, `-fg` foreground, and so on. You can always read them at dzen2 official page or it's github page.

If you see the script, i `conky`-ing the input for `dzen2`. That means, `conky` will produce the output and i'm piping it to `dzen2`. Okay, let's move to the `conky` config.

{% highlight sh %}
background no
out_to_console yes
out_to_x no
update_interval 0.5
total_run_times 0
use_spacer none

{% endhighlight %}
<br>
and now i will make the input.

{% highlight sh %}
TEXT
^fg(\#E38179)^i(/home/yotsuba/.xmonad/xbm/uparrow1.xbm)^fg() \
${upspeedf wlp6s0}  \
^fg(\#E38179)^i(/home/yotsuba/.xmonad/xbm/downarrow1.xbm)^fg() \
${downspeedf wlp6s0}  \
^bg(\#e38179)  \
^fg(\#ffffff)\
${exec date +"%a, %b-%d %H:%M" | tr '[:lower:]' '[:upper:]'}  \

{% endhighlight %}
<br>
Here is the result.
<br>
<br>
![monad-com](/img/monad-comp.png)
<br>
<br>

#### What's more?
<br>
i dont know whats wrong but this jekyll engine take a foolish act again. fuck
