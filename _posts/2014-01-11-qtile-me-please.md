---
layout: default
title: Qtile me, please
category: 
tags: []
---
{% include JB/setup %}
## Qtile me..
i'm using qtile now, and planning on using it over my xmonad. maybe not, i still love xmonad. but qtile definitely good at layouting. i really fall in love with its TreeTab layout. so, why don't you give it a try?

here is few tricks to mod qtile.
first, you have to know where is your qtile's conf. it's inside `.config/qtile/config.py`

The theme should reference these variables whenever needed.
    
### Workspaces with more edible names

It's a pain in the ass when you want to config qtile and know nothing about programming and shit, like myself. And i don't know from right to left how to change workspaces names like i do on monad or subtle. <br>
Open `config.py` and look for `group_names` section. 

    group_names = [
	   ("fuck", {}),
	   ("this", {}),
	   ("shit", {}),
	   ("i'm", {}),
	   ("done", {}),
    ]
    
    groups = [Group(name, **kwargs) for name, kwargs in group_names]
    
    for i, (name, kwargs) in enumerate(group_names, 1):
    # mod1 + letter of group = switch to group
    keys.append(
        Key([mod], str(i), lazy.group[name].toscreen())
    )

    # mod1 + shift + letter of group = switch to & move focused window to group
    keys.append(
        Key([mod, "shift"], str(i), lazy.window.togroup(name))
    )


And that's it. We can use `enumerate` to read the group names and arrange some shortcut keys to give us proper feel.
