### Here is a quick list of links, pointing to tutorials on important stuffs I want them done after I distrohopped

[Install Pipewire](https://pipewire-debian.github.io/pipewire-debian/)\
[Fix Slow Shutdown/Reboot w/KDE](https://redd.it/oq2aez)\
[Install Flatpak Development(For Steam etc)](https://launchpad.net/~flatpak/+archive/ubuntu/development)\
OpenSUSE: `sudo ln -s ../lib64/qt5/bin/qdbus /usr/bin/qdbus`: without this kde compact shutdown applet won't work.\
https://www.reddit.com/r/kde/comments/motlyc/script_to_apply_your_custom_breeze_colorscheme_to/ <- because inconsistency is ugly, also override GTK_THEME as Breeze\
For `xdg-settings`, set `default-web-broser` to `io.gitlab.librewolf-community.desktop`, also for http/https schemes\
https://gist.github.com/sorat0mo/d809d0928f5613e2d3fb7d13e904bd0d fix the ugly fonts

After installing `fcitx5`, set the following variables in `/etc/environment`:
```
GTK_IM_MODULE=fcitx5
QT_IM_MODULE=fcitx5
XMODIFIERS=@im=fcitx5
SDL_IM_MODULE=fcitx5
```
