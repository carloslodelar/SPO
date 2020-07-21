# Generate stake keys and address



### Stake key pair

Now let us create our _stake key pair_ :

```text
 cardano-cli shelley stake-address key-gen \
 --verification-key-file stake.vkey \
 --signing-key-file stake.skey
```

### Stake address

Finally, we can create our stake address. This address **CAN'T** receive payments but will receive the rewards from participating in the protocol. We will save this address in the file `stake.addr`

```text
 cardano-cli shelley stake-address build \
 --stake-verification-key-file stake.vkey \
 --out-file stake.addr \
 --testnet-magic 42
```

This created the file stake.addr, let's check its content:

```text
cat stake.addr
> 5821e0872296956a4d86ee9654060734e83dddc56016fb2ecc7cbb435ee8e3c1053d9d
```

### Regenerate payment address

Now that we have a stake address, it is time to regenerate a payment address. This time we use both the stake verification key and payment verification key to build the address. With this, both addresses will be linked together and associated with one another. 

```text
 cardano-cli shelley address build \
 --payment-verification-key-file payment.vkey \
 --stake-verification-key-file stake.vkey \
 --out-file paymentwithstake.addr \
 --testnet-magic 42
```

