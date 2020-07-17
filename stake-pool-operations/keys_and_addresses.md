# Generate payment keys and addresses

We need to create two sets of keys and addresses. One set to control our funds \(make and receive payments\) and one set to control our stake \(to participate in the protocol delegating our stake\)

Let's produce our cryptographic keys first, as we will need them to later create our addresses:

### Payment key pair

Generate a _payment key pair_:

```text
 cardano-cli shelley address key-gen \
 --verification-key-file payment.vkey \
 --signing-key-file payment.skey
```

This will create two files \(here named `payment.vkey` and `payment.skey`\), one containing the _public verification key_, one the _private signing key_.

The files are in plain-text format and human readable:

```text
 cat payment.vkey

 > type: VerificationKeyShelley
 > title: Free form text
 > cbor-hex:
 >  18af58...
```

The first line describes the file type and should not be changed. The second line is a free form text that we could change if we so wished. The key itself is the cbor-encoded byte-string in the fourth line.

### Payment address

We then use `payment.vkey` and `stake.vkey` to create our `payment address`:

```text
 cardano-cli shelley address build \
 --payment-verification-key-file payment.vkey \
 --out-file payment.addr \
 --testnet-magic 42
```

This created the file payment.addr that is already associated with our stake keys:

```text
cat payment.addr
> 00ec78e3d3916636101f6d9539c451f248ba200f38f2c33129f7ef36d66853603e872296956a4d86
```

To query your address \(see the utxo's at that address\), you first need to set environment variable `CARDANO_NODE_SOCKET_PATH` to the socket-path specified in your node configuration. In this example we will use the block-producing node created in the previous steps:

```text
export CARDANO_NODE_SOCKET_PATH=~/cardano-node/relay/db/node.socket
```

make sure that your node is running. Then use  `cardano-cli shelley query utxo` to find out the address' balance:

```text
cardano-cli shelley query utxo \
--address $(cat payment.addr) \
--testnet-magic 42
```

you should see something like this:

```text
                       TxHash                                 TxIx        Lovelace
----------------------------------------------------------------------------------
```

