---
layout: post
title: "Resurrect XMonad"
category: 
tags: []
---
{% include JB/setup %}
Today I decided to install XMonad once moar. It's the only tiling wm I've enjoyed for a long time. I put a simple and fast xmonad.hs for my new config and will tinker with it after I can login into bare minimum xmonad desktop. 

Configuring xmonad is rather easy for me. A lot more easier than most of tiling wm out there. In my opinion, haskell syntax is a lot more make sense than the others, for example, awesome wm with lua, qtile with python, or dwm which is C and is not dynamic at all. The only downside of xmonad for me is its huge library, and stand alone compiler, ghc. Size and compiler, isn't really a downside probably. That eliminates the only downside this wm has, so it's perfect. At least for me. This time, I used 3 main layouts for my xmonad. First is ResizableTall with WindowArranger, Fullscreen, and lastly Circle layout. <b>Cirlce is Elliptical, overlapping layout</b>. That's how it's described. Just take a look at picture below.

![xmonad-circle](/img/xmonad-circle.png)

That's Circle Layout.

<br><br><br>

#### Long Time No See

It's been a long time since I still actively mod my desktop. I installed urxvt, and it's still vanilla. Need to make .Xresources. Oh, and I'll parse dzen2 opt to .Xresources too, so it will kill two birds with one stone. 

Next step is to make a colorscheme. I'll make one with dark background and calm light color. I don't want purple, so I'll just replace it with another red and pink variant. Here's the colorscheme.

![colorscheme](/img/colorscheme.png)

Next is to configure mpd, ncmpcpp as well. Then weechat. 

It's easy to configure mpd and ncmpcpcpp. But for weechat, it's a hell lot of work. Weechat provides wide customization, that means there will be a lot of effort to produce a good custom weechat look and feel. I'll just make a minimal weechat look, disabled the bar and nicklist, custom prompt, and that's it. Will continue in future.

Here's the final screenshot.

![xmonad-megane](/img/xmonad-megane.png)

	xmonad
	urxvt, colorscheme is mentioned above
	running weechat and custom ncmpcpp

<br>
<br>

#### Update 2015 Nov 18

Somehow, my xmonad changed to pink themed. Pink is manly. Majin Buu is pink. Boros is said to be pink. Patrick is pink. In the old time, pink (or red) represent manliness, came from the color of blood, and in the other hand, blue represent calmness, which is for female. But nowadays, everythings are reversed. 

![xmonad-pink](/img/xmonad-pink.png)

#### In The Future

Won't post xmonad's step by step configuration, I've already done that multiple times, and there're too many xmonad tutorial over the internet, so I won't trouble myself with one. Any other than xmonad, I'll post it, depends on my level of laziness.

Ask me anything
