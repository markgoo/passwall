基于lean openwrt编译最后一版 开源 passwall

可以使用ubuntu/debian

sudo apt-get update
sudo apt-get -y install build-essential asciidoc binutils bzip2 gawk gettext git libncurses5-dev libz-dev patch python3.5 unzip zlib1g-dev lib32gcc1 libc6-dev-i386 subversion flex uglifyjs git-core gcc-multilib p7zip p7zip-full msmtp libssl-dev texinfo libglib2.0-dev xmlto qemu-utils upx libelf-dev autoconf automake libtool autopoint device-tree-compiler g++-multilib antlr3 gperf

git clone https://github.com/coolsnowwolf/lede

cd /lede/package
git clone https://github.com/keramist/lienol-openwrt-package.git
cd
cd lede

./scripts/feeds update -a && ./scripts/feeds install -a
make menuconfig
make -j8 download V=s
make -j20 V=s


二次编译
cd lede
git pull
./scripts/feeds update -a && ./scripts/feeds install -a
make defconfig
make -j8 download
make -j$(($(nproc) + 1)) V=s

重新配置
rm -rf ./tmp && rm -rf .config
make menuconfig
make -j$(($(nproc) + 1)) V=s

个人建议删除
rm -rf lede
后重新下载配置编译
