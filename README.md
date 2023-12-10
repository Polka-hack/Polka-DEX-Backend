## Polka DEX Backend Code

A new Cumulus-based Substrate node, ready for hacking :rocket:

## Local Development

Follow these steps to prepare a local Substrate development environment :hammer_and_wrench:

### Simple Setup

Install all the required dependencies with a single command (be patient, this can take up to 30
minutes).

```bash
curl https://getsubstrate.io -sSf | bash -s -- --fast
```

### Manual Setup

Find manual setup instructions at the
[Substrate Developer Hub](https://substrate.dev/docs/en/knowledgebase/getting-started/#manual-installation).

### Build

Once the development environment is set up, build the node template. This command will build the
[Wasm](https://substrate.dev/docs/en/knowledgebase/advanced/executor#wasm-execution) and
[native](https://substrate.dev/docs/en/knowledgebase/advanced/executor#native-execution) code:

```bash
cargo build --release
```

## Run

### Single Staging Node Chain

Purge any existing staging chain state:

```bash
./target/release/parachain-collator purge-chain --chain staging
```

Start a staging chain:

```bash
./target/release/parachain-collator --chain staging
```

Or, start a staging chain with detailed logging:

```bash
RUST_LOG=debug RUST_BACKTRACE=1 ./target/release/parachain-collator -lruntime=debug --chain staging
```

### Local Testnet

Polkadot (rococo-branch):
```
./target/release/polkadot build-spec --chain rococo-local --raw --disable-default-bootnode > rococo_local.json

./target/release/polkadot --chain ./rococo_local.json -d cumulus_relay1 --validator --bob --port 50555
./target/release/polkadot --chain ./rococo_local.json -d cumulus_relay0 --validator --alice --port 50556
```

```
# this command assumes the chain spec is in a directory named polkadot that is a sibling of the working directory
./target/release/parachain-collator -d local-test --validator --ws-port 9945 --port 40333 --parachain-id 200 -- --chain dex_raw.json --port 40444 --bootnodes=/ip4/127.0.0.1/tcp/30333/p2p/12D3KooWNvB9rzENgxaxbj72osHGk4dVeUiYvWkauC3TUQC7p5tc
```

If you want to see the multi-node consensus algorithm in action, refer to
[our Start a Private Network tutorial](https://substrate.dev/docs/en/tutorials/start-a-private-network/).