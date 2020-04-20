基于lean openwrt编译最后一版 开源 passwall

可以使用ubuntu/debian

sudo apt-get update
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf


git clone -b dev-lean-lede https://github.com/Lienol/openwrt lean-lede

cd ./lede  
1 编辑   
nano feeds.conf.default  
添加  
src-git passwall https://github.com/keramist/passwall  
注释掉 原来的 lienol 源，
2 或者直接添加passwall 包到/lean-lede/package/lean/下

./scripts/feeds update -a && ./scripts/feeds install -a  
make menuconfig  
make -j8 download V=s  
make -j20 V=s  


二次编译  
cd lede  
git pull  
./scripts/feeds update -a && ./scripts/feeds install -a  
make defconfig  
make -j8 download V=s   
make -j$(($(nproc) + 1)) V=s  

重新配置  
rm -rf ./tmp && rm -rf .config  
make menuconfig  
make -j$(($(nproc) + 1)) V=s  

个人建议删除  
rm -rf lede  
后重新下载配置编译  

passwall 挺好的 ，感谢作者，  
但是tg 的非passwall官方群就是sb行径，  
推广机场，无可厚非，  
但用户说不好，有问题，只要说机场不好，就直接禁言，  
不知道马甲有千千万？    
祝他们都早日吃上免费饭。  
大家不爽的可以去举报。
