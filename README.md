# fio.validate

The following outlines the structure of the presale and token allocation data in the .csv files and the actions that need to be performed to load them during startup.
## File format
Data will be provided in csv file in the following format:
* Type
  * single - transfer to a single key account
  * msig - transfer to msig
  * presale - accounts are created and token deposited for presale or address giveaway accounts
* FIO public key(s) - pipe-delimited
  * Type: single
      * Single FIO Public Key
  * Type: msig
      * Msig account’s private key
      * Msig account’s public key
      * Public keys which constitute the msig
  * Type: presale
      * FIO Private key
      * FIO Public key
      * Foundation pub key for permissions
* Multisig threshold (if fio or msig, else 0)
* Amount of locked (in SUFs) tokens. This should be used for lock schedule. Entries with lock type 0 will have 0 here.
* Amount of tokens (in SUFs) to transfer. Some entries will have a 0, which means account and locks should be created but no tokens will be transferred. Tokens for those accounts will be transferred by Dapix after Mainnet.
* Lock type
  * 0 - no lock
  * 1 
  * 2
  * 3
  * 4

## Step M1
For each entry in file:
* (if type=single or type=presale) An account has to be created
* (if type=msig) Multisig has to be created
  * Use private/public key specified and create account for it using FIO way. This will be the msig account.
  * Accounts for each provided key has to be created using FIO way.
  * Permissions for owner and active should be replaced in msig account with accounts generated from provided keys
* (if type=presale) Permissions for owner and active should be replaced account generated from provided key
* (if lock type 1 or 2 or 3 or 4) Token lock entry has to be created
* (if amount > 0) Tokens need to be minted and transferred to account

## Step M2
FIO Domains from Pre-sale will be allocated to designated FIO public keys. A final csv will contain:
* FIO Domain
* FIO public key

For each entry:

* An account has to be created
* FIO Domain is created and assigned to that account with standard expiration date

## Step M4
FIO Addresses from Pre-sale will be allocated to designated FIO public keys. A final csv will contain:
* FIO Address
* FIO public key

For each entry:
* An account has to be created
* FIO Address is assigned to that account with standard expiration date and bundled transactions, but with no registration fee charged
