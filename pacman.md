# pacman

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