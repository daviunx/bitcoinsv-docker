# bitcoinsv-docker
Local bitcoinsv regtest node setup for local development with docker.

# Build and run
`docker-compose build && docker-compose up`

This will run 2 containers with bitcoind running on it. 

# Access to container node 1
`docker exec -it sv-node1 /bin/bash`

# Generate blocks & get coin rewards

To generate blocks and get coin rewards run:

`bitcoin-cli -rpcuser=sv -rpcpassword=svrocks -regtest generate 200`

Or from outside of the container:

`docker exec -it sv-node1 bitcoin-cli -rpcuser=sv -rpcpassword=svrocks -regtest generate 200`

200 blocks will be generated. 25 coins as reward will be received per each block generated.

# Send coins to node-2 address
## Get new address
`docker exec -it sv-node2 bitcoin-cli -rpcuser=sv -rpcpassword=svrocks -regtest -rpcport=28332 getnewaddress`

This will return an address, in this example `mr6hzQMoTFeZZSSoJGSWkuVBRy5y4FtWLU`

## Send coins from node-1
`docker exec -it sv-node1 bitcoin-cli -rpcuser=sv -rpcpassword=svrocks -regtest sendtoaddress mr6hzQMoTFeZZSSoJGSWkuVBRy5y4FtWLU 200`

**Remember: you will need to generate a block to put this transaction so node-2 will receive the coins **

# Updating bitcoin configuration
bitcoin.conf file is located at `sv/node-x/bitcoin.conf`. Edit the file with your needs and rebuild following Build & Run steps.


## Configuration node-1
Can be found in `sv/node-1/bitcoin.conf`

````
excessiveblocksize=0
maxstackmemoryusageconsensus=0
maxstackmemoryusagepolicy=0
regtest=1
server=1
datadir=/home/root/.bitcoin
rpcuser=sv
rpcpassword=svrocks
rpcallowip=::/0
rpcport=18332
rest=1
txindex=1
port=245
addnode=sv-node2:246
````

## Configuration node-2
Can be found in `sv/node-2/bitcoin.conf`

````
excessiveblocksize=0
maxstackmemoryusageconsensus=0
maxstackmemoryusagepolicy=0
regtest=1
server=1
datadir=/home/root/.bitcoin
rpcuser=sv
rpcpassword=svrocks
rpcallowip=::/0
rpcport=28332
rest=1
txindex=1
port=246
````


Enjoy!