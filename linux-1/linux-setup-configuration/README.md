# Linux Setup & Config

## Security Reference

{% embed url="https://plusbryan.com/my-first-5-minutes-on-a-server-or-essential-security-for-linux-servers" %}

## **Update / Upgrade System**

```
apt-get update && apt-get upgrade -y
```

## Configure fail2ban

{% embed url="https://www.linode.com/docs/security/using-fail2ban-to-secure-your-server-a-tutorial/" %}

#### Install Fail2ban** &** email support

```
apt install fail2ban 
apt install sendmail
```

#### Create local copy of config fil**e**

```
cp /etc/fail2ban/fail2ban.conf /etc/fail2ban/fail2ban.local
```

#### Create local copy of jail file

```
cp /etc/fail2ban/jail.conf /etc/fail2ban/jail.local
```

#### Configure local jail settings

```
[sshd] 
enabled = true

ignoreip = 127.0.0.1/8 [plus known ips]
```

#### Configure mail

... tbd

## Secure Access to the Server

### Create Login User

```
> adduser kahuna # complete the prompts with throwaway password

> passwd -d kahuna # wipe password

> mkdir /home/kahuna/.ssh
> chmod 700 /home/kahuna/.ssh
```

### Create SSH Keys

```
> nano /home/kahuna/.ssh/authorized_keys
```

Add the contents of the id\_rsa.pub on your local machine and any other public keys that you want to have access to this server to this file.

```
> chmod 400 /home/kahuna/.ssh/authorized_keys
> chown kahuna:kahuna /home/kahuna -R
```

### Test Login User & Enable Sudo

Keep the current terminal (root user) open, and attempt SSH login (without password) in a separate terminal with the new Login User. &#x20;

```
> ssh kahuna@111.222.333.444 -p 22
```

If successful, go back to the root user session and add the new Login User to the **sudo** group.

```
> usermod -aG sudo kahuna
```

Enable all **sudo** group members to issue sudo commands without being prompted for a password.   As root, edit the /etc/sudoers file using the **visudo** editor.

```
> visudo

# Allow members of group sudo to execute any command
%sudo   ALL=(ALL:ALL) NOPASSWD:ALL
```

### Disable Root Login and Password Auth

Lock down SSH by disabling Root login and password authentication, and change the SSH port to something non-standard (not 22).  &#x20;

Be sure to open this new port up_ _in **UFW** firewall in the next step, before reloading the SSH configuration!

```
> nano /etc/ssh/sshd_config

Port 7777 # change from 22
LoginGraceTime 1m
PermitRootLogin no
PasswordAuthentication no
```

### Enable Firewall

Being careful not to lock ourselves out before completing the setup .. in the root user session, issue the following rules to UFW:

```
> ufw allow 80
> ufw allow 443
> ufw allow 7777 # the new SSH port
> ufw allow 22 # to keep our current session alive

> ufw enable
```

New restart SSH:

```
> service ssh restart
```

Now attempt an SSH login to port 7777 as the Login User in a separate terminal:

```
> ssh kahuna@xxx.xxx.xxx -p 7777
```

If successful, in the root user session, remove the rules for Port 22 from UFW and reload:

```
> ufw status numbered

     To                         Action      From
     --                         ------      ----
[ 1] 80                         ALLOW IN    Anywhere
[ 2] 443                        ALLOW IN    Anywhere
[ 3] 7777                       ALLOW IN    Anywhere
[ 4] 22                         ALLOW IN    Anywhere
[ 5] 80 (v6)                    ALLOW IN    Anywhere (v6)
[ 6] 443 (v6)                   ALLOW IN    Anywhere (v6)
[ 7] 7777 (v6)                  ALLOW IN    Anywhere (v6)
[ 8] 22 (v6)                    ALLOW IN    Anywhere (v6)

> ufw delete 8
> ufw delete 4
> ufw reload
```

Finally, log out and close the root user session.  From here on out we'll use the new Login User on our new SSH port instead, and apply **sudo **/ ** sudo su** for admin permissions when needed.

## Git

Install and configure git

* set name and email

`git config --global user.name "myname"`

`git config --global user.email "me@domain.com"`

* set github SSH key
* set global .gitignore [https://gist.github.com/octocat/9257657](https://gist.github.com/octocat/9257657)

`git config --global core.excludesfile ~/.gitignore_global`

## Tmux

set .tmux.conf [https://github.com/obzidi4n/tmux-conf](https://github.com/obzidi4n/tmux-conf)

install tmux plugin manager [https://github.com/tmux-plugins/tpm](https://github.com/tmux-plugins/tpm)

install tmux logging [https://github.com/tmux-plugins/tmux-logging](https://github.com/tmux-plugins/tmux-logging)

## Python3 and dependencies

`apt install python3-pip`

## Java

`sudo apt install default-jre`

## Rclone

Install rclone [https://rclone.org/downloads/](https://rclone.org/downloads/) `curl https://rclone.org/install.sh | sudo bash`

Configure for Google Cloud Storage [https://rclone.org/googlecloudstorage/](https://rclone.org/googlecloudstorage/)

`rclone config`

## Nginx

Install Nginx

```
> apt install nginx
```

This UFW app rule opens both ports 80 and 443.   Can use this instead of separate UFW rules for these ports.

```
> ufw allow 'Nginx Full'

> ufw status numbered

     To                         Action      From
     --                         ------      ----
[ 1] 7777                       ALLOW IN    Anywhere
[ 2] Nginx Full                 ALLOW IN    Anywhere
[ 3] 7777 (v6)                  ALLOW IN    Anywhere (v6)
[ 4] Nginx Full (v6)            ALLOW IN    Anywhere (v6)
```

## MySQL

{% embed url="https://www.digitalocean.com/community/tutorials/how-to-install-mysql-on-ubuntu-20-04" %}

may have to use the deprecated _mysql\_native\_password_ method to auth users, php-mysql doesn't support the new sha2

## phpmyadmin

{% embed url="https://www.digitalocean.com/community/tutorials/how-to-install-and-secure-phpmyadmin-with-nginx-on-an-ubuntu-18-04-server" %}



## Certbot SSH Certificate

[https://certbot.eff.org/lets-encrypt/ubuntuother-nginx](https://certbot.eff.org/lets-encrypt/ubuntuother-nginx)

## PHP

`apt install php-fpm`

may have to manually install mysqli, it's deprecated in PHP 7+

`apt install php-mysql`
