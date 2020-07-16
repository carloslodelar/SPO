# Start your nodes:

First we restart our **relay node** with:

```text
cardano-node run \
--topology shelley_testnet-topology.json \
--database-path db \
--socket-path db/node.socket \
--host-addr <PUBLIC IP> \
--port <PORT> \
--config shelley_testnet-config.json
```

then, we start our **block producing** node with:

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

