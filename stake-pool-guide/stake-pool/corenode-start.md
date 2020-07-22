# Start your core node

To start your node as leader candidate you need to add the keys and node certificate to the command that we have used to run the node: 

```text
cardano-node run \
--topology shelley_testnet-topology.json \
--database-path /db \
--socket-path /db/node.socket \
--host-addr <PUBLIC IP> \
--port <PORT> \
--config shelley_testnet-config.json \
--shelley-kes-key kes.skey \
--shelley-vrf-key vrf.skey \
--shelley-operational-certificate node.cert
```

