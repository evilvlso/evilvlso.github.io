---
```Shell
#!/bin/bash
apt-get update
apt-get install -y libxss1 libappindicator1 libindicator7
wget https://dl.google.com/linux/direct/google-chrome-stable_current_amd64.deb
dpkg -i  google-chrome-stable_current_amd64.deb
```
### 如果报错了
`apt-get install -y -f ` 就OK👌了