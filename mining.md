## Mining MaxxChain

These instructions are for Ubuntu users, will work for version 18,20,22.
Note that there are similarity in setting up a mining node and a regular node but some 
minor change and precautions needs to be taken.

## Setup a user 

Create a user ubuntu and provide sudo permission
```bash
useradd -m ubuntu
passwd ubuntu
```
Make him sudo

```bash
usermod -aG sudo ubuntu
```
Try not to use root to install. Use ubuntu user to continue with steps below.

## Default Ports
Allow ports 30303 on firewall with the following command

#### 🚨 Security Alert 🚨    
Do not open port (8545)

```bash
ufw allow 30303 # allows peers connect to you but not required if you don't want to publish your node address
ufw deny 8545 # do this just to be sure the port is not left open
```   

Switch to the ubuntu user we just created above

```bash
su ubuntu
cd ~
```

## Install Go Lang if you have not already done so: 

#### 🚨 Make sure you are in /home/ubuntu folder 🚨

```bash
wget https://storage.googleapis.com/golang/go1.19.linux-amd64.tar.gz
tar -xvf go1.19.linux-amd64.tar.gz
sudo rm -fr /usr/local/go
sudo mv go /usr/local
export GOROOT=/usr/local/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

## Installing MaxxChain Node 

### Clone Repo and build geth

```bash
cd ~
git clone https://github.com/maxxchain/go-ethereum
cd go-ethereum/
sudo apt-get update && sudo apt-get dist-upgrade -y
sudo apt-get install build-essential make git screen unzip curl nginx pkg-config nmap xterm screen tcl -y
make geth
```

### Add geth to path (optional)
```bash
export PATH=/root/go-ethereum/build/bin:$PATH"
```

### Setup genesis Block

```bash
git clone https://github.com/maxxchain/genesis-block && cd genesis-block
```

#### If you want to mine MaxxChain Testnet use 👇

```bash
geth --datadir data init /path/to/genesis-block/testnet.json
```

#### If you will be mining MaxxChain Mainnet use 👇
```bash
geth --datadir data init /path/to/genesis-block/mainnet.json
```

### Start Geth Node Mining

```bash
geth --networkid 10201 --datadir data --mine --miner.threads=1 --miner.etherbase=0x3784d4d687806e031487a3ef4c48c7893016e9e7
```

### Chain Id's for MaxxxChain Mainnet and Testnet 
- Mainnet = 10201
- Testnet = 10203

#### 🚨 Important note 🚨
Make sure to replace the --networkid 10201 with the appropiate chain id depending if you want
to run the MaxxChain mainnet or the testnet.    


### Connect to geth console to add seed peers

```bash
git clone https://github.com/maxxchain/bootnodes && cd bootnodes
```

- Give permission to the executable bash file

```bash
sudo chmod 755 mainnet-init.sh
sudo chmod 755 testnet-init.sh
```

### Run the command to install community defined MaxxChain peers onto your geth
#### If you are running MaxxChain mainnet 
```bash
./mainnet-init.sh
```    
    
#### If you are running MaxxChain testnet 
```bash
./testnet-init.sh
```

Congratulations you have your geth full node up and running.

