# Linux Workstation Setup

This isn't really a howto but rather something closer to a checklist to help spin up a linux workstation suitable for use as a developer's workstation.

## My System
I'm using:
- Macbook Pro: 2018, 15-inch
  [My system](https://support.apple.com/en-us/111949)
  Note: Mine has
  - 16 GB ram 2400 MHz DDR4
  - 2.2 GHz 6-Core Intel Core i7
  - Sequoia 15.7.7

I'm running my virtual environment using
- Professional Version 12.2.5 (20904517)

In order to get around the hard drive space limitation on this computer I'm running everything on a 1TB LaCie solid state external hard drive.

Not the fastest creature in the world but it does what I need for now.

## System

ubuntu 26.04 desktop

Note: I like my background to be a solid color rather than some design which distracts from my work.  Ubuntu no longer supports this through a GUI interface but you can set it up via bash terminal ....

1. Disable the current wallpaper image
```
gsettings set org.gnome.desktop.background picture-uri ""
gsettings set org.gnome.desktop.background picture-uri-dark ""
```

2. Ensure a solid color shading type
```
gsettings set org.gnome.desktop.background color-shading-type 'solid'
```
4. Set your desired color (replace with your hex code)
```
gsettings set org.gnome.desktop.background primary-color '#092230'
```

for a little help picking colors:
[google color picker](https://share.google/JAQIBlyElVjXcnYs7)

## Core Tools

- Python
- Ruby
- 

## Github
Setup a ssh key:

```
user@system:~$ ssh-keygen -t ed25519 -C "email@myaddress.com"
Generating public/private ed25519 key pair.
Enter file in which to save the key (/home/a542/.ssh/id_ed25519): 
Enter passphrase for "/home/username/.ssh/id_ed25519" (empty for no passphrase): 
Enter same passphrase again: 
Your identification has been saved in /home/username/.ssh/id_ed25519
Your public key has been saved in /home/username/.ssh/id_ed25519.pub
The key fingerprint is:
(redacted fingerprint) email@myaddress.com
The key's randomart image is:
+--[ED25519 256]--+
|                 |
 (stuff deleted)
|                 |
+----[SHA256]-----+
```
start the ssh agent
```
user@system:~$ eval "$(ssh-agent -s)"
Agent pid 6861
```

add the key to the ssh-agent
```
user@system:~$ ssh-add ~/.ssh/id_ed25519
Identity added: /home/user/.ssh/id_ed25519 (email@myaddress.com)
```

```
a542@SJH2-Ubuntu:~$ cat ~/.ssh/id_ed25519.pub
ssh-ed25519 -deleted- email@myaddress.com
```
