
## [Installation](https://github.com/yuezk/GlobalProtect-openconnect#installation)

### [Debian/Ubuntu based distributions](https://github.com/yuezk/GlobalProtect-openconnect#debianubuntu-based-distributions)

[ Install from PPA (Ubuntu 18.04 and later, except 24.04)](https://github.com/yuezk/GlobalProtect-openconnect#install-from-ppa-ubuntu-1804-and-later-except-2404)

```
sudo apt-get install gir1.2-gtk-3.0 gir1.2-webkit2-4.0
sudo add-apt-repository ppa:yuezk/globalprotect-openconnect
sudo apt-get update
sudo apt-get install globalprotect-openconnect
```

Note

For Linux Mint, you might need to import the GPG key with: `sudo apt-key adv --keyserver keyserver.ubuntu.com --recv-keys 7937C393082992E5D6E4A60453FC26B43838D761` if you encountered an error `gpg: keyserver receive failed: General error`.

#### **Ubuntu 24.04 and later**[](https://github.com/yuezk/GlobalProtect-openconnect#ubuntu-2404-and-later)

The `libwebkit2gtk-4.0-37` package was [removed](https://bugs.launchpad.net/ubuntu/+source/webkit2gtk/+bug/2061914) from its repo, before [the issue](https://github.com/yuezk/GlobalProtect-openconnect/issues/351) gets resolved, you need to install them manually:

```shell
wget http://launchpadlibrarian.net/704701349/libwebkit2gtk-4.0-37_2.43.3-1_amd64.deb
wget http://launchpadlibrarian.net/704701345/libjavascriptcoregtk-4.0-18_2.43.3-1_amd64.deb

sudo dpkg --install *.deb
```

And the latest package is not available in the PPA, you can follow the [Install from deb package](https://github.com/yuezk/GlobalProtect-openconnect#install-from-deb-package) section to install the latest package.

#### **Ubuntu 18.04**[](https://github.com/yuezk/GlobalProtect-openconnect#ubuntu-1804)

The latest package is not available in the PPA either, but you still needs to add the `ppa:yuezk/globalprotect-openconnect` repo beforehand to use the required `openconnect` package. Then you can follow the [Install from deb package](https://github.com/yuezk/GlobalProtect-openconnect#install-from-deb-package) section to install the latest package.

#### Install from deb package[](https://github.com/yuezk/GlobalProtect-openconnect#install-from-deb-package)

Download the latest deb package from [releases](https://github.com/yuezk/GlobalProtect-openconnect/releases) page. Then install it with `apt`:

```shell
sudo apt install --fix-broken globalprotect-openconnect_*.deb
```

# How to connect the paloalto with CLI in Linux

```bash
sudo gpclient --ignore-tls-errors connect <Gatewayip> --user <username>
```

# Stop VPN connection

1. Use ctrl + C to stop connection of VPN.
2. Use below command to kill all the connected process of VPN.
```bash
sudo kill -9 $(ps -aux | grep 'gpclient' | awk '{print $2}')
```

# How to connect with Tmux session 
More at [[Tmux]]
1. connect with detached mode
```bash
tmux new -d -s vpn 'sudo gpclient --ignore-tls-errors connect <Gatewayip> --user <username>'
```
2. enter the tumx session
```
tmux attach -t vpn
```
3. enter the user password to allow connection and detach the terminal to keep running in background
```
Ctrl + b then d
```
