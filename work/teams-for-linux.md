
```
sudo nano /etc/apparmor.d/usr.bin.teams-for-linux
```

```
sudo apparmor_parser -r /etc/apparmor.d/usr.bin.teams-for-linux
```

```
teams-for-linux 
```

```
ll /opt/teams-for-linux/chrome-sandbox
```

```
ls -l /opt/teams-for-linux/chrome-sandbox
```

```
sudo chown root:root /opt/teams-for-linux/chrome-sandbox
```

```
sudo chmod 4755 /opt/teams-for-linux/chrome-sandbox
```

```
ls -l /opt/teams-for-linux/chrome-sandbox
```






```bash
cat /etc/apparmor.d/usr.bin.teams-for-linux
`#include <tunables/global>`

`profile usr.bin.teams-for-linux flags=(attach_disconnected, complain) {`
    `# Allow sys_admin capability`
    `capability sys_admin,`

    `# Allow basic filesystem access`
    `/usr/bin/teams-for-linux rix,`
    `/usr/bin/teams-for-linux/** rw,`

    `# Add any other necessary permissions here`
`}`

```