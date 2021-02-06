#### 账户信息
```
*VPN账号 intesim *VPN密码 intesim_test2021 
*子账号 intetest10 *用户密码 2MWxPaUK 
*子账号 intetest14 *用户密码 AeHQ9CUb 
*子账号 intetest5 *用户密码 vAp6c8A1 
*子账号 intetest2 *用户密码 qiIFzMtS 
*子账号 intetest16 *用户密码 KNFYxQM5 
*子账号 intetest11 *用户密码 rYMVjgWN 
*子账号 intetest7 *用户密码 YJSktVdH 
*子账号 intetest20 *用户密码 UTFm0e8a 
*子账号 intetest18 *用户密码 FZc2jz53 
*子账号 intetest6 *用户密码 Ixuys0MV 
*子账号 intetest13 *用户密码 1L4yOdoQ 
*子账号 intetest1 *用户密码 fgWAuNtA 
*子账号 intetest17 *用户密码 RHyIfjLV 
*子账号 intetest9 *用户密码 WzMqa8yG 
*子账号 intetest12 *用户密码 FVljHZC5 
*子账号 intetest8 *用户密码 JlblacUb 
*子账号 intetest4 *用户密码 dXx21dqP 
*子账号 intetest15 *用户密码 Ub5R7b3c 
*子账号 intetest19 *用户密码 3wdZxhGS 
*子账号 intetest3 *用户密码 UGhZj7TL 
```
#### csub命令命令设置

``` 
ssh intetest20@173.0.31.63
密码：
cd GPFS8p/
mkdir aipInstall
cd aipInstall/
scp intesim@173.0.31.63:/home/export/base/nsccwuxi_intesim/intesim/GPFS8p/aip_install/9.20.3/skyformaip-9.20.3rhel6.tar.gz .
密码：t00jnReR
tar xvf skyformaip-9.20.3rhel6.tar.gz
mkdir Install
./client-install --dir=/home/export/base/nsccwuxi_intesim/intetest20/GPFS8p/aipInstall/Install/    

gsn018
192.168.212.77
gsn017
41.0.0.17
cd Install/etc  
cat aip.sh >> ~/.bashrc
vim ~/.bashrc 
出现以下内容则是设置成功
-------------------------------------------
# User specific aliases and functions#
# aip.sh:
#   Setup user environment for SkyForm AIP
#
-------------------------------------------
回到install目录 cd ..
rm -rf bin/b*
source ~/.bashrc
csub 
能使用则成功
```
#### 设置openbox环境
```

cd ~
scp -r intesim@173.0.31.63:/home/export/base/nsccwuxi_intesim/intesim/.config/openbox .config/
密码：t00jnReR
cp .vnc/xstartup .vnc/xstartup.orig
scp intesim@173.0.31.63:/home/export/base/nsccwuxi_intesim/intesim/.vnc/xstartup .vnc/
密码：t00jnReR
vim ~/.bashrc
在最后一行加入：export PATH=/openbox1217/bin:$PATH
source ~/.bashrc
vncserver -geometry 1440x1080
```