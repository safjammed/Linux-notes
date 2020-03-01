# How to choose default editor in Linux ssh
Vim can be pain in the ass for many of us. Even now, i struggle to close that damn thing but some of the linux distros comes with it by default. Well fear no more, I've got you

#### I use nano btw 
```
sudo apt install -y nano
```
### Process
```
sudo update-alternatives --config editor
```
This command show you the text editors. The one you are using has the * in front. type in the number to change the default editor
