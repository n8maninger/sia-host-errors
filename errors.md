# Important Log Items

## host has reached its collateral budget and cannot accept the file contract

### Reasons
+ Your host has reached its maximum collateral budget

### Resolution
+ Restart Sia to clear stale contracts
+ Increase collateral budget

## wallet must be unlocked before it can be used

### Reasons
+ Your wallet is locked or scanning

### Resolution
+ Unlock your wallet or wait for it to finish scanning

## not enough storage remaining to accept sector

### Reasons
+ One or more of your host storage folders is inaccessible

### Resolution
+ Check your storage folders and make sure they are visible to Sia

# Generic Communication Errors

These are safe to ignore for the most part

## EOF
## i/o timeout
## read/write on closed pipe
## write: broken pipe
## use of closed network connection
## connection reset by peer
## boolean value was not 0 or 1
## stream timed out
## failed to flush bufferstream timed out
## challenge signature is invalid
## invalid or unknown RPC ID
## chacha20poly1305: message authentication failed

# Renter/Host Communication Issues

## length 10095 exceeds maxLen of 4096

### Reasons
TODO

## encoded object exceeded allocation limit by

### Reasons
TODO

## Price table requested is expired

### Reasons
TODO

## Price table not found

### Reasons
TODO

## the requested file contract is currently locked

### Reasons
TODO

## renter has provided an incorrectly sized sector

### Reasons
TODO

## rejected for bad revision number

### Reasons
TODO

## transaction has a file contract with an outdated revision number

### Reasons
TODO

## cannot fetch storage proof segment for unknown file contract

### Reasons
TODO

## could not find the desired sector

### Reasons
TODO

## storage obligation not found in database

### Reasons
TODO

## download request has invalid sector bounds

### Reasons
TODO

## host supplied invalid Merkle proof

### Reasons
TODO

## Ephemeral Account Logs

## ephemeral account maximam balance exceeded

### Reasons
TODO

## ephemeral account withdrawals are inactive because the host is not synced

### Reasons
TODO

## unknown payment method

### Reasons
TODO

## ephemeral account withdrawal message expired

### Reasons
TODO

## ephemeral account deposit cancelled due to a shutdown

### Reasons
TODO

## ephemeral account withdrawal cancelled due to a shutdown

### Reasons
TODO

## ephemeral account withdrawal message expires too far into the future

### Reasons
TODO

# Consensus Sync Log Items

## wallet has coins spent in incomplete transactions - not enough remaining coins

### Reasons
TODO

## Consensus conflict on the origin transaction set, id

### Reasons
TODO

## transaction spends a nonexisting siacoin output

### Reasons
TODO

## siacoin inputs do not equal siacoin outputs for transaction

### Reasons
TODO

# Transaction Pool Log Items

## transaction set is too large for this transaction pool

### Reasons
TODO

## transaction set contains only duplicate transactions

### Reasons
TODO

# Contract Revision Log Items

## renter is requesting revision after the revision deadline

### Reasons
TODO

## rejected for including too few transaction fees

### Reasons
TODO

## rejected for low paying host missed output

### Reasons
TODO

## rejected for low paying host valid output

### Reasons
TODO

## rejected for high paying renter valid output

### Reasons
TODO

## rejected for low value void output

### Reasons
TODO

## rejected for bad file size

### Reasons
TODO

## rejected for having an unexpected number of outputs

### Reasons
TODO

## rejected for small window size

### Reasons
TODO

## rejected for a window that starts too soon

### Reasons
TODO

## file contract proposal expects the host to pay more than the maximum allowed collateral

### Reasons
TODO

## Rejecting storage obligation expiring at block XXXXXX, current height is XXXXXX

### Reasons
TODO

## renter proposed a file contract with a too-long duration

### Reasons
TODO

## rejected for bad file merkle root

### Reasons
TODO

## Full time has elapsed, but the revision transaction could not be submitted to consensus

### Reasons
TODO

## invalid signature

### Reasons
TODO

# Contract State Logs

## file contract complete, id 

### Reasons
TODO

## No need to submit a storage proof for the contract. Revenue is

### Reasons
TODO

## Successfully submitted a storage proof. Revenue is

### Reasons
TODO

## No need to submit a storage proof the contract. Revenue is

### Reasons
TODO

## Missed storage proof. Revenue would have been

### Reasons
TODO

# UPNP Warnings

## no UPnP-enabled gateway found

### Reasons
TODO

### Resolution
TODO

## WARN: could not automatically forward port

### Reasons
TODO

### Resolution
TODO
