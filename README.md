如何编译自己需要的 OpenWrt 固件
-
注意：
-
1. **不要**用 **root** 用户进行编译！！！
  `非必要 请输入 `export FORCE_UNSAFE_CONFIGURE=1` && export `FORCE=1` `
2. 国内用户编译前最好准备好梯子
3. 默认登陆IP 192.168.2.1 密码 admin


编译命令如下:
-
1. 若你是  Ubuntu 20.04 LTS x64

   > 命令行输入 `sudo apt-get update` ，然后输入
   ```
   sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3 python2.7 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf wget curl swig rsync
   ```

2. 使用 ```git clone https://github.com/B5CSGO/R5S``` 命令下载好源代码，然后 `cd R5S` 进入目录

3. ```bash
   ./scripts/feeds update -a
   ./scripts/feeds install -a -f
   make menuconfig
   ```

3. `make -j8 download V=s` 下载dl库（国内请尽量全局科学上网）

4. 输入 `make -j1 V=s` （-j1 后面是线程数。第一次编译推荐用单线程）即可开始编译你要的固件了。

本套代码保证肯定可以编译成功。里面包括了 R22 所有源代码，包括 IPK 的。

你可以自由使用，但源码编译二次发布请注明我的 GitHub 仓库链接。谢谢合作！
=
如果你使用WSL或WSL2进行编译：
------
由于wsl的PATH路径中包含带有空格的Windows路径，有可能会导致编译失败，请在将make -j1 V=s或make -j$(($(nproc) + 1)) V=s改为

首次编译：
```bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin make -j1 V=s 
```
二次编译：
```bash
PATH=/usr/local/sbin:/usr/local/bin:/usr/sbin:/usr/bin:/sbin:/bin make -j$(($(nproc) + 1)) V=s
```

