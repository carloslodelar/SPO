# Start your node



Starting the the node uses the command `cardano-node run` and a set of options.

You can get the complete list of available options with `cardano-node run`

```text
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
```

To start the node, run the following command from inside the relay directory: 

```text
 cardano-node run \
 --topology shelley_testnet-topology.json \
 --database-path db \
 --socket-path db/node.socket \
 --host-addr x.x.x.x \
 --port 3001 \
 --config shelley_testnet-config.json
```

{% hint style="info" %}
Replace x.x.x.x with your public IP 
{% endhint %}

Create the environment variable CARDANO\_NODE\_SOCKET\_PATH 

```text
export CARDANO_NODE_SOCKET_PATH=~/relay/db/node.socket
```

Check whether the node is syncing by fetching the current tip,  a couple of times, `slotNo` should be increasing. `--testnet-magic 42` identifies the Shelley testnet

```text
cardano-cli shelley query tip --testnet-magic 42

{
    "blockNo": 16900,
    "headerHash": "eb964968c860a8abb1ab81bc9da54b572efc01428a5c98d15e5affb5dd9afd12",
    "slotNo": 371284
}



cardano-cli shelley query tip --testnet-magic 42

{
    "blockNo": 16903,
    "headerHash": "ca49a73331bf29808aa33361ae98b41fe797bafb922901af556b7605e386645b",
    "slotNo": 371358
}
```

