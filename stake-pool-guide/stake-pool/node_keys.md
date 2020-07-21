# Generate your stake pool keys

A stake pool needs at least 2 running nodes: A **block-producing** node and a **relay** node.

We need to setup our **block-producing** node. You can build the node from source or maintain a single build on your local machine and only upload the binaries to your **block-producing** and **relay** servers. Just make sure you have consistent versions across them.

![network diagram](../../.gitbook/assets/basic-network-with-relays-producers-passivenodes-walletnodes.png)

The **block-producing** node will only connect with it's **relay**, while the **relay** will establish connections with other relays in the network. Each node must run in an independent server.

## Basic block-producing node firewall configuration:

* Make sure you can only login with SSH Keys, not password.
* Make sure to setup SSH connections in a port different than the default 22
* Make sure to configure the firewall to only allow connections from your relay nodes by setting up their ip addresses.

## Basic relay node firewall configuration:

* Make sure you can only login with SSH Keys, not password.
* Make sure to setup SSH connections in a port different than the default 22.
* Make sure you only have the strictly necessary ports opened.

## Creating keys for our block-producing node

**WARNING:** You may want to use your **local machine** for this process \(assuming you have cardano-node and cardano-cli on it\). Make sure you are not online until you have put your **cold keys** in a secure storage and deleted the files from you local machine.

The **block-producing node** or **pool node** needs:

* **Cold** key pair,
* **VRF** Key pair,
* **KES** Key pair,
* **Operational Certificate**

Create a directory on your local machine to store your keys:

```text
mkdir pool-keys
cd pool-keys
```

## 1. Generate **Cold** Keys and a **Cold\_counter**:

```text
cardano-cli shelley node key-gen \
--cold-verification-key-file cold.vkey \
--cold-signing-key-file cold.skey \
--operational-certificate-issue-counter-file cold.counter
```

## 2. Generate VRF Key pair

```text
cardano-cli shelley node key-gen-VRF \
--verification-key-file vrf.vkey \
--signing-key-file vrf.skey
```

## 3. Generate the KES Key pair

```text
cardano-cli shelley node key-gen-KES \
--verification-key-file kes.vkey \
--signing-key-file kes.skey
```

## 4. Generate the Operational Certificate

We need to know the slots per KES period, we get it from the genesis file:

```text
cat shelley_testnet-genesis.json | grep KESPeriod
> "slotsPerKESPeriod": 3600,
```

So one period lasts 3600 slots.

Then we need the current tip of the blockchain:

We can use your relay node to query the tip:

```text
cardano-cli shelley query tip --testnet-magic 42

{
    "blockNo": 27470,
    "headerHash": "bd954e753c1131a6cb7ab3a737ca7f78e2477bea93db54511cedefe8899ebed0",
    "slotNo": 656260
}
```

Look for Tip `unSlotNo` value. In this example we are on slot 656260. So we have KES period is 182:

```text
expr 656260 / 3600
> 182
```

{% hint style="info" %}
`slotNo` and `Kes-period` will be different when you run this commands. So make sure to calculate them yourself. 
{% endhint %}

To generate the certificate:

```text
cardano-cli shelley node issue-op-cert \
--kes-verification-key-file kes.vkey \
--cold-signing-key-file cold.skey \
--operational-certificate-issue-counter cold.counter \
--kes-period 120 \
--out-file node.cert
```

## Move the cold keys to secure storage and remove them from your local machine.

The best place for your cold keys is a **SECURE USB** or other **SECURE EXTERNAL DEVICE**, not a computer with internet access.

## Copy your cold keys from your server to your local machine and from them to COLD storage. 

You can do this with scp command. 

```text
scp -rv -P<SSH PORT> -i ~/.ssh/<SSH_PRIVATE_KEY> ~/pool-keys USER@<PUBLIC_IP>:~/

> Transferred: sent 3220, received 6012 bytes, in 1.2 seconds
Bytes per second: sent 2606.6, received 4866.8
debug1: Exit status 0
```

Log in to your server and verify that the files are there:

```text
ls pool-keys

> kes.skey  kes.vkey  node.cert  vrf.skey  vrf.vkey  
```

Later on we will learn how to register our pool in the blockchain.

