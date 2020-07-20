# Command Line Interface

This command line interface provides a collection of tools for key generation, transaction construction, certificate creation and other important tasks.

It is organized in a hierarchy of subcommands, and each level comes with its own built-in documentation of command syntax and options.

We can get the top level help by simply typing the command without arguments:

```text
cardano-cli
```

We will be told that one available subcommand is `shelley`, and typing

```text
cardano-cli shelley
```

will display available sub-subcommands, one of which is `node`. We can continue drilling down the hierarchy:

```text
cardano-cli shelley node
```

and learn about the sub-sub-subcommand `key-gen`. Typing

```text
cardano-cli shelley node key-gen
```

will inform us about the parameters this command takes, so we can for example generate a key-pair of offline keys and a file for the issue counter by typing

```text
cardano-cli shelley node key-gen \
--cold-verification-key-file cold.vkey \
--cold-signing-key-file cold.skey \
--operational-certificate-issue-counter-file cold.counter
```

![\`cardano-cli\` command hierarchy](../../.gitbook/assets/cli.png)

