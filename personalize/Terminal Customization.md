# Terminal Customization

I like my terminal to be like this :

```shell
uname@hostname:~
$
```

rather than this :

```shell
uname@hostname:~$
```

and also you can backup your data with this command :

```shell
dconf dump /org/gnome/terminal/ > ~/gnome_terminal_settings_backup.txt
```

Reset (wipe out) the settings before loading a new one (probably not really required):

```shell
dconf reset -f /org/gnome/terminal/
```

Load the saved settings:

```shell
dconf load /org/gnome/terminal/ < gnome_terminal_settings_backup.txt
```

# your entire dconf database

it is stored in the single file `~/.config/dconf/user` .

# My Setup

```plain
[legacy/profiles:]
default='b1dcc9dd-5262-4d8d-a863-c897e6d979b9'
list=['b1dcc9dd-5262-4d8d-a863-c897e6d979b9', 'adad0998-8247-48d8-a62b-6b5eb8f27dc9']

[legacy/profiles:/:adad0998-8247-48d8-a62b-6b5eb8f27dc9]
palette=['rgb(23,20,33)', 'rgb(192,28,40)', 'rgb(38,162,105)', 'rgb(162,115,76)', 'rgb(18,72,139)', 'rgb(163,71,186)', 'rgb(42,161,179)', 'rgb(208,207,204)', 'rgb(94,92,100)', 'rgb(246,97,81)', 'rgb(51,209,122)', 'rgb(233,173,12)', 'rgb(42,123,222)', 'rgb(192,97,203)', 'rgb(51,199,222)', 'rgb(255,255,255)']
use-theme-colors=true
visible-name='normal'

[legacy/profiles:/:b1dcc9dd-5262-4d8d-a863-c897e6d979b9]
audible-bell=true
background-color='rgb(0,1,26)'
background-transparency-percent=51
font='Monospace 14'
foreground-color='rgb(0,172,161)'
highlight-colors-set=false
palette=['rgb(23,20,33)', 'rgb(192,28,40)', 'rgb(38,162,105)', 'rgb(162,115,76)', 'rgb(0,85,190)', 'rgb(163,71,186)', 'rgb(42,161,179)', 'rgb(208,207,204)', 'rgb(94,92,100)', 'rgb(246,97,81)', 'rgb(51,209,122)', 'rgb(233,173,12)', 'rgb(42,123,222)', 'rgb(192,97,203)', 'rgb(51,199,222)', 'rgb(255,255,255)']
use-system-font=false
use-theme-colors=false
use-theme-transparency=true
use-transparent-background=false
visible-name='mahdic200'
```







