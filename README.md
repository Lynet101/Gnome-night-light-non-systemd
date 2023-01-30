# Gnome-night-light-artix
Get gnome-night-light going on Openrc, S6, Runit and Dinit

This is litteraly just a guide, because it took me ages to figure out this was a thing, and i imagine there's probably others in the same situation.

Gnome uses a service called "colord" to operate nightlight. Now "colord" is of course a systemd service, which is why it doesn't work on other init systems.
But, like with so many other things, we have been blessed by the [init]-world collections. A custom colord version exists both in dinit-world, openrc-world, s6-world and runit-world, meaning it can just be installed through pacman with ```pacman -S colord-{init}``` for example ```pacman -S colord-openrc```

Now 'colord' might fail the first time you run ```rc-service colord start``` (dunno if the problem exists on other inits as well), but fear not. This happened to me as well, and the solution that worked was rather simple. Just run ```sudo (or doas) /usr/lib/colord``` once the daemon has succesfully ran for a couple of seconds, hit **Ctrl + C** and try to launch it with the init system again.

Once succesfully launched, you will have to logout and back in (restart gdm), and the nightlight will work just fine :)
