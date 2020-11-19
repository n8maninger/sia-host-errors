# Important Log Items

## host has reached its collateral budget and cannot accept the file contract
Your host has reached its maximum collateral budget. Restart Sia to clear stale contracts or increase collateral budget

## wallet must be unlocked before it can be used
Your wallet is locked or scanning. Unlock your wallet or wait for it to finish scanning

## not enough storage remaining to accept sector
One or more of your host storage folders is inaccessible. Check your storage folders and make sure they are visible to Sia

# Renter/Host Communication Issues
These are purely informational and occur during communication with renters.

## challenge signature is invalid
Occurs when the renter fails to prove that they own the contract they are trying to update. 

## bad signature from renter: invalid signature
Occurs when the renter fails to prove that they own the contract they are trying to update. 

## length 1234 exceeds maxLen of
## encoded object exceeded allocation limit by
Occurs when the renter has sent more data than expected  

# Price Table Log Items
Price tables are an agreement between the host and a renter to transact at a certain price. The price table is valid for 10 minutes, after which the renter must update their price table. In most cases these do not indicate an issue with your host.

## Price table requested is expired
The renter tried to use a price table, but it had already expired.

## Price table not found
The renter tried to use a price table unknown to the host. This can occur if the renter did not pay for the price table update.

## File Contract Log Items
The log lines below can occur when renters and hosts revise the file contract. In most cases these do not indicate an issue with your host.

## the requested file contract is currently locked
To revise a contract it has to be locked, a renter attempted to use a file contract that was already locked. This could inidicate failure to unlock a contract after disconnect, but it's more likely an issue from the renter.

## renter has provided an incorrectly sized sector
The renter tried to upload a sector that did not match the host's sector size \[4MiB\]

## transaction has a file contract with an outdated revision number
Usually, the host submits the last contract revision to the block chain in order to get payed, however the renter can also submit the last revision to ensure the host is penalized if it does not meet its obligation. This occurs if the renter has already submitted the same revision the host is attempting to submit or that the host has an older revision, which under normal circumstances should not be possible. The host may still attempt to submit a proof if they are able.

## could not find the desired sector
Occurs when a renter requests data that is not available on the host. This has started occuring a lot more since Skynet portals attempt to download data from every host if it does not know which hosts are storing the Skylink. Usually not an issue.

## storage obligation not found in database
Occurs if the renter tried to use a file contract that the host does not know about.

## download request has invalid sector bounds
Occurs if the renter tried to request a section of a sector that is greater than the host's sector size \[4MiB\]

# Contract Revision Log Items
Both the renter and the host must agree and sign a contract revision for it to be valid, these occur when the renter and the host have a dispute on one of those revisions. They usually occurs if the renter and host are on different block heights.

A storage contract has 3 lifecycle events: creation, revision, and finalization. Creation occurs when the renter and host agree to create a storage contract and lock allowance and collateral into it. Revision occurs when the renter and host agree to revise the contract through upload, download, or funding an ephemeral account. Finalization occurs when the renter or host submits the final revision to the blockchain, indicating the contract will no longer be updated. After finalization, during the contract's proof window, a host can determine whether a storage proof needs to be submitted. If the host submits a valid storage proof the contract's valid proof outputs are created, otherwise the missed outputs are created. There are situations where it is not in the host's best interest to submit a storage proof, so not submiting a proof does not necessarily indicate failure.

### Valid Proof Outputs
+ Renter returned allowance
+ Host revenue + returned collateral

### Missed Proof Outputs
+ Renter returned allowance
+ Host returned collateral
+ Renter burned allowance + host burned collateral

## renter is requesting revision after the revision deadline
The renter has tried to revise a contract after it has expired and during the proof period.

## rejected for bad revision number
Contracts have a revision number that must always increase, occurs when the renter attempted to revise an old version of the contract.

## rejected for including too few transaction fees
Occurs when the renter provides a transaction that the host does not feel can actually be confirmed on the blockchain due to transaction fees.

## rejected for low paying host missed output
Occurs when the renter submitted a revision that has the host posting more collateral than it should.

## rejected for low paying host valid output
Occurs when the renter submits a revision that does not pay the host enough.

## rejected for high paying renter valid output
This occurs if the renter submits a revision that did not transfer enough money from the renter's allowance.

## rejected for low value void output
This occurs if the renter submits a revision that does not burn enough allowance if the host fails

## rejected for bad file size
Occurs when the renter submits a revision with a data size that does not make sense or the fdataile size was not updated.

## rejected for having an unexpected number of outputs
Contracts in most situations should have 2 valid proof outputs and 3 missed proof outputs. There are situations where there are only 2 missed proof outputs on a contract. This occurs if the renter submits a revision that does not contain the expected number of outputs.

## rejected for small window size
This occurs if the contract's proof window is less than the host's minimum window duration \[144 blocks\]

## rejected for a window that starts too soon
This occurs when a renter attempts to create a contract where the proof window starts too soon. The proof window, by default, must be at least 20 blocks away.

## rejected for bad file merkle root
The merkle root is used to prove that the host correctly stored the data using merkle proofs. This occurs if the renter changed the contract's merkle root during a download revision or gave a different than expected merkle root during an upload revision. 

## renter proposed a file contract with a too-long duration
This occurs if the file contract's duration is longer than the host's max duration. Increasing `maxduration` may reduce the occurence, but your host is payed at the end of the file contract so may not be ideal.

## file contract proposal expects the host to pay more than the maximum allowed collateral
This occurs when a renter attempts to lock more collateral into a single contract then the host allows. Adjusting `maxcollateral` may reduce the occurence, but your host may lock more funds into contracts that aren't necessarily going to be used. About 4TB worth of collateral is a good maximum.

# Contract State Logs

## file contract complete, id 

## No need to submit a storage proof for the contract. Revenue is

## Successfully submitted a storage proof. Revenue is

## No need to submit a storage proof the contract. Revenue is

## Missed storage proof. Revenue would have been

# Ephemeral Account Logs
Ephemeral accounts are used for quicker interactions between a renter and host. The renter funds an ephemeral account using a file contract, after funding the ephemeral account can be used to transact with the host without needing to update or lock the file contract allowing for high parallelism and better performance.

## ephemeral account maximam balance exceeded
The renter tried to deposit more money than the host allows, this is normally not a problem as ephemeral accounts can be refilled quickly and easily. There is a `maxephemeralaccountbalance` setting, but the current guidance from the core team is to leave it at the default \[1SC\].

## ephemeral account withdrawals are inactive because the host is not synced
Ephemeral account withdrawals are not available until the consensus and host module are both synced. Usually just need to wait until everything is ready, but may be good to check that you have peers.

## unknown payment method
The renter tried to use an invalid payment method to fund the ephemeral account, currently ephemeral accounts can only be funded through contracts.

## ephemeral account withdrawal message expired
Withdrawal requests must be signed and timestamped with an expiration block height. Occurs when the renter has tried to send a withdrawal request after it has expired.

## ephemeral account deposit cancelled due to a shutdown
Occurs when the host was shutdown in the middle of an ephemeral deposit request

## ephemeral account withdrawal cancelled due to a shutdown
Occurs when the host was shutdown in the middle of an ephemeral deposit request

## ephemeral account withdrawal message expires too far into the future
Occurs when the expiration of a withdrawal request is too far into the future \[20 blocks\]

# Syncing Log Items
Sync issues can happen in distributed networks, usually just waiting for the next block resolves the issue.

## wallet has coins spent in incomplete transactions - not enough remaining coins
Occurs when the wallet has spent all of its confirmed outputs, waiting one block for confirmations should resolve the issue.

## Consensus conflict on the origin transaction set, id
Most likely occurs if the host is not fully synced, check your peers and your sync height

## transaction spends a nonexisting siacoin output
This occurs when the payment for a contract formation or revision has a non-existing siacoin output. Usually a syncing issue, and most likely an issue on the renter side. Should resolve itself in a few blocks if the host is synced to the correct blockchain.

## siacoin inputs do not equal siacoin outputs for transaction
A valid transaction must spend all of its input value, either through returning change to the wallet or using it for the file contract. This occurs when the payment for a contract formation or revision has more input money then it outputs. Most likely on the renter side, this has started happening more often as people experiment with custom Sia implementations.

## transaction set is too large for this transaction pool
Occurs when a transaction set is too large to be confirmed on the Sia blockchain. A transaction set must be less than 25000 bytes. This usually occurs when a wallet is extremely fragmented and needs to be defragmented.

## transaction set contains only duplicate transactions
Occurs when a transaction set has already been broadcast, in full, to the network.

# Registry Log Errors
These errors are specific to the Skynet registry.

## registered data is too large
The data stored in a single registry entry can not be more than 113 bytes

## marshaled entry has wrong size
This occurs when a renter has submitted a registry entry that is not exactly 256 bytes, usually indicating an invalid format.

## provided revision number is invalid
This occurs when a renter submits an update to a registry entry with a revision number less than the existing entry.

## provided revision number is already registered
This occurs when a renter submits an update to a registry entry with the same revision number as the existing entry

## provided signature is invalid
This occurs when a renter submits an update to the registry entry with an invalid signature, indicating someone is trying to update the entry using the wrong key.

# Generic Communication Errors
The errors below will make up most of the log lines. They are safe to ignore for the most part, but are included for completeness.

+ EOF
+ i/o timeout
+ read/write on closed pipe
+ write: broken pipe
+ use of closed network connection
+ connection reset by peer
+ boolean value was not 0 or 1
+ stream timed out
+ failed to flush bufferstream timed out
+ invalid or unknown RPC ID
+ chacha20poly1305: message authentication failed

# UPNP Warnings
UPNP allows Sia to forward ports automatically. It's not very reliable and requires router support. These can be ignored if you setup a static IP and forwarded ports to your host manually.

+ no UPnP-enabled gateway found
+ WARN: could not automatically forward port
