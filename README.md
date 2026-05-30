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

My virtual environment
- Professional Version 12.2.5 (20904517)

In order to get around the hard drive space limitation on this computer I'm running everything on a 1TB LaCie solid state external hard drive.

Not the fastest creature in the world but it does what I need for now.

## System

ubuntu 26.04 desktop

Note: I like my background to be a solid color rather than some design which distracts from my work.  Ubuntu no longer supports this through a GUI interface but you can set it up via bash terminal ....

### Initial system update
```
sudo apt update
sudo apt upgrade
sudo apt install build-essential dkms
```
### Install git
`sudo apt install git`

### Install vscode
```
wget -O code-latest.deb 'https://code.visualstudio.com/sha/download?build=stable&os=linux-deb-x64
sudo apt install ./code-latest.deb
```
Install extensions
- Python
- Pylance
- Docker
- GitLens
- REST Client (for API testing)

### Install ruby
```
sudo apt install gcc make libssl-dev libreadline-dev zlib1g-dev libsqlite3-dev libyaml-de
git clone https://github.com/rbenv/rbenv.git ~/.rbenv
~/.rbenv/bin/rbenv init
```

refresh the terminal before proceeding `~/.bashrc`
```
mkdir -p "$(rbenv root)"/plugins
git clone https://github.com/rbenv/ruby-build.git "$(rbenv root)"/plugins/ruby-build
```

verify rbev installation 

`rbenv -v`

```
rbenv install 3.4.6 --verbose` note it takes some time to run the ruby installation
rbenv global 3.4.6
```

### Core developer tools
`sudo apt install -y python3 python3-pip python3-venv curl build-essential`

### Docker
```
sudo apt install -y ca-certificates curl gnupg lsb-release
sudo mkdir -p /etc/apt/keyrings
curl -fsSL https://download.docker.com/linux/ubuntu/gpg | sudo gpg --dearmor -o /etc/apt/keyrings/docker.gpg

echo \
  "deb [arch=$(dpkg --print-architecture) signed-by=/etc/apt/keyrings/docker.gpg] \
  https://download.docker.com/linux/ubuntu \
  $(lsb_release -cs) stable" | \
  sudo tee /etc/apt/sources.list.d/docker.list > /dev/null

sudo apt update
sudo apt install -y docker-ce docker-ce-cli containerd.io
```
allow docker to be run without using sudo
`sudo usermod -aG docker $USER`

### Python tools (PEP 668 “externally-managed-environment” protection now in effect)
pip can only install packages in a virtual environment.
```
sudo apt install pipx
pipx ensurepath
pipx install poetry
pipx install uv
```

### Postgres client tools
`sudo apt install -y postgresql-client`

### Check installations
Refresh the terminal
`source ~/.bashrc`

and run:
```
python3 --version
pip --version
docker --version
git --version
code --version
```

### To change ubuntu desktop to a solid color (no GUI support for this)
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


## Github - ssh key setup
On the linux system:
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
user@system:~$ cat ~/.ssh/id_ed25519.pub
ssh-ed25519 -deleted- email@myaddress.com
```

[Add SSH to github account](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/adding-a-new-ssh-key-to-your-github-account)

[Testing your SSH connection](https://docs.github.com/en/authentication/connecting-to-github-with-ssh/testing-your-ssh-connection)

# Project templates
## Fast API template
```
app/
  api/
  services/
  schemas/
  db/
  core/
tests/
.env.example
pyproject.toml (if using poetry)
```
