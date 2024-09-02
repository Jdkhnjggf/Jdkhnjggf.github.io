---
layout:     post
title:      "Launch AMD SEV-SNP VM with console"
subtitle:   "用console安装SEV-SNP虚拟机"
date:       2024-08-31 02:01:00
author:     "luobobo"
header-img: "img/paper-note-bg.jpg"
tags:
    - post
---

lbb第一次装es的时候没记notes，过程及其痛苦。

最近又装了一次snp，加倍痛苦。

好像现在也没啥好教程，简单记一下只用terminal (ssh access)，没有GUI的情况下如何最快装好sev-snp VM.

1. 先听它的。 Github
``` bash
git clone https://github.com/AMDESE/AMDSEV.git
cd AMDSEV
git checkout snp-latest

# 如果你想ssh连这个VM, 在common.sh 里给qemu 加上`--enable-slirp`
./build.sh --package
sudo cp kvm.conf /etc/modprobe.d/
```

2. 再听它的
``` bash
cd snp-release-<date>
./install.sh

sudo reboot now
```

Reboot the machine and choose SNP Host kernel from the grub menu.


``` bash
uname -r
# 版本后面应该会有一串rcX-sev-

dmesg | grep -i -e rmp -e sev
# 注意看那个firmware 版本大于1.51，不然你麻烦了

cat /sys/module/kvm_amd/parameters/sev_snp 
Y
```

3. Prepare Guest (好，现在开始含糊起来了)

``` bash
# 先create disk image
qemu-img create -f qcow2 guest_vm.img 40G

# 下载ISO镜像，这里假设你没有gui,只用console,不装vncviewer
# 血泪教训1: 装ubuntu22.04, 用20.04卡在boot环节好久
# 装server, 不然你进去以后麻烦一堆
wget https://releases.ubuntu.com/jammy/ubuntu-22.04.4-live-server-amd64.iso
```

4. Install Guest
``` bash
sudo ./launch-qemu.sh -hda guest_40G.qcow2 -cdrom ubuntu-22.04.4-live-server-amd64.iso

# 进去以后有text图形化界面，看的懂字就问题不大，这一步会装进上一步创建好的disk image里

# 提前给root创建好密码 passwd
# 提前创个普通用户方便待会儿ssh/scp
adduser yourusername

sudo reboot now
```

5. boot from qcow2
``` bash
# 第一步先改launch-vm.sh

USE_DEFAULT_NETWORK="1"

# network 那里我用的
add_opts "-netdev user,id=vmnic,hostfwd=tcp::8000-:22 -device e1000,netdev=vmnic,romfile="

# Launch VM
sudo ./launch-qemu.sh -hda guest_40G.qcow2 

# 冷静，现在还不能用-sev-snp, guest kernel不对 
# snp-release-（date）下面
(Host): scp -P 8000 ./linux/guest/*.deb yourname@localhost:/home/yourname

(VM): dpkg -i *.deb
(VM): sudo reboot now
```

6. Finally
``` bash
sudo ./launch-qemu.sh -hda guest_40G.qcow2 -sev-snp
```
