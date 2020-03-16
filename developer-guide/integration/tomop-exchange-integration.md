---
description: >-
  This document describes how TomoP works for exchanges to allow users to
  deposit privately
---

# TomoP exchange integration

Exchanges will use `exchange deposit address` for users to deposit assets privately. To understand exchange deposit address, let's decode the structure of a TomoP privacy address.

## TomoP privacy address structure

Here's an example of a typical privacy address in TomoP

`9Lysjv9CYsEMEdkYjtRu3Z1Tev4pm9HvGqHnhVAbXMK33yZLDYnoh6ExThWkKMpKBmpuobBiefhmXe5s1PrdktFVjqncW8q`

This is the Base58 format of the following data  
  
0346226e21bdb6cc3ddcccde7ff7678af5a150bfc72433800ab45359ded501705a03c8827ebe7c19ba0358518a88351ff9d8f660dddaceac7e1d0a1b6987e711b0b3ca6f30a2

The data consist of 70 bytes \(140 hex characters\) including:   
`public view key (33 bytes) | public spend key (33 bytes) | checksum (4 bytes)`

`Public view key` and `public spend key` are public keys in compressed format corresponding to `private view key` and `private spend key` , of which

* Private spend key is a normal private key of users \(32 bytes\)
* `Private view key = keccak256(private spend key)`

Each user only needs to keep their single private key in order to be able to send and receive transaction privately.

When Alice wants to send some TOMO to Bob privately, Alice would take Bob's privacy address, decode the Base58 format to have public view and spend keys of Bob in order to generate a stealth address, which is used as recipient to send TOMO privately.

Stealth address is a one time generated address that is different from every transaction. Stealth address is generated using a cryptographic scheme that only Bob could recognize that the stealth address is generated for him.

## What's Exchange Deposit Address \(EDA\)?

`Exchange Deposit Address (EDA)` is Base58-encoded data of the following data:

`public view key (33 bytes) | public spend key (33 bytes) | userID (8 bytes) | checksum (4 bytes)`

User ID is the ID of a user on the exchange that the users wants to deposit. Basically, every user of the exchange will have the same `public view key` and `public spend key` but the difference is userID.

**Deposit steps:**

* Generate stealth address from public view and spend key
* For the UTXO for the stealth address, generate `depositID = ECDH - userID` 
* Make private transaction for the stealth address and `depositID`
* `depositID` will be published to privacy smart contract

```text
struct UTXO {
    CompressPubKey[3] keys; //commitmentX, pubkeyX, txPubX
    uint256 amount; //encoded amount
    uint256 mask;   //encoded mask
    uint256 txID;
    uint256 depositID;  //deposit ID = ECDH - userID
}
```

**Exchange deposit verification steps:**

* Check if the UTXO belongs to the exchange privacy address \(using private view key to check\)
* Compute `userID = depositID - ECDH`
* Check if `userID` matches with one of the user IDs in their database.
* If yes, then that's a deposit transaction to the account that corresponds to the userID

Exchange will have to generate exchange deposit address for every user based on their public keys and userID.

Note that, for deposit, exchanges only need 1 private keys to manage all deposits of all users.

