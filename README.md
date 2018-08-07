T
is is biscoin.

Install dependencies:

sudo apt-get install build-essential libtool autotools-dev autoconf pkg-config libssl-dev
sudo apt-get install libboost-all-dev

sudo add-apt-repository ppa:bitcoin/bitcoin
sudo apt-get update
sudo apt-get install libminiupnpc-dev 

sudo apt-get install libdb4.8-dev
sudo apt-get install libdb4.8++-dev

Change to own coin name:

find . -type f -print0 | xargs -0 sed -i 's/biscoin/{own coin}/g'
find . -type f -print0 | xargs -0 sed -i 's/Biscoin/{own coin}/g'
find . -type f -print0 | xargs -0 sed -i 's/BisCoin/{own coin}/g'
find . -type f -print0 | xargs -0 sed -i 's/BISCOIN/{own coin}/g'
find . -type f -print0 | xargs -0 sed -i 's/BIC/{own coin}/g'

find . -type f -print0 | xargs -0 sed -i 's/9333/6333/g'
find . -type f -print0 | xargs -0 sed -i 's/9332/6332/g'

Openssl Generate Key:

openssl ecparam -genkey -name secp256k1 -out alertkey.pem
openssl ec -in alertkey.pem -text > alertkey.hex
openssl ecparam -genkey -name secp256k1 -out testnetalert.pem
openssl ec -in testnetalert.pem -text > testnetalert.hex
openssl ecparam -genkey -name secp256k1 -out genesiscoinbase.pem
openssl ec -in testnetalert.pem -text > genesiscoinbase.hex

alert.cpp ->> pszTestKey = "{key}";

main.h ->> MAX_MONEY = {defalut 84000000} * COIN;
main.h ->> COINBASE_MATURITY = {default 100};
main.h ->> return dPriority > COIN * {default 576} / 250;

main.cpp ->> nSubsidy = {num} * COIN;
main.cpp ->> txNew.vout[0].nValue = {num} * COIN;

main.cpp ->> nSubsidy >>= (nHeight / {defaule 840000}); 
main.cpp ->> nTargetTimespan = {defalut 3.5 day}
main.cpp ->> nTargetSpacing = {defalut 2.5 minutes}

main.cpp ->> block.nTime = {epoch time}; // terminal: date +%s 


First build and run:

make -f makefile.unix USE_UPNP=-

./biscoind

After first run. You need push block.hashMerkleRoot == uint256("0x{new hash get from .biscoin}") // from main.cpp

build and run again for testnet:

./biscoind -testnet

After run. you need change block.nNonce = {get from .biscoin}; // in if (fTestNet) from main.cpp

And change hashGenesisBlock = uint256("0x{get from .biscoin}"); // in method bool LoadBlockIndex() from main.cpp

build and run again:

./biscoind

After run. you need change block.nNonce = {get from .biscoin}; // from main.cpp

And change uint256 hashGenesisBlock("0x{get from .biscoin}"); // from main.cpp

 checkpoint.cpp ->> you need change mapCheckpoints and data uint256("0x{hash}") and data nTime - testnet mirror

last make in root project:

qmake
make

and run ./biscoin-qt -testnet and ./biscoin
or you will run ./biscoind

/////////////// COMPLETE //////////////////

Full node:

in biscoin.conf from .biscoin

server=1
rpcuser=user
rpcpassword=password

Add node:

addnode={full node ip}


//////////////////////////////////////////

Basic biscoin command:

getinfo
getmininginfo
setgenerate true
setgenerate false


*pnSeed[]= from net.cpp
you can generate from command perl ip.perl
