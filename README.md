# My private makedeb

## Using the repository of pre-compiled packages
```bash
wget -qO - https://karunaratne.net/sakaru-makedeb/pgp-key.public | gpg --dearmor | sudo tee /etc/apt/trusted.gpg.d/sakaru-makedeb.gpg > /dev/null
echo 'deb https://karunaratne.net/sakaru-makedeb ./' > /etc/apt/sources.list.d/sakaru-makedeb.list
sudo apt update
```

Then test using something like `sudo apt install tfswitch`.

## Developing new packages
Relies on [makedeb](https://www.makedeb.org/). Install that using:
```bash
wget -qO - "https://proget.makedeb.org/debian-feeds/makedeb.pub" | gpg --dearmor | sudo tee /usr/share/keyrings/makedeb-archive-keyring.gpg 1> /dev/null
echo "deb [signed-by=/usr/share/keyrings/makedeb-archive-keyring.gpg arch=all] https://proget.makedeb.org makedeb main" | sudo tee /etc/apt/sources.list.d/makedeb.list 1> /dev/null
sudo apt update
sudo apt install makedeb
```

Then to build a package:
```bash
cd <package>
makedeb
sudo dpkg -i <deb file>
```
