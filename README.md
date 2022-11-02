# My private makedeb

## Using the repository of pre-compiled packages
```bash
name="sakaru-makedeb"
wget -qO - https://karunaratne.net/sakaru-makedeb/pgp-key.public | gpg --dearmor | sudo tee "/etc/apt/trusted.gpg.d/$name.gpg" 1> /dev/null
echo "deb https://karunaratne.net/sakaru-makedeb ./" | sudo tee /etc/apt/sources.list.d/$name.list
(echo "92749694f84f3cb20bfe1d43ed83df4392e1e717a9af61d7bd6daee63845f16a /etc/apt/trusted.gpg.d/$name.gpg" | sha256sum -c) && sudo apt update
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

## Rules
- Don't make packages with the same name as packages in the default Ubuntu repositories
- Prefer building packages from source
- If downloading a pre-compiled package, name the package with the "-bin" suffix
- If a first-party Ubuntu repository already exists, don't re-package it here without good reason
- Don't change the default configurations unless required
