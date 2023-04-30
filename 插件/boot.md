# 介绍

手机启动后自动运行脚本。

# 下载

Github (需要登录 Github 账号): https://github.com/termux/termux-boot/actions/workflows/debug_build.yml

F-droid: https://f-droid.org/packages/com.termux.boot/

# 这玩意咋用啊？

~~自己看README.md啊！~~

1. 安装Termux:Boot

2. 关闭 Termux 和 Termux:Boot 的电池优化

   ![](https://user-images.githubusercontent.com/57583560/235346132-b66dabad-98c6-4fa8-bc8a-409bb2142c01.png)

   3. 启动一次 Termux:Boot

   4. 在 Termux 中 创建 `~/.termux/boot/` 目录，把要自启的脚本丢进去

   5. 为了防止休眠，请在每个脚本的开头加上`termux-wake-lock`

## 举个栗子

```bash
#!/data/data/com.termux/files/usr/bin/sh
# 设置唤醒锁
termux-wake-lock
# 启动ssh服务
sshd
```

