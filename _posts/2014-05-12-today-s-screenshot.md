---
layout: default
title: Today was a good day
category:
tags: []
---
{% include JB/setup %}
<head>
	<title>Spoiler HTML code</title>
	<style type="text/css">
body,input
	{
	font-family:"Trebuchet ms",arial;font-size:0.9em;
	bgcolor:#000000;
	}
.spoiler
	{
	border:1px solid #ddd;
	padding:1px;
	}
.spoiler .inner
	{
	border:1px solid #eee;
	padding:1px;margin:3px;
	}
	</style>
	<script type="text/javascript">
function showSpoiler(obj)
	{
	var inner = obj.parentNode.getElementsByTagName("div")[0];
	if (inner.style.display == "none")
		inner.style.display = "";
	else
		inner.style.display = "none";
	}
	</script>
</head>
### Today's Idea
I was talking with my friends about altered dimension, devil, satan, and jinn (?spectral creatures, i guess?) and it's a nice topic i think.. 

My Teacher said, jinn, or devil, or any spectral creatures that appeared before any human eyes was a result of manifestation. Creatures like that, were actualy energies that pile up and became a 'hard material'. In my language, it's called "penampakan". And that manifestation is from our thought. It explains why many sightings all over the world takes different form. So we move from that talk to any sightings-talking. We talked about how my friend meet his grandma that was passed away a long time ago. He said, it's not his grandma, but a spectral creatures that look like his grandma. We came to a conclusion. There're 2 type of sightings that can occur related to any deceased person. Wether it's the person we knew or not. One, it's from memories that left before they're passed away. And the other is from that spectral creatures that made its manifestation from our thoughts. Ah.. my English isn't good, so i can't continue this babbling anymore.. well..
<br>
<br>

### XMonad Again..

Actually, i was going to add a spoiler on to my code, but it didn't work as it's intended to do, so i remove that spoiler. This post now contains my xmonad.hs code, so you can copy and paste it to your machine as well. 
<br>
<br>
<p align="center"><img style="float: center" src=/img/today1.png /></p>

<br>
And below is the code for my xmonad. Or you can download it [here](/assets/ge.xmonad.rar) for complete packages including some home made icons and scripts. Tell me if you have any difficulties implementing my config.<br>
<br>

{% highlight hs %}

import XMonad 
import Control.Monad 
import System.IO 
import XMonad.Hooks.DynamicLog 
import XMonad.Hooks.ManageDocks 
import XMonad.Hooks.SetWMName 

import XMonad.Util.Run (spawnPipe)
import XMonad.Util.EZConfig (additionalKeys)
import XMonad.Util.Loggers

import XMonad.Actions.CycleWS (prevWS, nextWS)

import XMonad.Layout.Spacing

ic = "^i(/home/yotsuba/.xmonad/symbol/"
place :: [String]
place = clickable $ [ ic++"mod-term.xbm)"
		    , ic++"mod-book.xbm)"
		    , ic++"mod-disk.xbm)"
		    , ic++"mod-home.xbm)"
		    , ic++"mod-ngap.xbm)" ]
	where clickable l = [ "^ca(1,xdotool key super+" ++ show (n) ++ ")" ++ ws ++ "^ca()" |
				(i,ws) <- zip [1..] l,
				 let n = i ]

muatulang = "xmonad --recompile && killall dzen2 && xmonad --restart"

skeys = [ ((mod4Mask .|. shiftMask, 	xK_r), 		spawn muatulang)
	, ((mod4Mask, 			xK_r),		spawn "dmenu_run -b")
	, ((mod4Mask, 			xK_Left), 	prevWS)
	, ((mod4Mask, 			xK_Right),	nextWS)
	]
	black = "#111111"
white = "#ffffff"
blues = "#7DC8C6"
greys = "#696969"

test h = do
	dynamicLogWithPP $ fuck h
fuck :: Handle -> PP
fuck h = defaultPP
	{ ppOutput		= hPutStrLn h
	, ppCurrent		= dzenColor (blues) (black) . pad
	, ppVisible		= dzenColor (white) (black) . pad
	, ppHidden		= dzenColor (white) (black) . pad
	, ppHiddenNoWindows	= dzenColor (greys) (black) . pad
	, ppSep 		= " ^r(2x2) "
	, ppWsSep		= ""
	, ppLayout		= dzenColor (white) (black) . pad
	, ppTitle		= dzenColor (white) (black) . pad
	}

main = do
	pan <- spawnPipe dzen2bar
	nap <- spawnPipe other
xmonad $ defaultConfig
	{ manageHook = manageDocks <+> manageHook defaultConfig
	, layoutHook = avoidStruts $ spacing 4 $ Tall 1 (3/10) (1/2) 
	, modMask = mod4Mask
	, workspaces = place
	, terminal = "urxvt"
	, startupHook = setWMName "LG3D"
	, logHook = test pan
	, borderWidth = 0
	} `additionalKeys` skeys
	where dzen2bar 	= "dzen2 -p -ta l -e 'button3=' -fn 'cure-9' -w 640 -h 18 -y 768"
      		other	= "sh /home/yotsuba/.xmonad/script/scientist.sh"
{% endhighlight %}
