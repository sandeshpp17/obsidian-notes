# What is forticlient openVPN.

FortiClient OpenVPN is a feature of FortiClient, a security solution provided by Fortinet. It allows users to establish secure VPN connections using the OpenVPN protocol. This is particularly useful for remote access to corporate networks, ensuring that data transmitted over the internet is encrypted and secure.

# How to connect with forticlient openVPN using cli

1. install forticlient openVPN using apt or nala
```bash
sudo apt install openfortivpn
```
or
```bash
sudo nala install openfortivpn
```

2. create new config file
```bash
sudo vi vpn/config.conf
```

```bash
host = <hostname or publci ip>
port = <vpn port>
username = <username>
password = <password>
trusted-cert = <ca encrypted path>
```
3. starting VPN session with config file
```
sudo openfortivpn --config vpn/config.conf  
```

4. start VPN session using CLI without config file
```bash
sudo openfortivpn <host/IP>:<Port> -u <username> -p <password>  --trusted-cert <ca path>
```
	To get the trusted ca use command without --trusted-cert argument in the command.
	If your username of password contains the # value then use "" for passing values

# How to connect with Tmux session 
### More at [[Tmux]]
1. connect with detached mode
```bash
tmux new -d -s vpn 'sudo openfortivpn --config vpn/config.conf'
```
OR
```bash
tmux new -d -s vpn 'sudo openfortivpn <host/IP>:<Port> -u <username> -p <password>  --trusted-cert <ca path>'
```
2. enter the tumx session
```
tmux attach -t vpn
```
3. enter the user password to allow connection and detach the terminal to keep running in background
```
Ctrl + b then d
```
