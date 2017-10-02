# insight-btcz
sudo apt-get -y install \
      build-essential pkg-config libc6-dev m4 g++-multilib \
      autoconf libtool ncurses-dev unzip git python \
      zlib1g-dev wget bsdmainutils automake libzmq3-dev
     
     
     
sudo apt-get -y install npm


wget -qO- https://raw.githubusercontent.com/creationix/nvm/master/install.sh | bash

export NVM_DIR="$HOME/.nvm"
[ -s "$NVM_DIR/nvm.sh" ] && . "$NVM_DIR/nvm.sh" # This loads nvm


nvm install v4

npm install str4d/bitcore-node-zcash

./node_modules/bitcore-node-zcash/bin/bitcore-node create zcash-explorer
cd zcash-explorer
../node_modules/bitcore-node-zcash/bin/bitcore-node install str4d/insight-api-zcash str4d/insight-ui-zcash

cat << EOF > bitcore-node.json
{
  "network": "mainnet",
  "port": 3001,
  "services": [
    "bitcoind",
    "insight-api-zcash",
    "insight-ui-zcash",
    "web"
  ],
  "servicesConfig": {
    "bitcoind": {
      "spawn": {
        "datadir": "./data",
        "exec": "zcashd"
      }
    }
  }
}
EOF
