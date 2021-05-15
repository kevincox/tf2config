# My TF2 Config

This is a little configuration framework I wrote for TF2.  It includes a way
to have different settings schemes (for example, recording and playing) and a 
weapon system that allows you to bind arbitrary actions on weapon switching
(example, change viewmodel settings or keybindings).

## Setting it up.

Just clone the folder into `~/.local/share/Steam/steamapps/common/Team Fortress 2/tf/custom/` (substitute the correct TF2 directory on Windows) and add `'+alias k_todo exec m_playing'` to your TF2 command line (the quotes are important).  If you want to use a different mode just change `m_playing` to something else (like `m_recording`).

## Weapon Switching

As mentioned, my configs have a super fancy weapon switching scheme.  The only
caveat is that you can't use previous/next weapons as I didn't write logic to
figure out what weapon would be next.  Personally, I bind scroll up, scroll
down, and clicking the mouse wheel to weapon 1, 3 and 2 respectively.  If you
want this functionality feel free to add it and send a pull request.

### Binding the keys.

To use the system you need to bind the proper keys.  You should bind your keys
to call `k_slot1` to `k_slot10`.  This will switch the weapon and call the
appropriate callbacks.

	bind "1" "k_slot1"
	bind "2" "k_slot2"
	bind "3" "k_slot3"

### Callbacks.

There are a number of callbacks on weapon switch to let you change settings.

#### k_slot*_vm

A callback for settings the viewmodel settings.

	// No viewmodel for my secondary.
	alias k_slot2_vm "r_drawviewmodel 0"

If unset it calls `k_default_vm`.

#### k_slot*_fov

A callback for setting the fov.

	// I like my primary upside down.
	alias k_slot1_vm "viewmodel_fov -55; viewmodel_fov_demo -55"

If unset it calls `k_default_fov`.

#### k_slot*_cust

A callback for anything else.

If unset it calls `k_default_cust` (which defaults to doing nothing).

## Naming Scheme

The naming scheme of the files is a little arbitrary, it just keeps them a bit
organized.  Anything starting with `k_` is considered an *internal* file and
probably shouldn't be changed.  Anything starting with `m_` is a *mode*, or
something that is set on the command line.  This essentially becomes your new
`autoexec.cfg`.  Anything starting with `s_` is a class config file that only
gets used when playing that class. Anything that starts with a `c_` is a
*config* file and is something that is used by the user in their custom files.

Feel free to edit the `s_`, `m_` and `c_` files, the `s_` files must not be
deleted while `c_` and `m_` files that you are not using can be removed (with
the exception of `m_common.cfg` which is always used, so keep it).

## Customizing.

### Global Settings

For global settings you need to edit the `m_` file that you are using.  There
is also `m_common.cfg` which is always `exec`ed, no matter what your command line
`k_todo` is set to.  These are analogous to an `autoexec.cfg` in a plain
configuration with the advantage that it is easy to change which one gets used
(by modifying the command line).

### Class Settings

The per-class settings are in the `s_${class}.cfg` files.  They work about the
same as the regular class files work.

## Included config files.

The `c_*` files are random configs that I found useful.  Feel free to use them
or not.  They aren't required as part of the framework.

### c_comms

My personal settings for comms.  Not too exciting.

### c_nolockmovement

A simple script that binds the movement keys such that you will always be moving
provided you are pressing a WASD key.  This is opposed to the default where
pressing opposing keys causes a deadlock.  In the case of opposing keys pressed
at the same time the last pressed takes precedence.

### c_regen
A simple script that causes you to constantly regen health and ammo. Useful for
rocket jumping practice.
