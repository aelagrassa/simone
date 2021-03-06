*Forked from the [CryptoNote](https://github.com/cryptonotefoundation/cryptonote) cryptocurrency protocol.*
<br>
# **What is Simone?**
Simone is a privacy based open source cryptocurrency. It is currently in early development and is planned to be used to tip small amounts of money privately and securely to strangers.
## **How much money is Simone (SMN) worth?**<br>
None.
## **Coin Information**<br>
- Abbreviation: SMN
- Max Coin Supply: 20,000,000,000,000,000<br>
- First Block Reward: ~24 SMN
- Emission Curve: 23
   - Block rewards will be reduced to 50% of the reward of the first mined block in about 10 years, or 2031
   - Block rewards will be reduced to 25% of the reward of the first mined block in about 22 years, or 2043
- Difficulty Target: 60 Seconds

## **Networking Information**
Required Ports:
- Default/P2P Port: 42019
- RPC Port: 42020

Seed Node DNS A Records:
- node-nyc-01.smn.network
- node-sfo-01.smn.network
- node-ams-01.smn.network
- node-fra-01.smn.network

## **Build Instructions**
Simone is currently only supported and tested on Ubuntu Linux, though other distributions would likely work based on the notes from the Ubuntu installs. Windows support is currently in development. If you are looking to run a wallet on Windows consider [WSL](https://docs.microsoft.com/en-us/windows/wsl/install). If you choose to use WSL simply create a new instance of Ubuntu 16.04 or 18.04 and follow the steps listed below.
\
\
For the casual user WSL or a virtual machine running Ubuntu 16.04 would be the easiest, albeit least secure, option. 

### WSL
If you are running Windows 11 or some recent versions of Windows 10 you can install the Simone node, wallet, and GUI wallet by leveraging WSL. To get started open an administrative CMD prompt and enter:
```
wsl --install -d Ubuntu-16.04
```
Once your Ubuntu instance is set up follow the **Ubuntu 16.04** section of this guide.
### Ubuntu 16.04

These instructions assume a clean build of Ubuntu 16.04 installed directly from the latest ISO provided by Cannonical, which can be found [here](https://releases.ubuntu.com/16.04). Build time will depend on your hardware. On a VM with two dedicated cores and 4GB of RAM the deployment process takes about 30 minutes.\
\
Note that we require a specific version of gcc and boost in order for the software to complile. If you simply clone the repository
and attempt to compile it is extremely likely that it will NOT work.

Perform updates and install the prerequisite software to complile Simone
```
sudo apt update & sudo apt upgrade -y
sudo apt install build-essential git cmake g++ python-dev autotools-dev libicu-dev libbz2-dev
```
Check the installed version of gcc. Tested and confirmed working with gcc version 5.4.0 \
```
gcc -v
```
`Expected output: gcc version 5.4.0 20160609 (Ubuntu 5.4.0-6ubuntu1~16.04.12)`\
\
Download and compile boost version 1.58.0. Depending on your system this may take a while. \
```
wget http://downloads.sourceforge.net/project/boost/boost/1.58.0/boost_1_58_0.tar.gz
tar -zxvf boost_1_58_0.tar.gz
cd boost_1_58_0
./bootstrap.sh
sudo ./b2 --with=all install
```
Check the installed version of boost. Tested and confirmed working with boost version 1.58.0 \
```
cat /usr/local/include/boost/version.hpp | grep "BOOST_LIB_VERSION"
```
`Expected output: #define BOOST_LIB_VERSION "1_58"`\
\
Create a new user to run the Simone node and wallet
```
cd
sudo adduser simone
```
Change to the new user\
```
su simone
cd
```
Clone the repository
```
git clone https://github.com/aelagrassa/simone
```
Change to the repository directory and compile. Depending on your system this may take a while.
```
cd simone
make
```
Simone should now be compiled and ready to go. You can now start the node.
```
cd build/release/src
./Simone
```
### Ubuntu 18.04

These instructions assume a clean build of Ubuntu 18.04 installed directly from the latest ISO provided by Cannonical, which can be found [here](https://releases.ubuntu.com/18.04). Build time will depend on your hardware. On a VM with two dedicated cores and 4GB of RAM the deployment process takes about 30 minutes.\
\
Note that we require a specific version of gcc and boost in order for the software to complile. If you simply clone the repository
and attempt to compile it is extremely likely that it will NOT work.

Perform updates and install the prerequisite software to complile Simone
```
sudo apt update & sudo apt upgrade -y
sudo apt install build-essential git cmake g++ python-dev autotools-dev libicu-dev libbz2-dev
```
Check the installed version of gcc. It is likely that Ubuntu 18.04 came with gcc version 7.5 which must be uninstalled\
```
gcc -v
```
`Expected output: gcc version 7.5.0 (Ubuntu 7.5.0-3ubuntu1~18.04)`\
\
Uninstall gcc 7.5 and prepare to install an earlier version
```
sudo apt purge gcc-7
```
Install gcc version 5
```
sudo apt install build-essential software-properties-common -y
sudo add-apt-repository ppa:ubuntu-toolchain-r/test -y
sudo apt update
sudo apt install gcc-snapshot -y
sudo apt update
sudo apt install gcc-5 g++-5 -y
sudo update-alternatives --install /usr/bin/gcc gcc /usr/bin/gcc-5 60 --slave /usr/bin/g++ g++ /usr/bin/g++-5
```
Check the installed version of gcc
```
gcc -v
```
`Expected output: gcc version 5.5.0 20171010 (Ubuntu 5.5.0-12ubuntu1)`\
\
Download and compile boost version 1.58.0. Depending on your system this may take a while. \
```
wget http://downloads.sourceforge.net/project/boost/boost/1.58.0/boost_1_58_0.tar.gz
tar -zxvf boost_1_58_0.tar.gz
cd boost_1_58_0
./bootstrap.sh
sudo ./b2 --with=all install
```
Check the installed version of boost. Tested and confirmed working with boost version 1.58.0 \
```
cat /usr/local/include/boost/version.hpp | grep "BOOST_LIB_VERSION"
```
`Expected output: #define BOOST_LIB_VERSION "1_58"`\
\
Create a new user to run the Simone node and wallet
```
cd
sudo adduser simone
```
Change to the new user\
```
su simone
cd
```
\
Clone the repository
```
git clone https://github.com/aelagrassa/simone
```
\
Change to the repository directory and compile. Depending on your system this may take a while.
```
cd simone
make
```
\
Simone should now be compiled and ready to go. You can now start the node.
```
cd build/release/src
./Simone
```

## **Mining Simone**
Because Simone is a CryptoNote fork any miners that work with CryptoNote will likely work with Simone but have yet to be tested. Mining can be done through the included CPU miner or simplewallet CLI itself. To begin mining you can use the following steps:
\
\
Note your wallet address either using the GUI or simplewallet\
\
Navigate to the src folder where the miner is contained
```
cd simone\build\release\src
```
Launch the miner referencing your address
```
./simplewallet
```
Start the miner, the number signifies how many threads you are willing to devote to mining
```
start_mining 1
```
Enjoy your warm and fuzzies for helping the network as well as enjoy some SMN as compensation

## **Other Useful Notes**
### Installing the Simone GUI Wallet ###
If you have a GUI and are interested in a more user-friendly alternative to Simone's **simplewallet** consider compiling and installing the Simone GUI wallet. Instructions can be found [here](https://github.com/aelagrassa/simonewallet).

### Running Simone on boot as a service in Ubuntu
\
Create the required service file.
```
sudo nano /etc/systemd/system/simone.service
```
\
Enter the following text. Update as needed for your setup. This configuration should work if you followed the install guides above.
```
[Unit]
Description=Simone Node
After=network.target

[Service]
User=simone
WorkingDirectory=/home/simone/simone/build/release/src

Type=simple
ExecStart=/home/simone/simone/build/release/src/Simone
StandardOutput=null
StandardError=null

Restart=always

[Install]
WantedBy=multi-user.target
```
Reload the systemctl daemon
```
sudo systemctl daemon-reload
```
Start the simone service
```
sudo systemctl start simone.service
```
Check the status of the simone service and ensure it is running
```
sudo systemctl status simone.service
```
Enable the simone service to automatically launch on startup
```
sudo systemctl enable simone.service
```
