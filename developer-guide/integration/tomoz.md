---
description: TomoZ is the runtime feature to perform gas-less transaction with TRC25 token
---

# TomoZ

### How it works

* TomoZ enables gas-less transaction for TRC25 by requiring the owner to deposit TOMO to VRC25Issuer contract. So when there is transaction call to TRC25 token, the gas fee will be paid by the owner. Please note that internal call to TRC25 token won't be gas-sponsored.
* The owner of TRC25 token must call `apply` function of `VRC25Issuer` contract at [0x8c0faeb5c6bed2129b8674f262fd45c4e9468bee](https://tomoscan.io/address/0x8c0faeb5c6bed2129b8674f262fd45c4e9468bee) after deployment in order to register for TomoZ. If a contract didn't register TomoZ yet, the transaction fee must be paid by the user who perform the transaction.
* When the TOMO for the TRC25 token is exhausted, user will pay gas for it normally unless the owner deposit more TOMO.

### Requirement

* Smart-contract that meet [TRC25 Specification](../standards-and-specification/trc25-specification.md).
* 10 TOMO for first time registration.

### How to apply

The owner of TRC25 token must call `apply` function of `VRC25Issuer` contract at [0x8c0faeb5c6bed2129b8674f262fd45c4e9468bee](https://tomoscan.io/address/0x8c0faeb5c6bed2129b8674f262fd45c4e9468bee).

The [source code](https://github.com/tomochain/trc25/raw/main/contracts/tests/VRC25Issuer.sol) and [ABI](https://github.com/tomochain/trc25/raw/main/metadata/VRC25Issuer.json) for VRC25Issuer contract can be found in [trc25 repository](https://github.com/tomochain/trc25/).

