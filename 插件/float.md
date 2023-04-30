# 介绍

俗称：小窗

# 下载

Github (需要登录 Github 账号): https://github.com/termux/termux-float/actions/workflows/debug_build.yml

F-droid: https://f-droid.org/en/packages/com.termux.window/

# 这玩意咋用啊？

打开插件，点击中间的`GRANT PERMISSION`，打开 Termux:Float 的悬浮窗权限。

调整大小： 一个手指按住黑色的边框，另外一个手指拖动下面的边缘

左上角的按钮是缩小，右上角是关闭。

# 设置

```bash
mkdir -p ~/.termux/
touch ~/.termux/termux.float.properties
```

支持下面的属性：

```bash
enforce-char-based-input
ctrl-space-workaround
bell-character
terminal-cursor-style
terminal-transcript-rows
back-key
default-working-directory
volume-keys
```

