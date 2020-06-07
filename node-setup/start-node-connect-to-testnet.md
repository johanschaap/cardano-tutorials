# How to start the node and connect it to the testnet.

## Get some configuration files

Starting the node and connecting it to the network requires 3 important files: 

* topology.json
* genesis.json
* config.json

You can download them [here](https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/index.html).

Or from the command line with: 

    wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/ff-topology.json
    wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/ff-genesis.json
    wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/ff-config.json
    

## Starting the node

Starting the the node uses the command `cardano-node run` and a set of options.
	
You can get the complete list of available options with `cardano-node run --help`  

	--topology FILEPATH             The path to a file describing the topology.
        --database-path FILEPATH        Directory where the state is stored.
        --socket-path FILEPATH          Path to a cardano-node socket
        --host-addr HOST-NAME           Optionally limit node to one ipv6 or ipv4 address
        --port PORT                     The port number
        --config NODE-CONFIGURATION     Configuration file for the cardano-node
        --validate-db                   Validate all on-disk database files
        --shutdown-ipc FD               Shut down the process when this inherited FD reaches EOF
        --shutdown-on-slot-synced SLOT  Shut down the process after ChainDB is synced up to the
                                        specified slot
   -h,--help                       Show this help text
   
To start a passive node, do:

	cardano-node run --topology path/to/ff-topology.json \
	                 --database-path path/to/db \
                         --socket-path path/to/db/node.socket \
			 --host-addr 192.0.2.0 \
			 --port PORT \
			 --config path/to/ff-config.json

you can check whether the node is syncing by fetching the current tip. (The `--testnet-magic 42` identifies the FF-testnet)

        export CARDANO_NODE_SOCKET_PATH=path/to/db/node.socket
        cardano-cli shelley query tip --testnet-magic 42
        
        > Tip (SlotNo {unSlotNo = 74680}) (ShelleyHash {unShelleyHash = HashHeader {unHashHeader = edfefc4ac1e6a6ad1551bcf0650ade22f2e99937936bb61d8d7d5fae2e6a19aa}}) (BlockNo {unBlockNo = 2030})

Note, that syncing phase can take some time. 
