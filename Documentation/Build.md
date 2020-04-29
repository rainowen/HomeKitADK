# Build ADK on RPI

## Prepare Compile ENV
``` shell
sudo apt update
sudo apt upgrade
sudo apt-get install clang libavahi-compat-libdnssd-dev libsqlite3-dev libasound2-dev libopus-dev libavahi-compat-libdnssd-dev
make homekit_adk_src
cd homekit_adk_src
wget http://ftp.br.debian.org/debian/pool/non-free/f/faac/libfaac-dev_1.29.9.2-2_armhf.deb
wget http://ftp.br.debian.org/debian/pool/non-free/f/faac/libfaac0_1.29.9.2-2_armhf.deb
sudo dkpg -i libfaac0_1.29.9.2-2_armhf.deb
sudo dkpg -i libfaac-dev_1.29.9.2-2_armhf.deb
```

## Git Clone the repo and build the ADK
```shell
git clone https://github.com/apple/HomeKitADK.git
cd HomeKitADK

make TARGET=Linux DOCKER=0 tools
./Tools/provision_raspi.sh --category 5 --setup-code 111-22-333 ./Output/Linux-armv6k-unknown-linux-gnueabihf/Debug/IP/Applications/.HomeKitStore
make TARGET=Linux DOCKER=0 apps
```
## Running the Lightbulb Demo app
```shell
cd ./Output/Linux-x86_64-pc-linux-gnu/Debug/IP/Applications/
./Lightbulb.OpenSSL
```
