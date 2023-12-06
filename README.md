# Genesis
This repository contains data files which encode "genesis" blocks for Topl's main network.  A "genesis" block (a.k.a. "big bang" block) is the first block in a blockchain.  In particular, it contains the initial distribution of tokens and staking registrations for the network.

## Structure
This repository contains a genesis block and a sample configuration file.
- `README.md`
- `toplnet/`
- `toplnet/config.yaml`

### Genesis structure
Within the `toplnet` directory, a genesis block is encoded using protobuf in a normalized structure.  The contents should include:
- `{blockId}.header.pbuf`
  - A protobuf-encoded BlockHeader file, where `{blockId}` is the ID of the genesis block
- `{blockId}.body.pbuf`
  - A protobuf-encoded BlockBody file, where `{blockId}` is the ID of the genesis block
  - From the decoded BlockBody, the transactionIds can be extracted which should map to the following files
- `{transactionId0}.transaction.pbuf`
  - A protobuf-encoded IoTransaction file, where `{transactionId0}` is the ID of the transaction contained within the genesis block
- `{transactionId1}.transaction.pbuf`
- `{transactionId2}.transaction.pbuf`
- ...
- `{transactionIdN}.transaction.pbuf`

#### Creation
A genesis block can be created using the Bifrost CLI's `init-mainnet` command.  The CLI will output the files that should be uploaded (via Pull Request) to this repository.

## Node Launch
A Bifrost node can be configured to point to this repository for its genesis configuration.  The custom configuration would include:
```yaml
bifrost:
  big-bang:
    type: public
    genesis-id: b_9ry5ZcSpRtcTB1p6rcQLeYCYMkFW4Q6oRqAbSShC57RZ
    source-path: https://raw.githubusercontent.com/Topl/Genesis/main/toplnet
```
