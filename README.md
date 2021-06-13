https://www.youtube.com/watch?v=U-IIKVaEhrA

# https://github.com/c4pt000/AlternativeCryptoCurrencyBuilder-scrypt



JUST DOWNLOAD YOUR COIN
EDIT YOUR COIN ARTWORK AND RENAME YOUR COIN
THEN CHANGE PCHMESSAGE IN CHAINPARAMS.CPP

artwork usually lives in /src/qt/res/icons

and grep for coin name and or sed replace

DOES NOT REQUIRE NEW GENESIS OR MERKLE HASH AT ALL FOR MAIN, TEST, OR REGRESSION NETWORKS

THEN LINK NODES TO DEPLOY YOUR NEW COIN

CHANGE TO YOUR UNIQUE VALUES AND COMMENT OUT THE DNS SEEDS
```
  pchMessageStart[0] = 0xee;
        pchMessageStart[1] = 0xff;
        pchMessageStart[2] = 0xgg;
        pchMessageStart[3] = 0xhh;
        
        
        some line in chainparams.cpp
        
             // Note that of those with the service bits flag, most only support a subset of possible options
//vSeeds.push_back(CDNSSeedData("radioblockchain.info", "seed-ns1.radioblockchain.info", true));
//vSeeds.push_back(CDNSSeedData("radioblockchain.info", "seed-ns2.radioblockchain.info" ));
//vSeeds.push_back(CDNSSeedData("radioblockchain.info", "seed-ns3.radioblockchain.info" ));

        
```

SAMPLE REMOTE VPS NODE FOR NEW NETWORK
```
upnp=1
listen=1
mempoolexpiry=72
maxmempool=300
maxorphantx=100
disablewallet=1
#prune=2200
## Spam protection
limitfreerelay=10
minrelaytxfee=0.0001

maxconnections=40

server=1
daemon=1

rpctimeout=30
rpcport=8332
rpcconnect=127.0.0.1

#rpcsslciphers=TLSv1+HIGH:!SSLv2:!aNULL:!eNULL:!AH:!3DES:@STRENGTH
#rpcsslcertificatechainfile=server.cert
#rpcsslprivatekeyfile=server.pem

# Do not use Internet Relay Chat to find peers.
noirc=0
minimizetotray=0

```
SAMPLE LOCAL CLIENT CONF FOR NEW WALLET-QT

```
#prune=2200   

rpcuser=root
rpcpassword=rpcpassword

rpcport=8332
rpcallowport=8333


rpcconnect=0.0.0.0
rpcbind=0.0.0.0
rpcallowip=127.0.0.1


            
dbcache=2048
maxorphantx=10
maxmempool=50
mempoolexpiry=24
maxconnections=10
maxuploadtarget=5000

whitelist=0.0.0.0/24



# change to your new remote VPS node(s)
addnode=104.237.145.126:9333



gen=1

daemon=1
server=1

```




# BLOCKCHAIN-GENERATOR (requires docker)


https://medium.com/@jordan.baczuk/how-to-fork-bitcoin-part-2-59b9eddb49a4

https://jbaczuk.github.io/blockchain_fundamentals/3-Development/3.2-Design.html

https://bitcoin.stackexchange.com/questions/80810/error-acceptblock-high-hash-proof-of-work-failed-code-16

https://github.com/c4pt000/AltcoinGenerator

requires replacing src/qt/res/icons properly

```
sudo dnf -y install dnf-plugins-core
 sudo dnf config-manager \
    --add-repo \
    https://download.docker.com/linux/fedora/docker-ce.repo
    
    
     sudo dnf install docker-ce docker-ce-cli containerd.io

 ```

* based off of genesis-generator and blockchain tools  (supports threads for faster genesis block generation)
# requires python3 + google go language + pip3

# requires version go 1.16.3
# or similar , pip 21.0.1 from /usr/lib/python3.9/site-packages/pip (python 3.9)

---------------------------------

for generate-genesis functionality
```
go mod init generate-genesis
go mod tidy
go build

pip install ecdsa
export COIN=bitcoin

```

```
./sha256.py "phrase here"

./pubkey.py -u <pubkey>
```

sha256 hash generator

```
./sha256.py "your phrase" 

2358feea3003a1d16af3454be4cec2f6a7db43bfc7daa101b8949fff91ed64b4 
``` 

PUBLIC_KEY generator
```
./pubkey.py -u 2358feea3003a1d16af3454be4cec2f6a7db43bfc7daa101b8949fff91ed64b4 


PUBLIC_KEY

048f74dca316b3faa7e947919babe20e274d5c1f4cf3366652bd360bb51322f652b575fd0461fb982fd9aabf39c879db9f08a5f505bb5671083bc085c1802eac56

```

```
example

time epoch
date +%s


./generate-genesis -algo scrypt -bits 1e0ffff0 -coins 10000000000 -psz "your phrase" -timestamp 1620011758 -pubkey 048f74dca316b3faa7e947919babe20e274d5c1f4cf3366652bd360bb51322f652b575fd0461fb982fd9aabf39c879db9f08a5f505bb5671083bc085c1802eac56 -threads 24

```

* edit src/amount.h for supply of network


to generate 3 assets for src/chainparams.cpp
```
edit 3net-assert-gen.sh for your PUBLIC_KEY 

wget https://raw.githubusercontent.com/c4pt000/BLOCKCHAIN-GENERATOR/main/3net-assert-gen.sh
chmod +x 3net-assert-gen.sh
sh 3net-assert-gen.sh
```


Genesis block generator
=======================


with thread support (24 threads)
![s1](https://raw.githubusercontent.com/c4pt000/BLOCKCHAIN-GENERATOR/main/24-threads-processor-jobs.png)
```
example

./generate-genesis -algo scrypt -bits 1e0ffff0 -coins 10000000000 -psz "your phrase" -timestamp 1620011758 -pubkey 048f74dca316b3faa7e947919babe20e274d5c1f4cf3366652bd360bb51322f652b575fd0461fb982fd9aabf39c879db9f08a5f505bb5671083bc085c1802eac56 -threads 24
```





<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
<br>
original code

<br>
<br>

Introduction
------------

This tool provides a convenient way to generate Genesis block for bitcoin-clone (altcoin) crypto currencies.


Build
-----

```shell
$ go get -d -v
$ go build
$ go test
```

Usage
-----

```shell
$ ./generate-genesis -h
Usage of ./generate-genesis:
  -algo string
        Algo to use: sha256, scrypt, x11, quark (default "sha256")
  -bits string
        Bits (default "1d00ffff")
  -coins uint
        Number of coins (default 5000000000)
  -nonce uint
        Nonce value (default 2083236893)
  -profile string
        Write profile information into file (debug)
  -psz string
        pszTimestamp (default "The Times 03/Jan/2009 Chancellor on brink of second bailout for banks")
  -pubkey string
        Pubkey (required) (default "04678afdb0fe5548271967f1a67130b7105cd6a828e03909a67962e0ea1f61deb649f6bc3f4cef38c4f35504e51ec112de5c384df7ba0b8d578a4c702b6bf11d5f")
  -threads int
        Number of threads to use (default 4)
  -timestamp uint
        Timestamp to use (default 1231006505)
```

Samples
-------

### Bitcoin (default)

```shell
$ ./generate-genesis
Ctrl Hash:      0x000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f
Target:         0x00000000ffff0000000000000000000000000000000000000000000000000000
Blk Hash:       0x000000000019d6689c085ae165831e934ff763ae46a2a6c172b3f1b60a8ce26f
Mkl Hash:       0x4a5e1e4baab89f3a32518a88c31bc87f618f76673e2cc77ab2127b7afdeda33b
Nonce:          2083236893
Timestamp:      1231006505
Pubkey:         04678afdb0fe5548271967f1a67130b7105cd6a828e03909a67962e0ea1f61deb649f6bc3f4cef38c4f35504e51ec112de5c384df7ba0b8d578a4c702b6bf11d5f
Coins:          5000000000
Psz:            'The Times 03/Jan/2009 Chancellor on brink of second bailout for banks'
```

### Litecoin

```shell
$ ./generate-genesis -algo scrypt -bits 1e0ffff0 -coins 5000000000 -nonce 2084524480 -timestamp 1317972665 -pubkey 040184710fa689ad5023690c80f3a49c8f13f8d45b8c857fbcbc8bc4a8e4d3eb4b10f4d4604fa08dce601aaf0f470216fe1b51850b4acf21b179c45070ac7b03a9 -psz "NY Times 05/Oct/2011 Steve Jobs, Apple’s Visionary, Dies at 56"
Ctrl Hash:      0x0000050c34a64b415b6b15b37f2216634b5b1669cb9a2e38d76f7213b0671e00
Target:         0x00000ffff0000000000000000000000000000000000000000000000000000000
Blk Hash:       0x0a2efd19744ffdff263e7223faf3a212c6040acfdc03d6b09f3e1ed1dd6f8272
Mkl Hash:       0x97ddfbbae6be97fd6cdf3e7ca13232a3afff2353e29badfab7f73011edd4ced9
Nonce:          2084524493
Timestamp:      1317972665
Pubkey:         040184710fa689ad5023690c80f3a49c8f13f8d45b8c857fbcbc8bc4a8e4d3eb4b10f4d4604fa08dce601aaf0f470216fe1b51850b4acf21b179c45070ac7b03a9
Coins:          5000000000
Psz:            'NY Times 05/Oct/2011 Steve Jobs, Apple’s Visionary, Dies at 56'
```

### Dash (x11)

```shell
$ ./generate-genesis -algo x11 -bits 1e0ffff0 -coins 5000000000 -psz "Wired 09/Jan/2014 The Grand Experiment Goes Live: Overstock.com Is Now Accepting Bitcoins" -pubkey "040184710fa689ad5023690c80f3a49c8f13f8d45b8c857fbcbc8bc4a8e4d3eb4b10f4d4604fa08dce601aaf0f470216fe1b51850b4acf21b179c45070ac7b03a9" -timestamp 1390095618 -nonce 28917600
Ctrl Hash:      0x00000ffd590b1485b3caadc19b22e6379c733355108f107a430458cdf3407ab6
Target:         0x00000ffff0000000000000000000000000000000000000000000000000000000
Blk Hash:       0x00000ffd590b1485b3caadc19b22e6379c733355108f107a430458cdf3407ab6
Mkl Hash:       0xe0028eb9648db56b1ac77cf090b99048a8007e2bb64b68f092c03c7f56a662c7
Nonce:          28917698
Timestamp:      1390095618
Pubkey:         040184710fa689ad5023690c80f3a49c8f13f8d45b8c857fbcbc8bc4a8e4d3eb4b10f4d4604fa08dce601aaf0f470216fe1b51850b4acf21b179c45070ac7b03a9
Coins:          5000000000
Psz:            'Wired 09/Jan/2014 The Grand Experiment Goes Live: Overstock.com Is Now Accepting Bitcoins'
```
