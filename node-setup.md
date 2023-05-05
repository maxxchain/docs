# MaxxChain Node Setup

These instructions are for Ubuntu 18,20,22

## User Creation 

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
Allow ports 30303, 8545 on firewall with the following command    

#### 🚨 Security Alert 🚨    
If you are mining do not open port (8545)

```bash
ufw allow 30303
ufw allow 8545
```   

## Pre-Requisites

you need to switch to ubuntu user to run the commands below

you can switch user using commands below

```bash
su ubuntu
cd ~
```

## Install Go Lang: 

// make sure you are in /home/ubuntu folder

```bash
wget https://storage.googleapis.com/golang/go1.19.linux-amd64.tar.gz
tar -xvf go1.19.linux-amd64.tar.gz
sudo rm -fr /usr/local/go
sudo mv go /usr/local
export GOROOT=/usr/local/go
export PATH=$GOPATH/bin:$GOROOT/bin:$PATH
```

## Installing MaxxChain Node 

## Clone Repo

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

## Genesis Block

- Download Genesis block and init blockchain

```bash
git clone https://github.com/maxxchain/genesis-block
```

## Run the following command to initialize geth with MaxxChain genesis block
```bash
cd genesis-block
```
#### For MaxxChain Testnet 
```bash
geth init /path/to/genesis-block/testnet.json
```

#### For MaxxChain Mainnet 
```bash
geth init /path/to/genesis-block/mainnet.json
```

## Start Geth and Node Sync

```bash
geth --networkid 10201 --port 30303 --http --http.port 8545 --http.addr 0.0.0.0 --http.api personal,eth,net --http.corsdomain '*' --syncmode full
```

### MaxxxChain Mainnet vs Testnet 
Mainnet chain id = 10201
Testnet chain id = 10203

#### Important note
Make sure to replace the --networkid 10201 with the appropiate chain id depending if you want
to run the MaxxChain mainnet or the testnet.    


## Connect to geth console to add seed peers

```bash
git clone https://github.com/maxxchain/bootnodes && cd bootnodes
```

- Give permission to the executable bash file

```bash
sudo chmod 755 mainnet-init.sh
sudo chmod 755 testnet-init.sh
```

- Run the command to install community defined MaxxChain peers onto your geth
### If you are running MaxxChain mainnet 
```bash
./mainnet-init.sh
```    
    
### If you are running MaxxChain testnet 
```bash
./testnet-init.sh
```

Congratulations you have your geth full node up and running.

