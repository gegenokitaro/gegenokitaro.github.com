---
layout: default
title: Today's Screenshot
description: ""
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

## XMonad Again..

<p align="center"><img style="float: center" src=/img/today1.png /></p>

<br>
<br>
<br>

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
		--, ppCurrent		= wrap " ^fg(#ffffff)^r(42x16)^ib(1)^fg(#111111)^p(-38)" "^fg()"
		, ppVisible		= dzenColor (white) (black) . pad
		--, ppHidden		= wrap " ^fg(#505050)^r(42x16)^ib(1)^fg(#ffffff)^p(-38)" "^fg()"
		, ppHidden		= dzenColor (white) (black) . pad
		--, ppHiddenNoWindows	= wrap " ^fg(#505050)^r(42x16)^ib(1)^fg(#ffffff)^p(-38)" "^fg()"
		, ppHiddenNoWindows	= dzenColor (greys) (black) . pad
		, ppSep 		= " ^r(2x2) "
		, ppWsSep		= ""
		--, ppLayout		= \l -> ""
		, ppLayout		= dzenColor (white) (black) . pad
		--, ppTitle		= \t -> ""
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

