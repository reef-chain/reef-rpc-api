# Reef Chain RPC API

- **[author](#author)**

- **[chain](#chain)**

- **[childstate](#childstate)**

- **[evm](#evm)**

- **[grandpa](#grandpa)**

- **[offchain](#offchain)**

- **[payment](#payment)**

- **[rpc](#rpc)**

- **[state](#state)**

- **[system](#system)**

Example of json rpc call:
```curl -H "Content-Type: application/json" -d '{"id":1, "jsonrpc":"2.0", "method": "rpc_methods"}' https://rpc.reefscan.com```
___


## author
 
### hasKey(publicKey: `Bytes`, keyType: `Text`): `bool`
- **jsonrpc**: `author_hasKey`
- **summary**: Returns true if the keystore has private keys for the given public key and key type.
 
### hasSessionKeys(sessionKeys: `Bytes`): `bool`
- **jsonrpc**: `author_hasSessionKeys`
- **summary**: Returns true if the keystore has private keys for the given session public keys.
 
### insertKey(keyType: `Text`, suri: `Text`, publicKey: `Bytes`): `Bytes`
- **jsonrpc**: `author_insertKey`
- **summary**: Insert a key into the keystore.
 
### pendingExtrinsics(): `Vec<Extrinsic>`
- **jsonrpc**: `author_pendingExtrinsics`
- **summary**: Returns all pending extrinsics, potentially grouped by sender
 
### removeExtrinsic(bytesOrHash: `Vec<ExtrinsicOrHash>`): `Vec<Hash>`
- **jsonrpc**: `author_removeExtrinsic`
- **summary**: Remove given extrinsic from the pool and temporarily ban it to prevent reimporting
 
### submitAndWatchExtrinsic(extrinsic: `Extrinsic`): `ExtrinsicStatus`
- **jsonrpc**: `author_submitAndWatchExtrinsic`
- **summary**: Submit and subscribe to watch an extrinsic until unsubscribed
 
### submitExtrinsic(extrinsic: `Extrinsic`): `Hash`
- **jsonrpc**: `author_submitExtrinsic`
- **summary**: Submit a fully formatted extrinsic for block inclusion

### unwatchExtrinsic(id: `SubscriptionId`): `bool`
- **jsonrpc**: `author_unwatchExtrinsic`
- **summary**: Unsubscribe from extrinsic watching

___


## chain
 
### getHead(blockNumber?: `BlockNumber`): `BlockHash`
- **jsonrpc**: `chain_getHead`/`chain_getBlockHash`
- **summary**: Get the block hash for a specific block

### getBlock(hash?: `BlockHash`): `SignedBlock`
- **jsonrpc**: `chain_getBlock`
- **summary**: Get header and body of a relay chain block
 
### getFinalizedHead(): `BlockHash`
- **jsonrpc**: `chain_getFinalizedHead`/`chain_getFinalisedHead`
- **summary**: Get hash of the last finalized block in the canon chain
 
### getHeader(hash?: `BlockHash`): `Header`
- **jsonrpc**: `chain_getHeader`
- **summary**: Retrieves the header for a specific block

### getRuntimeVersion(at?: `BlockHash`): `RuntimeVersion`
- **jsonrpc**: `chain_getRuntimeVersion`
- **summary**: Get the runtime version
 
### subscribeAllHeads(): `Header`
- **jsonrpc**: `chain_subscribeAllHeads`
- **summary**: Retrieves the newest header via subscription
 
### subscribeFinalizedHeads(): `Header`
- **jsonrpc**: `chain_subscribeFinalizedHeads`/`chain_subscribeFinalisedHeads`
- **summary**: Retrieves the best finalized header via subscription
 
### subscribeNewHead(): `Header`
- **jsonrpc**: `chain_subscribeNewHeads`/`chain_subscribeNewHead`/`subscribe_newHead`
- **summary**: Retrieves the best header via subscription

### subscribeRuntimeVersion(): `RuntimeVersion`
- **jsonrpc**: `chain_subscribeRuntimeVersion`
- **summary**: Retrieves the runtime version via subscription

### unsubscribeAllHeads(id: `SubscriptionId`): `bool`
- **jsonrpc**: `chain_unsubscribeAllHeads`
- **summary**: Unsubscribe all heads

### unsubscribeFinalizedHeads(id: `SubscriptionId`): `bool`
- **jsonrpc**: `chain_unsubscribeFinalizedHeads`/`chain_unsubscribeFinalisedHeads`
- **summary**: Unsubscribe finalized heads

### unsubscribeNewHeads(id: `SubscriptionId`): `bool`
- **jsonrpc**: `chain_unsubscribeNewHead`/`chain_unsubscribeNewHeads`/`unsubscribe_newHead`
- **summary**: Unsubscribe new heads

### unsubscribeRuntimeVersion(id: `SubscriptionId`): `bool`
- **jsonrpc**: `chain_unsubscribeRuntimeVersion`
- **summary**: Unsubscribe runtime version

___


## childstate
 
### getKeys(childKey: `PrefixedStorageKey`, prefix: `StorageKey`, at?: `Hash`): `Vec<StorageKey>`
- **jsonrpc**: `childstate_getKeys`
- **summary**: Returns the keys with prefix from a child storage, leave empty to get all the keys
 
### getKeysPaged(childKey: `PrefixedStorageKey`, prefix: `StorageKey`, count: `u32`, startKey?: `StorageKey`, at?: `Hash`): `Vec<StorageKey>`
- **jsonrpc**: `childstate_getKeysPaged`/`childstate_getKeysPagedAt`
- **summary**: Returns the keys with prefix from a child storage with pagination support
 
### getStorage(childKey: `PrefixedStorageKey`, key: `StorageKey`, at?: `Hash`): `Option<StorageData>`
- **jsonrpc**: `childstate_getStorage`
- **summary**: Returns a child storage entry at a specific block state
 
### getStorageHash(childKey: `PrefixedStorageKey`, key: `StorageKey`, at?: `Hash`): `Option<Hash>`
- **jsonrpc**: `childstate_getStorageHash`
- **summary**: Returns the hash of a child storage entry at a block state
 
### getStorageSize(childKey: `PrefixedStorageKey`, key: `StorageKey`, at?: `Hash`): `Option<u64>`
- **jsonrpc**: `childstate_getStorageSize`
- **summary**: Returns the size of a child storage entry at a block state

___


## evm

### call(data: `CallRequest`, at?: `BlockHash`): `Bytes`
- **jsonrpc**: `evm_call`
- **summary**: Call contract, returning the output data.

### estimateGas(data: `CallRequest`, at?: `BlockHash`): `U128`
- **jsonrpc**: `evm_estimateGas`
- **summary**: Estimate gas needed for execution of given contract.

### estimateResources(from: `H160`, unsignedExtrinsic: `Bytes`, at?: `BlockHash`): `EstimateResourcesResponse`
- **jsonrpc**: `evm_estimateResources`
- **summary**: Estimate resources needed for execution of given contract.

___


## grandpa
 
### proveFinality(blockNumber: `BlockNumber`): `Option<EncodedFinalityProofs>`
- **jsonrpc**: `grandpa_proveFinality`
- **summary**: Prove finality for the given block number, returning the Justification for the last block in the set.
 
### roundState(): `ReportedRoundStates`
- **jsonrpc**: `grandpa_roundState`
- **summary**: Returns the state of the current best round state as well as the ongoing background rounds
 
### subscribeJustifications(): `JustificationNotification`
- **jsonrpc**: `grandpa_subscribeJustifications`
- **summary**: Subscribes to grandpa justifications

### unsubscribeJustifications(id: `SubscriptionId`): `bool`
- **jsonrpc**: `grandpa_unsubscribeJustifications`
- **summary**: Unsubscribe to grandpa justifications

___


## offchain
 
### localStorageGet(kind: `StorageKind`, key: `Bytes`): `Option<Bytes>`
- **jsonrpc**: `offchain_localStorageGet`
- **summary**: Get offchain local storage under given key and prefix
 
### localStorageSet(kind: `StorageKind`, key: `Bytes`, value: `Bytes`): `Null`
- **jsonrpc**: `offchain_localStorageSet`
- **summary**: Set offchain local storage under given key and prefix

___


## payment
 
### queryFeeDetails(extrinsic: `Bytes`, at?: `BlockHash`): `FeeDetails`
- **jsonrpc**: `payment_queryFeeDetails`
- **summary**: Query the detailed fee of a given encoded extrinsic
 
### queryInfo(extrinsic: `Bytes`, at?: `BlockHash`): `RuntimeDispatchInfoV1`
- **jsonrpc**: `payment_queryInfo`
- **summary**: Retrieves the fee information for an encoded extrinsic

___


## rpc
 
### methods(): `RpcMethods`
- **jsonrpc**: `rpc_methods`
- **summary**: Retrieves the list of RPC methods that are exposed by the node

___


## state
 
### call(method: `Text`, data: `Bytes`, at?: `BlockHash`): `Bytes`
- **jsonrpc**: `state_call`/`state_callAt`
- **summary**: Perform a call to a builtin on the chain
 
### getChildReadProof(childStorageKey: `PrefixedStorageKey`, keys: `Vec<StorageKey>`, at?: `BlockHash`): `ReadProof`
- **jsonrpc**: `state_getChildReadProof`
- **summary**: Returns proof of storage for child key entries at a specific block state.
 
### getKeys(key: `StorageKey`, at?: `BlockHash`): `Vec<StorageKey>`
- **jsonrpc**: `state_getKeys`
- **summary**: Retrieves the keys with a certain prefix
 
### getKeysPaged(key: `StorageKey`, count: `u32`, startKey?: `StorageKey`, at?: `BlockHash`): `Vec<StorageKey>`
- **jsonrpc**: `state_getKeysPaged`/`state_getKeysPagedAt`
- **summary**: Returns the keys with prefix with pagination support.
 
### getMetadata(at?: `BlockHash`): `Metadata`
- **jsonrpc**: `state_getMetadata`
- **summary**: Returns the runtime metadata
 
### getPairs(prefix: `StorageKey`, at?: `BlockHash`): `Vec<KeyValue>`
- **jsonrpc**: `state_getPairs`
- **summary**: Returns the keys with prefix, leave empty to get all the keys (deprecated: Use getKeysPaged)
 
### getReadProof(keys: `Vec<StorageKey>`, at?: `BlockHash`): `ReadProof`
- **jsonrpc**: `state_getReadProof`
- **summary**: Returns proof of storage entries at a specific block state
 
### getRuntimeVersion(at?: `BlockHash`): `RuntimeVersion`
- **jsonrpc**: `state_getRuntimeVersion`
- **summary**: Get the runtime version
 
### getStorage(key: `StorageKey`, at?: `BlockHash`): `StorageData`
- **jsonrpc**: `state_getStorage`/`state_getStorageAt`
- **summary**: Retrieves the storage for a key
 
### getStorageHash(key: `StorageKey`, at?: `BlockHash`): `Hash`
- **jsonrpc**: `state_getStorageHash`/`state_getStorageHashAt`
- **summary**: Retrieves the storage hash
 
### getStorageSize(key: `StorageKey`, at?: `BlockHash`): `u64`
- **jsonrpc**: `state_getStorageSize`/`state_getStorageSizeAt`
- **summary**: Retrieves the storage size
 
### queryStorage(keys: `Vec<StorageKey>`, fromBlock: `Hash`, toBlock?: `BlockHash`): `Vec<StorageChangeSet>`
- **jsonrpc**: `state_queryStorage`
- **summary**: Query historical storage entries (by key) starting from a start block
 
### queryStorageAt(keys: `Vec<StorageKey>`, at?: `BlockHash`): `Vec<StorageChangeSet>`
- **jsonrpc**: `state_queryStorageAt`
- **summary**: Query storage entries (by key) starting at block hash given as the second parameter
 
### subscribeRuntimeVersion(): `RuntimeVersion`
- **jsonrpc**: `state_subscribeRuntimeVersion`
- **summary**: Retrieves the runtime version via subscription
 
### subscribeStorage(keys?: `Vec<StorageKey>`): `StorageChangeSet`
- **jsonrpc**: `state_subscribeStorage`
- **summary**: Subscribes to storage changes for the provided keys
 
### traceBlock(block: `Hash`, targets: `Option<Text>`, storageKeys: `Option<Text>`, methods: `Option<Text>`): `TraceBlockResponse`
- **jsonrpc**: `state_traceBlock`
- **summary**: Provides a way to trace the re-execution of a single block
  
### unsubscribeRuntimeVersion(id: `SubscriptionId`): `bool`
- **jsonrpc**: `state_unsubscribeRuntimeVersion`
- **summary**: Unsubscribe runtime version

### unsubscribeStorage(id: `SubscriptionId`): `bool`
- **jsonrpc**: `state_unsubscribeStorage`
- **summary**: Unsubscribe state storage changes

___


## system
 
### accountNextIndex(accountId: `AccountId`): `Index`
- **jsonrpc**: `system_accountNextIndex`/`account_nextIndex`
- **summary**: Retrieves the next accountIndex as available on the node
 
### addLogFilter(directives: `Text`): `Null`
- **jsonrpc**: `system_addLogFilter`
- **summary**: Adds the supplied directives to the current log filter
 
### addReservedPeer(peer: `Text`): `Text`
- **jsonrpc**: `system_addReservedPeer`
- **summary**: Adds a reserved peer
 
### chain(): `Text`
- **jsonrpc**: `system_chain`
- **summary**: Retrieves the chain
 
### chainType(): `ChainType`
- **jsonrpc**: `system_chainType`
- **summary**: Retrieves the chain type
 
### dryRun(extrinsic: `Bytes`, at?: `BlockHash`): `ApplyExtrinsicResult`
- **jsonrpc**: `system_dryRun`/`system_dryRunAt`
- **summary**: Dry run an extrinsic at a given block
 
### health(): `Health`
- **jsonrpc**: `system_health`
- **summary**: Return health status of the node
 
### localListenAddresses(): `Vec<Text>`
- **jsonrpc**: `system_localListenAddresses`
- **summary**: The addresses include a trailing /p2p/ with the local PeerId, and are thus suitable to be passed to addReservedPeer or as a bootnode address for example
 
### localPeerId(): `Text`
- **jsonrpc**: `system_localPeerId`
- **summary**: Returns the base58-encoded PeerId of the node
 
### name(): `Text`
- **jsonrpc**: `system_name`
- **summary**: Retrieves the node name
 
### nodeRoles(): `Vec<NodeRole>`
- **jsonrpc**: `system_nodeRoles`
- **summary**: Returns the roles the node is running as
 
### properties(): `ChainProperties`
- **jsonrpc**: `system_properties`
- **summary**: Get a custom set of properties as a JSON object, defined in the chain spec
 
### removeReservedPeer(peerId: `Text`): `Text`
- **jsonrpc**: `system_removeReservedPeer`
- **summary**: Remove a reserved peer
 
### reservedPeers(): `Vec<Text>`
- **jsonrpc**: `system_reservedPeers`
- **summary**: Returns the list of reserved peers
 
### syncState(): `SyncState`
- **jsonrpc**: `system_syncState`
- **summary**: Returns the state of the syncing of the node
 
### version(): `Text`
- **jsonrpc**: `system_version`
- **summary**: Retrieves the version of the node
