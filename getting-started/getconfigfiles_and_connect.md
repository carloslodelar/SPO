# Get configuration files

Starting the node and connecting it to the testnet requires 3 configuration files:

* topology.json
* genesis.json
* config.json

In your home directory, create a new directory for the configuration files:

```text
cd
mkdir relay
cd relay
```

{% hint style="info" %}
You can download the configuration files from:

 [https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/index.html](https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/index.html)
{% endhint %}

Or with the command line using:

```text
wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/shelley_testnet-config.json
wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/shelley_testnet-shelley-genesis.json
wget https://hydra.iohk.io/job/Cardano/cardano-node/cardano-deployment/latest-finished/download/1/shelley_testnet-topology.json
```



