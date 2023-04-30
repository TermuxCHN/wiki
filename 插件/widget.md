# 介绍

通过桌面快捷方式运行 Termux 里的脚本。

# 下载

Github (需要登录 Github 账号): https://github.com/termux/termux-widget/actions/workflows/debug_build.yml

F-droid: https://f-droid.org/en/packages/com.termux.widget

# 这玩意咋用啊？

先在 Termux 中执行以下命令：

```bash
mkdir -p /data/data/com.termux/files/home/.shortcuts
chmod 700 -R /data/data/com.termux/files/home/.shortcuts
mkdir -p /data/data/com.termux/files/home/.shortcuts/tasks
chmod 700 -R /data/data/com.termux/files/home/.shortcuts/tasks
```

如果你想让脚本在前台运行，就把脚本丢到`~/.shortcuts/`

如果你想让脚本在后台运行，就把脚本丢到`~/.shortcuts/tasks/`

## 图标

在 Termux 中执行以下命令：

```bash
mkdir -p /data/data/com.termux/files/home/.shortcuts/icons
chmod -R a-x,u=rwX,go-rwx /data/data/com.termux/files/home/.shortcuts/icons
```

命名要求：

`脚本名字.png`，如`scripts.sh.png`。

