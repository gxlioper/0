# arch-linux-surface

This is an Arch Linux packager that applies 
[jakeday's patches for Surface devices](https://github.com/jakeday/linux-surface) 
to the Linux kernel of your choice. 

## Pre-Installation

First thing you're going to want to do is to clone this repository:

```
git clone https://github.com/dmhacker/arch-linux-surface
cd arch-linux-surface
```

Before you begin compiling & installing the patched kernel, it's recommended that you 
install all necessary firmware that your Surface device needs and replace suspend with hibernate.
You can do this by running the `setup.sh` script with superuser permissions.

```
sudo sh setup.sh
```

Now, you are ready to begin compilation of your kernel. 
Alternatively, you could download the 
[pre-built kernel binaries](https://github.com/dmhacker/arch-linux-surface/releases) 
and skip ahead to the installation section.

## Compilation

To generate the build directory for the kernel, you need to run the `configure.sh` script. 
The packager will prompt for the target major version of the Linux kernel during configuration.

```
sh configure.sh 
```

Once configure is finished, it will output a directory titled `build-[VERSION]`. 
Note that [VERSION] is the full version of the kernel and not just its major version. 
To build this kernel, use these two commands: 

```
cd build-[VERSION] 
MAKEFLAGS="-j[NPROC]" makepkg -sc
```

  \* Replace [VERSION] with whatever kernel version configure outputs.   
  \*\* Replace [NPROC] with the number of available processors in your machine.  

If you are unable to issue this command because of write permission issues, use the following
command to give yourself access, replacing [USER] and [VERSION] with their appropriate values:

```
chown -R [USER] build-[VERSION]
```

## Installation

When the build process is completed, under `build-[VERSION]`, you will find these packages:
```
linux-surface-[VERSION]-1-x86_64.pkg.tar.xz
linux-surface-headers-[VERSION]-1-x86_64.pkg.tar.xz
linux-surface-docs-[VERSION]-1-x86_64.pkg.tar.xz
```
You can either install them with `sudo pacman -U ...` or do something else with them.


 # 良心友情链接

[腾讯QQ群快速检索](http://u.720life.cn/s/8cf73f7c)

[软件免费开发论坛](http://u.720life.cn/s/bbb01dc0)