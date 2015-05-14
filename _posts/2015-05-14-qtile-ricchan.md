---
layout: post
title: "Qtile, Ricchan!!"
category: 
tags: []
---
{% include JB/setup %}
For the love of god, I'm using qtile once again. It's cool. Simple. 

Here's a little review. What makes me choose qtile over others tiling manager? Well, I don't really know why I choose qtile either.. I just thought that qtile is alien to me since I don't use it for a long time. For that matter, I thought it will be hit and go, install and use. No more timesink wm where I spent most of the time tinkering with it and try to configure how it looks. For the most part, it's true. It comes with okay default look, so just use it and get shits done. Well.. 

Not long after that, I remembered the reason I use qtile for the first time is its TreeTab layout. So, I decided to look at its config and, maybe, try to tinker a bit. Just a bit. For TreeTab layout. But it's been a long time, so I need to check some documentations. First thing to do, is to visit its website, <a href="http://www.qtile.org">Qtile</a>, and read some documentations. Cool. So well written even for a computer illiterate like me. Not to mention qtile.org has awesome design and really sweet, also it's easy on the eyes. Long story short, I end up tinkering with my qtile's config and here is my qtile.
<br>
<br>

![qtile](/img/qtilenowaifu.png)

<br>
<br>
Actually, I use Gnome3 on daily basis. But since I got my memory broken and left me with just merely 2GB on 64bit machine, you know how terrible it is to run that memory-eater DE on my machine, I thought I have to switch to light environment. Usually, I would take xmonad, but not this time. Xmonad, Awesome, MonsterWM, and so on are timesink wm, for me. And I just installed a fresh Arch on this machine, so xmonad is a no no for me. Its haskell library is so goddamn huge and I hate that part of xmonad. How about any other wm? Let's say, Awesome WM. I'm not a fan of its behavior. It's just strange. dwm, MonsterWM, Spectrwm, FVWM, WMFS, and so on, they just, timesink wm. You just configure it once for all, they said.. I said, NO. I'm a migratory bird. I'm not satisfied with static environment. I need a change sometimes. And it's just a pain in the ass to configure so it can behave like I need. So, Qtile, I choose you!

I'd love to post how to configure qtile, but maybe later. Instead, I will make a little comparation between many WM (especially tiling wm) that I've been used. It's just my opinion, so the experience may varies from others perspective.
<br>
<br>

<table>
	<tr>
		<th style="width:20%">WM</th>
		<th style="width:40%">Pro</th>
		<th style="width:40%">Cons</th>
	</tr>
	<tr>
		<td><b>Xmonad</b></td>
		<td>
			Very customizable, indeed.<br>
			I love the way it behaves.<br>
			Can use many third party apps.
		</td>
		<td>
			Fucking HUGE library<br>
			Inconsistent as fuck in Arch repo<br>
			Ermm.. MUST use many third party apps to works well.
		</td>
	</tr>
	<tr>
		<td><b>AwesomeWM</b></td>
		<td>
			Very wide range of costumization.<br>
			Popular.<br>
			Has a lot of useful widgets.
		</td>
		<td>
			I fucking hate it.<br>
			Fucking Lua.<br>
			Too much configuration but still behave unnaturally.
		</td>
	</tr>
	<tr>
		<td><b>Qtile</b></td>
		<td>
			Just werk, I think.<br>
			Pretty much easy configuration.<br>
			Has TreeTab Layout!<br>
		</td>
		<td>
			Not very customizable, really.. <br>
			Not in the official repo (but I don't really care). <br>
			Unpopular as fuck.
		</td>
	</tr>
	<tr>
		<td><b>
			dwm derivatives<br>
			(catwm, franken, ...)<br>
			must-compile-kek</b>
		</td>
		<td>
			Muh Freedom.<br>
			You can make whatever you want (if you can). <br>
			Hardcore Masochist. (+)
		</td>
		<td>
			Too much hassle.<br>
			A pain in the ass.<br>
			Hardcore Masochist. (-)
		</td>
	</tr>
</table>

<br>
<br>

And, that's it. Before I go, let me dump my configuration here, in case I need it some other time.

{% highlight py %}
# Copyright (c) 2010 Aldo Cortesi
# Copyright (c) 2010, 2014 dequis
# Copyright (c) 2012 Randall Ma
# Copyright (c) 2012-2014 Tycho Andersen
# Copyright (c) 2012 Craig Barnes
# Copyright (c) 2013 horsik
# Copyright (c) 2013 Tao Sauvage
#
# Permission is hereby granted, free of charge, to any person obtaining a copy
# of this software and associated documentation files (the "Software"), to deal
# in the Software without restriction, including without limitation the rights
# to use, copy, modify, merge, publish, distribute, sublicense, and/or sell
# copies of the Software, and to permit persons to whom the Software is
# furnished to do so, subject to the following conditions:
#
# The above copyright notice and this permission notice shall be included in
# all copies or substantial portions of the Software.
#
# THE SOFTWARE IS PROVIDED "AS IS", WITHOUT WARRANTY OF ANY KIND, EXPRESS OR
# IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF MERCHANTABILITY,
# FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT. IN NO EVENT SHALL THE
# AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY CLAIM, DAMAGES OR OTHER
# LIABILITY, WHETHER IN AN ACTION OF CONTRACT, TORT OR OTHERWISE, ARISING FROM,
# OUT OF OR IN CONNECTION WITH THE SOFTWARE OR THE USE OR OTHER DEALINGS IN THE
# SOFTWARE.

from libqtile.config import Key, Screen, Group, Drag, Click, Match
from libqtile.command import lazy
from libqtile import layout, bar, widget
from libqtile.dgroups import simple_key_binder

mod = "mod4"

keys = [
    # Switch between windows in current stack pane
    Key(
        [mod], "k",
        lazy.layout.down()
    ),
    Key(
        [mod], "j",
        lazy.layout.up()
    ),

    # Move windows up or down in current stack
    Key(
        [mod, "control"], "k",
        lazy.layout.shuffle_down()
    ),
    Key(
        [mod, "control"], "j",
        lazy.layout.shuffle_up()
    ),

    # Switch window focus to other pane(s) of stack
    Key(
        [mod], "space",
        lazy.layout.next()
    ),

    Key(
        [mod], "Left",
        lazy.screen.prevgroup()
    ),
    
    Key(
        [mod], "Right",
        lazy.screen.nextgroup()
    ),

    # Swap panes of split stack
    Key(
        [mod, "shift"], "space",
        lazy.layout.rotate()
    ),

    # Toggle between split and unsplit sides of stack.
    # Split = all windows displayed
    # Unsplit = 1 window displayed, like Max layout, but still with
    # multiple stack panes
    Key(
        [mod, "shift"], "Return",
        lazy.layout.toggle_split()
    ),
    Key([mod], "Return", lazy.spawn("urxvt")),

    # Toggle between different layouts as defined below
    Key([mod], "Tab", lazy.nextlayout()),
    Key([mod], "w", lazy.window.kill()),

    Key([mod, "control"], "r", lazy.restart()),
    Key([mod, "control"], "q", lazy.shutdown()),
    Key([mod], "r", lazy.spawncmd()),
]

groups = [
    Group(" urxvt "),
    Group(" web ", matches=[Match(wm_class=["Firefox"])]),
    Group(" blender "),
    Group(" inkscape "),
    Group(" gimp "),
    Group(" doc "),
]

dgroups_key_binder = simple_key_binder("mod4")


layouts = [
    layout.Max(),
    layout.MonadTall(
            name="xmonad tall",
            ratio=0.5,
            border_width=8,
            border_focus="#335260",
            border_normal="#69B2B8",
        ),
    layout.TreeTab(
            font='Liberation Sans',
            name="looking good",
            bg_color="#31363D",
            inactive_bg="151515",
            panel_width=100,
            margin_left=0,
            margin_y=0,
            sections=['TreeTab'],
            section_left=0,
            padding_x=4,
            active_bg="#69B2B8",
            rounded=False,
        ),
    layout.Stack(
            num_stacks=2,
            border_width=8,
            border_focus="#335260",
            border_normal="#69B2B8",
        ),
    layout.Floating(
            name="floating",
            border_width=8,
            border_focus="#335260",
            border_normal="#69B2B8",
        )
]

floating_layout = layout.Floating(
            name="floating",
            border_width=8,
            border_focus="#69B2B8",
            border_normal="#335260",
        )

widget_defaults = dict(
    font='Liberation Sans',
    fontsize=12,
    background="#974E69",
    markup=True,
)

screens = [
    Screen(
        bottom=bar.Bar(
            [
                widget.GroupBox(
                        borderwidth=0,
                        margin=0,
                        padding=6,
                        active="FFFFFF",
                        inactive="BABABA",
                        highlight_method="block",
                        this_current_screen_border="#335260",
                        invert_mouse_wheel=True,
                        rounded=False,
                    ),
                widget.Prompt(),
                widget.CurrentLayout(
                        background="#69B2B8",
                    ),
                widget.Spacer(),
                #widget.WindowName(),
                widget.TextBox("testing", name="default"),
                widget.Systray(),
                widget.Clock(format=' %I:%M %p '),
            ],
            24,
            background="#335260",
        ),
    ),
]

# Drag floating layouts.
mouse = [
    Drag([mod], "Button1", lazy.window.set_position_floating(),
        start=lazy.window.get_position()),
    Drag([mod], "Button3", lazy.window.set_size_floating(),
        start=lazy.window.get_size()),
    Click([mod], "Button2", lazy.window.bring_to_front())
]

dgroups_app_rules = []
main = None
follow_mouse_focus = True
bring_front_click = False
cursor_warp = False
auto_fullscreen = True

# XXX: Gasp! We're lying here. In fact, nobody really uses or cares about this
# string besides java UI toolkits; you can see several discussions on the
# mailing lists, github issues, and other WM documentation that suggest setting
# this string if your java app doesn't work correctly. We may as well just lie
# and say that we're a working one by default.
#
# We choose LG3D to maximize irony: it is a 3D non-reparenting WM written in
# java that happens to be on java's whitelist.
wmname = "LG3D"
{% endhighlight %}

<br>
<br>
<div id="centering">
a little joke featuring Ricchan.
<br>
<br>
<img src="/img/ricchan on qtile.jpg"></div>