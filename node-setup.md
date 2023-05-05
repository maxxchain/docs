# MaxxChain Node Setup

Basic Instructions to start a new node on Ubuntu Distro. Based on your OS and environment, you may need to make changes.

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

Open ports 30303, 8545 

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
git clone https://github.com/maxxchain/go-ethereum
ls -la
cd go-ethereum/
sudo apt-get update && sudo apt-get dist-upgrade -y
sudo apt-get install build-essential make git screen unzip curl nginx pkg-config nmap xterm screen tcl -y
make geth
```

## Genesis Block

- Download Genesis block and init blockchain

```bash
git clone https://github.com/maxxchain/genesis-block
```

- Change directory to go-ethereum 

```bash
cd go-ethereum/
```

- Run the following command to initialize geth with MaxxChain genesis block

```bash
./build/bin/geth init /path/to/genesis-block/mainnet.json
```

- Start Geth and Node Sync
```bash
./build/bin/geth --networkid 10201 --port 30303 --http --http.port 8545 --http.addr 0.0.0.0 --http.api personal,eth,net --http.corsdomain '*' --syncmode full
```

## Connect to geth console to add seed peers

```bash
git clone https://github.com/maxxchain/bootnodes && cd bootnodes
```

- Give permission to the executable bash file

```bash
sudo chmod 755 init.sh
```

- Run the command and it will automatically install all seed peers on your geth and you are ready to go

```bash
./init.sh
```

Congratulations you have your geth full node up and running.

