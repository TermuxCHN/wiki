# pacman

[了解更多](https://github.com/termux-pacman)

## 安装

```shell
pkg i pacman -y
pacman -Syyu
pacman -S $(pkg list-i | sed 's|/| |; s|Listing...||' | awk '{ printf $1 " " }') --overwrite "*"
pacman -Rcns apt #可选，建议删掉
```

然后重启Termux，执行`termux-setup-package-manager`

* pkg也可以调用pacman

## 卸载

```shell
pacman -Sy apt
apt remove --purge pacman -y
apt update -y
apt upgrade -y
```

然后重启Termux，执行`termux-setup-package-manager`

# glibc-packages

```bash
[gpkg-dev]
Server = https://s3.amazonaws.com/termux-pacman.us/gpkg-dev/$arch
```



# tur

```bash
[tur]
Server = https://s3.amazonaws.com/termux-pacman.us/tur/$arch

[tur-continuous]
Server = https://s3.amazonaws.com/termux-pacman.us/tur-continuous/$arch

[tur-multilib]
Server = https://s3.amazonaws.com/termux-pacman.us/tur-multilib/$arch
```

