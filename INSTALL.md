# How to install ElectrumX for Sumcoin using the ElectrumX installer script
This guide assumes you have Sumcoind running and synced with the Sumcoin blockchain with RPC credentials set and transaction indexing enabled.

## Step 1 - Download the script
Clone the script:   

```
git clone https://github.com/bauerj/electrumx-installer.git
```

Navigate into the directory were you cloned the script: 

```
cd electrumx-installer
```

## Step 2 - Run the script
Now run the script to install ElectrumX with Sumcoin:   

```
sudo bash ./install.sh --electrumx-git-url https://github.com/Tech1k/electrumx-sum.git
```

* Let the script install all required dependencies and install ElectrumX (this takes about 2-5 minutes).

### You should get the following:

```
Installing installer dependencies                                                                           
Adding new user for electrumx                                                                           
Creating database directory in /db                                                                           
INFO:    Python 3.6 is already installed.
Installing git                                                                           
Installing RocksDB                                                                           
Installing pyrocksdb                                                                           
Checking pyrocksdb installation                                                                           
Installing electrumx                                                                           
Installing init scripts                                                                           
INFO:    Use service electrumx start to start electrumx once it's configured
Generating TLS certificates                                                                           
INFO:    electrumx has been installed successfully. Edit /etc/electrumx.conf to configure it....
```

## Step 3 - Configure ElectrumX for Sumcoin
Edit the ElectrumX configuration file:  
```
sudo nano /etc/electrumx.conf
```

* Here's how the configuration file should look: 

```
# default /etc/electrumx.conf for systemd
COIN = Sumcoin
NET = mainnet

# REQUIRED
DB_DIRECTORY = /db
# Bitcoin Node RPC Credentials
DAEMON_URL = http://<RPCUSER>:<RPCPASSWORD>@localhost:3332/


# See http://electrumx.readthedocs.io/en/latest/environment.html for
# information about other configuration settings you probably want to consider.

DB_ENGINE=rocksdb

SSL_CERTFILE=/etc/electrumx/server.crt
SSL_KEYFILE=/etc/electrumx/server.key
#TCP_PORT=50001
#SSL_PORT=50002
# Listen on all interfaces:
#HOST=
```

Note: replace `<RPCUSER>` with your Sumcoind RPC username and `<RPCPASS>` with your RPC password.

## Step 4 - Start ElectrumX
Start ElectrumX by running: 

`service electrumx start`

Check the logs and indexing progress of ElectrumX with: 

`journalctl -u electrumx -f`

If everything installed correctly, you should see ElectrumX properly syncs with your Sumcoin node and listens for incoming connections.


