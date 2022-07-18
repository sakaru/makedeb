# My private makedeb

Relies on [makedeb](https://www.makedeb.org/). Install that using:
```bash
wget -qO - 'https://proget.makedeb.org/debian-feeds/makedeb.pub' | gpg --dearmor | sudo tee /usr/share/keyrings/makedeb-archive-keyring.gpg 1> /dev/null
echo 'deb [signed-by=/usr/share/keyrings/makedeb-archive-keyring.gpg arch=all] https://proget.makedeb.org/ makedeb main' | sudo tee /etc/apt/sources.list.d/makedeb.list
sudo apt update
sudo apt install makedeb
```

Then to build a package:
```bash
cd <package>
makedeb
sudo dpkg -i <deb file>
```