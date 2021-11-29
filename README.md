*Forked from the [CryptoNote](https://github.com/cryptonotefoundation/cryptonote) cryptocurrency protocol.*
<br>
# **What is Simone?**
Simone is a privacy based open source cryptocurrency. It is currently in early development and is planned to be used to tip small amounts of money privately and securely to strangers.

## **Coin Information**<br>
- Max Coin Supply: 18446744073709551616<br>
- First Block Reward: ~22,000 SMN
- Emission Curve: 23
   - Block rewards will be reduced to 50% of the reward of the first mined block in about 10 years, or 2031
   - Block rewards will be reduced to 25% of the reward of the first mined block in about 22 years, or 2043
- Difficulty Target: 60 Seconds

## **Networking Information**
Required Ports:
- Default/P2P Port: 42019
- RPC Port: 42020

Seed Node DNS A Records:
- node-nyc-01.smn.network:42019
- node-sfo-01.smn.network:42019

## **Build Instructions**
Simone is currently only supported and tested on Ubuntu Linux, though other distributions would likely work based on the notes from the Ubuntu installs. Windows support is currently in development. If you are looking to run a wallet on Windows consider [WSL](https://docs.microsoft.com/en-us/windows/wsl/install).

### Ubuntu 16.04

These instructions assume a clean build of Ubuntu 16.04 installed directly from the latest ISO provided by Cannonical, which can be found [here] (https://releases.ubuntu.com/16.04). Build time will depend on your hardware. On a VM with two dedicated cores and 4GB of RAM the deployment process takes about 30 minutes.\
\
Note that we require a specific version of gcc and boost in order for the software to complile. If you simply clone the repository
and attempt to compile it is extremely likely that it will NOT work.

Perform updates and install the prerequisite software to complile Simone
\
`sudo apt update` \
`sudo apt upgrade` \
`sudo apt install build-essential git cmake g++ python-dev autotools-dev libicu-dev libbz2-dev` \
\
Check the installed version of gcc. Tested and confirmed working with gcc version 5.4.0 \
\
`gcc -v`\
`Expected output: gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.12)`\
\
Download and compile boost version 1.58.0. Depending on your system this may take a while. \
\
`wget http://downloads.sourceforge.net/project/boost/boost/1.58.0/boost_1_58_0.tar.gz` \
`tar -zxvf boost_1_58_0.tar.gz` \
`cd boost_1_58_0` \
`./bootstrap.sh` \
`sudo ./b2 --with=all install` \
\
Check the installed version of boost. Tested and confirmed working with boost version 1.58.0 \
\
`cat /usr/local/include/boost/version.hpp | grep "BOOST_LIB_VERSION"` \
`Expected output: #define BOOST_LIB_VERSION "1_58"` \
\
Create a new user to run the Simone node and wallet \
\
`cd`\
`sudo adduser simone`\
\
Change to the new user\
\
`su simone`\
`cd`\
\
Clone the repository\
\
`git clone https://github.com/aelagrassa/simone` \
\
Change to the repository directory and compile. Depending on your system this may take a while.\
\
`cd simone` \
`make` \
\
Simone should now be compiled and ready to go. You can now start the node. \
\
`cd build/release/src` \
`./Simone`

## **Other Useful Notes**
### Running Simone as a serivce in Ubuntu
\
Create the required service file.\
\
`sudo nano /etc/systemd/system/simone.service`\
\
Enter the following text. Update as needed for your setup. This configuration should work if you followed the install guides above.
```
[Unit]
Description=Simone Node
After=network.target

[Service]
User=root
WorkingDirectory=/home/simone/simone/build/release/src

Type=simple
ExecStart=/home/simone/simone/build/release/src/Simone
StandardOutput=null
StandardError=null

Restart=always

[Install]
WantedBy=multi-user.target
```
Reload the systemctl daemon\
`sudo systemctl daemon-reload`\
\
Start the simone service
`sudo systemctl start simone.service`\
\
Check the status of the simone service and ensure it is running\
`sudo systemctl status simone.service`
\
Enable the simone service to automatically launch on startup
`sudo systemctl enable example.service`\
