# apt

Package Management

[https://linuxize.com/post/how-to-use-apt-command/](https://linuxize.com/post/how-to-use-apt-command/)

## update

Update the list of

```bash
apt update
```

## list

View the list of available packages from repos.

```bash
apt list # everything
apt list | grep search-term # grep it

apt list --installed
apt list --upgradable
```

## upgrade

To upgrade the installed packages to their latest versions

```bash
apt upgrade # all currently upgradeable packages
apt upgrade package-name # just one package
```

## autoremove

Remove unused packages and dependencies

```bash
apt autoremove
```

## show

Display package information

```bash
apt show package-name
```

## search

Search repos for available packages

```bash
apt search package-name
```
