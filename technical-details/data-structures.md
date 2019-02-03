# Binary Data Structures

## Blockchain objects

### Address

| \# | Field name | Type | Length |
| --- | :---: | :---: | --- |
| 1 | Version\(0x01\) | Byte | 1 |
| 2 | Address scheme \(0x54 for Testnet and 0x57for Mainnet\) | Byte | 1 |
| 3 | Public key hash | Bytes | 20 |
| 4 | Checksum | Bytes | 4 |

Public key hash is first 20 bytes of\_SecureHash\_of public key bytes. Checksum is first 4 bytes of\_SecureHash\_of version, scheme and hash bytes. SecureHash is hash function Keccak256\(Blake2b256\(data\)\).

### Alias

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Version \(0x02\) | Byte | 1 |
| 2 | Address scheme \(0x54 for Testnet and 0x57 for Mainnet\) | Byte | 1 |
| 3 | Alias bytes length \(N\) | Int | 2 |
| 4 | Alias bytes | Bytes | N |

Alias is a UTF-8 string with the following constraints:

* It contains from 4 to 30 UTF-8 characters
* It can contain characters only from the following alphabet: `-.0123456789@_abcdefghijklmnopqrstuvwxyz` 
* It cannot contain '\n' or any leading/trailing whitespaces

### Proof

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Proof size \(N\) | Short | 2 |
| 2 | Proof | Bytes | N |

### AddressOrAlias

A recipient that can be encoded either as pure address or alias. Both `Address` and `Alias` are `AddressOrAlias`.

### Block

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Version \(0x02 for Genesis block, 0x03 for common block\) | Byte | 0 |
| 2 | Timestamp | Long | 1 |
| 3 | Parent block signature | Bytes | 64 |
| 4 | Consensus block length \(always 40 bytes\) | Int | 4 |
| 5 | Base target | Long | 8 |
| 6 | Generation signature\* | Bytes | 32 |
| 7 | Transactions block length \(N\) | Int | 4 |
| 8 | Transaction \#1 bytes | Bytes | M1 |
| ... | ... | ... | ... |
| 8 + \(K - 1\) | Transaction \#K bytes | Bytes | MK |
| 9 + \(K - 1\) | Generator's public key | Bytes | 32 |
| 10 + \(K - 1\) | Block's signature | Bytes | 64 |

Generation signature is calculated as Blake2b256 hash of the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Previous block's generation signature | Bytes | 32 |
| 2 | Generator's public key | Bytes | 32 |

Block's signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Version \(0x02 for Genesis block,, 0x03 for common block\) | Byte | 1 |
| 2 | Timestamp | Long | 8 |
| 3 | Parent block signature | Bytes | 64 |
| 4 | Consensus block length \(always 40 bytes\) | Int | 4 |
| 5 | Base target | Long | 8 |
| 6 | Generation signature\* | Bytes | 32 |
| 7 | Transactions block length \(N\) | Int | 4 |
| 8 | Transaction \#1 bytes | Bytes | M1 |
| ... | ... | ... | ... |
| 8 + \(K - 1\) | Transaction \#K bytes | Bytes | MK |
| 9 + \(K - 1\) | Generator's public key | Bytes | 32 |

### Order

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Sender's public key | Bytes | 32 |
| 2 | Matcher's public key | Bytes | 32 |
| 3 | Amount's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 4 | Amount's asset ID \(\*if used\) | Bytes | 0 \(32\*\) |
| 5 | Price's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 6 | Price's asset ID \(\*\*if used\) | Bytes | 0 \(32\*\*\) |
| 7 | Order type \(0 - Buy, 1 - Sell\) | Bytes | 1 |
| 8 | Price | Long | 8 |
| 9 | Amount | Long | 8 |
| 10 | Timestamp | Long | 8 |
| 11 | Expiration | Long | 8 |
| 12 | Matcher fee | Long | 8 |
| 13 | Signature | Bytes | 64 |

The price listed for amount asset in price asset \* 10^8.

Expiration is order time to live, timestamp in future, max = 30 days in future.

The signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Sender's public key | Bytes | 32 |
| 2 | Matcher's public key | Bytes | 32 |
| 3 | Amount's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 4 | Amount's asset ID \(\*if used\) | Bytes | 0 \(32\*\) |
| 5 | Price's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 6 | Price's asset ID \(\*\*if used\) | Bytes | 0 \(32\*\*\) |
| 7 | Order type \(0 - Buy, 1 - Sell\) | Bytes | 1 |
| 8 | Price | Long | 8 |
| 9 | Amount | Long | 8 |
| 10 | Timestamp | Long | 8 |
| 11 | Expiration | Long | 8 |
| 12 | Matcher fee | Long | 8 |

### Transactions

Transaction types:

| № | Transaction type |
| --- | --- |
| 1 | GenesisTransaction |
| 2 | PaymentTransaction\* |
| 3 | IssueTransaction |
| 4 | TransferTransaction |
| 5 | ReissueTransaction |
| 6 | BurnTransaction |
| 7 | ExchangeTransaction |
| 8 | LeaseTransaction |
| 9 | LeaseCancelTransaction |
| 10 | CreateAliasTransaction |
| 11 | MassTransferTransaction |
| 12 | DataTransaction |
| 13 | SetScriptTransaction |
| 14 | SponsorFeeTransaction |

\* - Deprecated

#### Genesis transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(1\) | Byte | 1 |
| 2 | Timestamp | Long | 8 |
| 3 | Recipient's address | Bytes | 26 |
| 4 | Amount | Long | 8 |

#### Issue transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x03\) | Byte | 1 |
| 2 | Signature | Bytes | 64 |
| 3 | Transaction type \(2\) | Byte | 1 |
| 4 | Sender's public key | Bytes | 32 |
| 5 | Name's length \(N\) | Short | 2 |
| 6 | Name's bytes | Bytes | N |
| 7 | Description's length \(M\) | Short | 2 |
| 8 | Description's bytes | Bytes | M |
| 9 | Quantity | Long | 8 |
| 10 | Decimals | Byte | 1 |
| 11 | Reissuable flag \(1-True, 0-False\) | Byte | 1 |
| 12 | Fee | Long | 8 |
| 13 | Timestamp | Long | 8 |

The transaction's signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x03\) | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Name's length \(N\) | Short | 2 |
| 4 | Name's bytes | Bytes | N |
| 5 | Description's length \(M\) | Short | 2 |
| 6 | Description's bytes | Bytes | M |
| 7 | Quantity | Long | 8 |
| 8 | Decimals | Byte | 1 |
| 9 | Reissuable flag \(1-True, 0-False\) | Byte | 1 |
| 10 | Fee | Long | 8 |
| 11 | Timestamp | Long | 8 |

#### Reissue transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x05\) | Byte | 1 |
| 2 | Signature | Bytes | 64 |
| 3 | Transaction type \(0x05\) | Byte | 1 |
| 4 | Sender's public key | Bytes | 32 |
| 5 | Asset ID | Bytes | 32 |
| 6 | Quantity | Long | 8 |
| 7 | Reissuable flag \(1-True, 0-False\) | 138 | 1 |
| 8 | Fee | Long | 8 |
| 9 | Timestamp | Long | 8 |

The transaction's signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x05\) | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Asset ID | Bytes | 32 |
| 4 | Quantity | Long | 8 |
| 5 | Reissuable flag \(1-True, 0-False\) | Byte | 1 |
| 6 | Fee | Long | 8 |
| 7 | Timestamp | Long | 8 |

#### Transfer transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x04\) | Byte | 1 |
| 2 | Signature | Bytes | 64 |
| 3 | Transaction type \(0x04\) | Byte | 1 |
| 4 | Sender's public key | Bytes | 32 |
| 5 | Amount's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 6 | Amount's asset ID \(\*if used\) | Bytes | 0 \(32\*\) |
| 7 | Fee's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 8 | Fee's asset ID \(\*\*if used\) | Bytes | 0\(32\*\*\) |
| 9 | Timestamp | Long | 8 |
| 10 | Amount | Long | 8 |
| 11 | Fee | Long | 8 |
| 12 | Recipient's AddressOrAlias object bytes | Bytes | M |
| 13 | Attachment's length \(N\) | Short | 2 |
| 14 | Attachment's bytes | Bytes | N |

The transaction's signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x04\) | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Amount's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 4 | Amount's asset ID \(\*if used\) | Bytes | 0\(32\*\) |
| 5 | Fee's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 6 | Fee's asset ID \(\*\*if used\) | Bytes | 0\(32\*\*\) |
| 7 | Timestamp | Long | 8 |
| 8 | Amount | Long | 8 |
| 9 | Fee | Long | 8 |
| 10 | Recipient's AddressOrAlias object bytes | Bytes | M |
| 11 | Attachment's length \(N\) | Short | 2 |
| 12 | Attachment's bytes | Bytes | N |

#### Versioned transfer transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Reserved \(Always 0\) | Byte | 1 |
| 2 | Transaction type | Byte | 1 |
| 3 | Version | Byte | 1 |
| 4 | Sender's public key | Bytes | 32 |
| 5 | Amount's asset flag \(0-ZBS, 1-Asset\) | Byte | 1 |
| 6 | Amount's asset ID \(\*if used\) | Bytes | 0 \(32\*\) |
| 7 | Timestamp | Long | 8 |
| 8 | Amount | Long | 8 |
| 9 | Fee | Long | 8 |
| 10 | Recipient's AddressOrAlias object bytes | Bytes | M |
| 11 | Attachment's length \(N\) | Short | 2 |
| 12 | Attachment's bytes | Bytes | N |
| 13 | Proofs' version | Byte | 1 |
| 14 | Proofs' number \(P\) | Short | 2 |
| 15 | Proofs | Proof | S |

* The fee only in ZBS;
* You may sign your transaction in your way and place the signature in proofs.

#### Burn transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | ChainId | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Asset ID | Bytes | 32 |
| 4 | Quantity | Long | 8 |
| 5 | Fee | Long | 8 |
| 6 | Timestamp | Long | 8 |
| 7 | Signature | Bytes | 64 |

The transaction's signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | ChainId | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Asset ID | Bytes | 32 |
| 4 | Quantity | Long | 8 |
| 5 | Fee | Long | 8 |
| 6 | Timestamp | Long | 8 |

#### Exchange transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x07\) | Byte | 1 |
| 2 | Buy order object length \(BN\) | Bytes | 4 |
| 3 | Sell order object length \(SN\) | Bytes | 4 |
| 4 | Buy order object bytes | Bytes | BN |
| 5 | Sell order object bytes | Bytes | SN |
| 6 | Price | Long | 8 |
| 7 | Amount | Long | 8 |
| 8 | Buy matcher fee | Long | 8 |
| 9 | Sell matcher fee | Long | 8 |
| 10 | Fee | Long | 8 |
| 11 | Timestamp | Long | 8 |
| 12 | Signature | Bytes | 64 |

The transaction's signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x07\) | Byte | 1 |
| 2 | Buy order object length \(BN\) | Bytes | 4 |
| 3 | Sell order object length \(SN\) | Bytes | 4 |
| 4 | Buy order object bytes | Bytes | BN |
| 5 | Sell order object bytes | Bytes | SN |
| 6 | Price | Long | 8 |
| 7 | Amount | Long | 8 |
| 8 | Buy matcher fee | Long | 8 |
| 9 | Sell matcher fee | Long | 8 |
| 10 | Fee | Long | 8 |
| 11 | Timestamp | Long | 8 |

#### Lease transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x08\) | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Recipient's AddressOrAlias object bytes | Bytes | N |
| 4 | Amount | Long | 8 |
| 5 | Fee | Long | 8 |
| 6 | Timestamp | Long | 8 |
| 7 | Signature | Bytes | 64 |

The transaction's signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x08\) | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Recipient's AddressOrAlias object bytes | Bytes | N |
| 4 | Amount | Long | 8 |
| 5 | Fee | Long | 8 |
| 6 | Timestamp | Long | 8 |

#### Lease Cancel Transactions

| \# | Field | Length | Type |
| --- | --- | --- | --- |
| 1 | Version\(0x01\) | 1 | Byte |
| 2 | chainByte | 1 | Bytes |
| 3 | LeaseId | 1 | ByteStr |
| 4 | fee | 8 | Long |
| 5 | Sender's public key | 32 | Bytes |
| 6 | TineStamp | 8 | Long |

#### Create alias transaction

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x0a\) | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Alias object length \(N\) | Short | 2 |
| 4 | Alias object bytes | Bytes | N |
| 5 | Fee | Long | 8 |
| 6 | Timestamp | Long | 8 |
| 7 | Signature | Bytes | 32 |

The transaction's signature is calculated from the following bytes:

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Transaction type \(0x0a\) | Byte | 1 |
| 2 | Sender's public key | Bytes | 32 |
| 3 | Alias object length \(N\) | Short | 2 |
| 4 | Alias object bytes | Bytes | N |
| 5 | Fee | Long | 8 |
| 6 | Timestamp | Long | 8 |

#### Mass Transfer transaction

| \# | Field name | Length |
| --- | --- | --- |
| 1 | Transaction type \(0x0b\) | 1 |
| 2 | Version \(0x01\) | 1 |
| 3 | Sender's public key | 32 |
| 4 | Asset flag \(0-ZBS, 1-Asset\) | 1 |
| 5 | Asset ID, if any | 0 / 32 |
| 6 | Number of transfers | 2 |
| 7 | AddressOrAlias object for transfer 1 | variable |
| 8 | Amount for transfer 1 | 8 |
| 9 | AddressOrAlias object for transfer 2 | variable |
| 10 | Amount for transfer 2 | 8 |
| ... | ... | ... |
| N+0 | Timestamp | 8 |
| N+1 | Fee | 8 |
| N+2 | Attachment length | 2 |
| N+3 | Attachment bytes | variable |
| N+4 | Proofs version \(0x01\) | 1 |
| N+5 | Proof count | 2 |
| N+6 | Proof1 length \(64\) | 2 |
| N+7 | Proof1 | 64 |
| ... | ... | ... |

The transaction signature is calculated from the fields 1 to N+3, i.e. proofs and signatures are not included.

**Note.** [**Here**](/technical-details/mass-transfer-transaction.md) you can find more details about Mass Transfer Transaction.

Below is a sample **Mass Transfer transaction** encoded as **JSON**:

```cpp
  {
  "type" : 11,
  "version" : 1,
  "id" : "BG7MQF8KffVU6MMbJW5xPowVQsohwJhfEJ4wSF8cWdC2",
  "sender" : "3HhQxe5kLwuTfE3psYcorrhogY4fCwz2BSh",
  "senderPublicKey" : "7eAkEXtFGRPQ9pxjhtcQtbH889n8xSPWuswKfW2v3iK4",
  "fee" : 200000,
  "timestamp" : 1518091313964,
  "proofs" : [ "4Ph6RpcPFfBhU2fx6JgcHLwBuYSpn..." ],   // see Proofs below
  "assetId" : null,
  "attachment" : "59QuUcqP6p",
  "transfers" : [ {
    "recipient" : "3HUQa6qtLhNvBJNyPV1pDRahbrcuQkaDQv2",
    "amount" : 100000000
  }, {
    "recipient" : "3HaAdZcCXAqhvFj113Gbe3Kww4rCGMUZaEZ",
    "amount" : 200000000
  },
  ...
  ]
}
```

### \#

#### Data transaction

| \# | Field name | Length |
| --- | --- | --- |
| 1 | Reserved \(Always 0\) | 1 |
| 2 | Transaction type \(0x0c\) | 1 |
| 3 | Version \(0x01\) | 1 |
| 4 | Sender's public key | 32 |
| 5 | Number of data entries | 2 |
| 6 | Key1 byte size | 2 |
| 7 | Key1 bytes, UTF-8 encoded | variable |
| 8 | Value1 type: 0 = integer 1 = boolean 2 = binary array | 1 |
| 9 | Value1 bytes | variable |
| ... | ... | ... |
| N | Timestamp | 8 |
| N+1 | Fee | 8 |
| N+2 | Proofs version \(0x01\) | 1 |
| N+3 | Proof count \(1\) | 1 |
| N+4 | Signature length \(64\) | 2 |
| N+5 | Signature | 64 |

The transaction signature is calculated from the fields 1 to N+1, i.e. proofs and signatures are not included.

**Note.** [**Here**](/en/technical-details/data-transaction.md) you can find more details about Data Transaction.

Below is a sample **Data transaction** encoded as **JSON**:

```cpp
{
 "type" : 12,
 "id" : "CwHecsEjYemKR7wqRkgkZxGrb5UEfD8yvZpFF5wXm2Su",
 "sender" : "3FjTpAg1VbmxSH39YWnfFukAUhxMqmKqTEZ",
 "senderPublicKey" : "5AzfA9UfpWVYiwFwvdr77k6LWupSTGLb14b24oVdEpMM",
 "fee" : 100000,
 "timestamp" : 1520945679531,
 "proofs" : [ "4huvVwtbALH9W2RQSF5h1XG6PFYLA6nvcAEgv79nVLW7myCysWST6t4wsCqhLCSGoc5zeLxG6MEHpcnB6DPy3XWr" ],
 "data" : [ {
   "key" : "int",
   "type" : "integer",
   "value" : 24
 }, {
   "key" : "bool",
   "type" : "boolean",
   "value" : true
 }, {
   "key" : "blob",
   "type" : "binary",
   "value" : "BzWHaQU"
 } ],
 "version" : 1,
 "height" : 303
}
```

#### Sponsored Fee Transaction

Set and cancel [fee sponsorship](sponsored-fee.md) for asset.

| \# | Field name | Type | Length |
| --- | ---: | --- | --- |
| 1 | Transaction type \(0x0e\) | Byte | 1 |
| 2 | Version \(0x01\) | Byte | 1 |
| 3 | Sender's public key | Bytes | 32 |
| 4 | Asset ID | Bytes | 32 |
| 5 | Minimal fee in assets\* | Long | 8 |
| 6 | Fee | Long | 8 |
| 7 | Timestamp | Long | 8 |
| 8 | Proofs\*\* | Bytes | 64 |

\* Zero value assume canceling sponsorship.

\*\* Currently only signature is supported, signature have Length = 64

**Note.** [**Here**](/technical-details/sponsored-fee.md) you can find more details about Sponsored Transaction.

Below is a sample **Sponsored transaction** encoded as **JSON**:

```cpp
{
  "type" : 14,
  "id" : "CwHecsEjYemKR7wqRkgkZxGrb5UEfD8yvZpFF5wXm2Su",
  "sender" : "3FjTpAg1VbmxSH39YWnfFukAUhxMqmKqTEZ",
  "senderPublicKey" : "5AzfA9UfpWVYiwFwvdr77k6LWupSTGLb14b24oVdEpMM",
  "minSponsoredAssetFee": 100000,
  "fee" : 100000000,
  "timestamp" : 1520945679531,
  "proofs" : [ "4huvVwtbALH9W2RQSF5h1XG6PFYLA6nvcAEgv79nVLW7myCysWST6t4wsCqhLCSGoc5zeLxG6MEHpcnB6DPy3XWr" ],
  "version" : 1,
  "height" : 303
}
```

#### Set Script Transaction

Sets the script which verifies all outgoing transactions. The set script can be changed by another.

| \# | Field name | Type | Length |
| --- | ---: | --- | --- |
| 1 | Transaction type \(0x0d\) | Byte | 1 |
| 2 | Version \(0x01\) | Byte | 1 |
| 3 | ChainId | Byte | 1 |
| 4 | Sender's public key | Bytes | 32 |
| 5 | 1 if script is not null, 0 otherwise | Byte | 1 |
| 6 | Script object length \(N\) | Short | 2 |
| 7 | Script object bytes | Bytes | N |
| 8 | Fee | Long | 8 |
| 9 | Timestamp | Long | 8 |
| 10 | proofs | Bytes | 64 |

[**Here**](/technical-details/0bsnetwork-contracts-language-description.md) you can find more details about 0bsnetwork smart-contracts.

[**Here**](/technical-details/0bsnetwork-contracts-language-description/standard-library.md) you can find more details about smart-contracts standard library.

[**Here**](/technical-details/0bsnetwork-contracts-language-description/creating-and-deploying-a-script-manually.md) you can find detailed instruction how to create and deploy a script manually.

# Set Asset Script Transaction

| Field | Type | Length |
| :--- | :--- | :--- |
| Transaction Type | Byte | 1 |
| Version | Byte | 1 |
| ChainId | Byte | 1 |
| Sender's Public Key | PublicKeyAccount | 32 |
| AssetId | Bytes | 32 |
| Fee | Long | 8 |
| Timestamp | Long | 8 |
| 1 if script is not null, 0 otherwise | Byte | 1 |
| Script object length \(N\) | Short | 2 |
| Script object bytes | Bytes | N |
| Proofs | Bytes | 64 |

Below is a sample **Set Asset Script** encoded as **JSON**:

```cpp
{
    "type" : 15,
    "id" : "EXDKRNL5Apiw3K9mvLjPVNTWRhDwEvzeA9GAXSrYfQsh",
    "assetId" : "L5Apiw3K9mvLjPVNTWRhDwEvzeA9GAEXDKRNXSrYfQsh",
    "sender" : "3N9dfiTb8Pd6hqhvXaf8GcdTxdwCAeyxsvr",
    "senderPublicKey" : "6gT9PnyXA2sQ9AyRYn1QqkquWSu44Hr3qzLxszchTD1J",
    "fee" : 100000000,
    "timestamp" : 1535102049904,
    "proofs" : [ "4QwRFUNZUk7KaWGnmnYp6pUqUrLjZk3hFwhQTaJN7SUAYDvmXVkU4DDWadH5pQWkaUYiAdCQFtqSKZyKwyaUdyUN" ],
    "version" : 1,
    "script" : "base64:AQQAAAALYWxpY2FANpZ25lZAUAAAAJYm9iU2lnbmVkB5fCpHI"
}
```

## Network messages

### Network message structure

All network messages shares the same structure except the Handshake.

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Payload | Bytes | N |

Magic Bytes are 0x12, 0x34, 0x56, 0x78. Payload checksum is first 4 bytes of\_FastHash\_of Payload bytes. FastHash is hash function Blake2b256\(data\).

### Handshake message

Handshake is used to start communication between two nodes.

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Application name length \(N\) | Byte | 1 |
| 2 | Application name \(UTF-8 encoded bytes\) | Bytes | N |
| 3 | Application version major | Int | 4 |
| 4 | Application version minor | Int | 4 |
| 5 | Application version patch | Int | 4 |
| 6 | Node name length \(M\) | Byte | 1 |
| 7 | Node name \(UTF-8 encoded bytes\) | Bytes | M |
| 8 | Node nonce | Long | 8 |
| 9 | Declared address length \(K\) or 0 if no declared address was set | Int | 4 |
| 10 | Declared address bytes \(if length is not 0\) | Bytes | K |
| 11 | Timestamp | Long | 8 |

### GetPeers message

GetPeers message is sent when sending node wants to know of other nodes on network.

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x01\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |

### Peers message

Peers message is a reply on GetPeers message.

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x02\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Peers count \(N\) | Int | 4 |
| 7 | Peer \#1 IP address | Bytes | 4 |
| 8 | Peer \#1 port | Int | 4 |
| ... | ... | ... | ... |
| 6 + 2 \* N - 1 | Peer \#N IP address | Bytes | 4 |
| 6 + 2 \* N | Peer \#N port | Int | 4 |

### GetSignatures message

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x14\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Block IDs count \(N\) | Int | 4 |
| 7 | Block \#1 ID | Bytes | 64 |
| ... | ... | ... | ... |
| 6 + N | Block \#N ID | Bytes | 64 |

### Signatures message

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x15\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Block signatures count \(N\) | Int | 4 |
| 7 | Block \#1 signature | Bytes | 64 |
| ... | ... | ... | ... |
| 6 + N | Block \#N signature | Bytes | 64 |

### GetBlock message

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x16\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Block ID | Bytes | 64 |

### Block message

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x17\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Block bytes \(N\) | Bytes | N |

### Score message

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x18\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Score \(N bytes\) | BigInt | N |

### Transaction message

| \# | Field name | Type | Length |
| :--- | :--- | :--- | :--- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x19\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Transaction \(N bytes\) | Bytes | N |

### Checkpoint message

| \# | Field name | Type | Length |
| --- | --- | --- | --- |
| 1 | Packet length \(BigEndian\) | Int | 4 |
| 2 | Magic Bytes | Bytes | 4 |
| 3 | Content ID \(0x64\) | Byte | 1 |
| 4 | Payload length | Int | 4 |
| 5 | Payload checksum | Bytes | 4 |
| 6 | Checkpoint items count \(N\) | Int | 4 |
| 7 | Checkpoint \#1 height | Long | 8 |
| 8 | Checkpoint \#1 signature | Bytes | 64 |
| ... | ... | ... | ... |
| 6 + 2 \* N - 1 | Checkpoint \#N height | Long | 8 |
| 6 + 2 \* N | Checkpoint \#N signature | Bytes | 64 |



