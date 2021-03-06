::: api__content__body
# API Reference

At LBRY, we utilize JSON-RPC for our API.
:::

::: api__content__example
```
This is a work-in-progress!
```
:::



::: api__content__body
## blob_announce

Announce blobs to the DHT.
:::

::: api__content__example
Returns:

```
(bool) true if successful
```

Arguments:

| Parameter   | Description                                                               |
|:------------|:--------------------------------------------------------------------------|
| blob_hash   | (str) announce a blob, specified by blob hash                             |
| sd_hash     | (str) announce all blobs associated with `sd_hash` and the sd hash itself |
| stream_hash | (str) announce all blobs associated with `stream_hash`                    |
:::



::: api__content__body
## blob_availability

Get blob availability.
:::

::: api__content__example
Returns:

```
(dict) {
  "is_available": <bool, true if blob is available from a peer from peer list>
  "reachable_peers": ["<ip>:<port>"],
  "unreachable_peers": ["<ip>:<port>"]
}
```

Arguments:

| Parameter      | Description                                                |
|:---------------|:-----------------------------------------------------------|
| blob_hash      | (str) check availability for this blob hash                |
| blob_timeout   | (int) how long to try downloading from a peer              |
| search_timeout | (int) how long to search for peers for the blob in the dht |
:::



::: api__content__body
## blob_delete

Delete a blob.
:::

::: api__content__example
Returns:

```
(str) Success/fail message
```

Arguments:

| Parameter   | Description                           |
|:------------|:--------------------------------------|
| blob_hash   | (str) blob hash of the blob to delete |
:::



::: api__content__body
## blob_get

Download and return a blob.
:::

::: api__content__example
Returns:

```
(str) Success/Fail message or (dict) decoded data
```

Arguments:

| Parameter            | Description                                                                                                        |
|:---------------------|:-------------------------------------------------------------------------------------------------------------------|
| blob_hash *required* | (str) blob hash of the blob to get                                                                                 |
| encoding             | (str) by default no attempt at decoding is made, can be set to one of the following decoders: "json"               |
| payment_rate_manager | (str) if not given the default payment rate manager will be used. Supported alternative rate managers: "only-free" |
| timeout              | (int) timeout in number of seconds                                                                                 |
:::



::: api__content__body
## blob_list

Returns blob hashes. If not given filters, returns all blobs known by the blob manager.
:::

::: api__content__example
Returns:

```
(list) List of blob hashes
```

Arguments:

| Parameter   | Description                           |
|:------------|:--------------------------------------|
| finished    | (bool) only return finished blobs     |
| needed      | (bool) only return needed blobs       |
| page        | (int) page of results to return       |
| page_size   | (int) results page size               |
| sd_hash     | (str) filter blobs by sd hash         |
| stream_hash | (str) filter blobs by stream hash     |
| uri         | (str) filter blobs by stream in a uri |
:::



::: api__content__body
## blob_reflect

Reflects specified blobs.
:::

::: api__content__example
Returns:

```
(list) reflected blob hashes
```

Arguments:

| Parameter        | Description             |
|:-----------------|:------------------------|
| reflector_server | (str) reflector address |
:::



::: api__content__body
## blob_reflect_all

Reflects all saved blobs.
:::

::: api__content__example
Returns:

```
(bool) true if successful
```
:::



::: api__content__body
## block_show

Get contents of a block.
:::

::: api__content__example
Returns:

```
(dict) Requested block
```

Arguments:

| Parameter            | Description                          |
|:---------------------|:-------------------------------------|
| blockhash *required* | (str) hash of the block to look up   |
| height *required*    | (int) height of the block to look up |
:::



::: api__content__body
## channel_export

Export serialized channel signing information for a given certificate claim id.
:::

::: api__content__example
Returns:

```
(str) Serialized certificate information
```

Arguments:

| Parameter           | Description                                |
|:--------------------|:-------------------------------------------|
| claim_id *required* | (str) Claim ID to export information about |
:::



::: api__content__body
## channel_import

Import serialized channel signing information (to allow signing new claims to the channel).
:::

::: api__content__example
Returns:

```
(dict) Result dictionary
```

Arguments:

| Parameter                              | Description            |
|:---------------------------------------|:-----------------------|
| serialized_certificate_info *required* | (str) certificate info |
:::



::: api__content__body
## channel_list

Get certificate claim infos for channels that can be published to.
:::

::: api__content__example
Returns:

```
(list) ClaimDict, includes "is_mine" field to indicate if the certificate claim is in the wallet.
```
:::



::: api__content__body
## channel_new

Generate a publisher key and create a new "@" prefixed certificate claim.
:::

::: api__content__example
Returns:

```
(dict) Dictionary containing result of the claim

{
  "claim_id": (str) claim ID of the resulting claim
  "fee": (float) fee paid for the claim transaction
  "nout": (int) nout of the resulting claim
  "tx": (str) hex encoded transaction
  "txid": (str) txid of resulting claim
}
```

Arguments:

| Parameter               | Description                                 |
|:------------------------|:--------------------------------------------|
| amount *required*       | (float) bid amount on the channel           |
| channel_name *required* | (str) name of the channel prefixed with "@" |
:::



::: api__content__body
## claim_abandon

Abandon a name and reclaim credits from the claim.
:::

::: api__content__example
Returns:

```
(dict) Dictionary containing result of the claim

{
  "fee": (float) fee paid for the transaction
  "txid": (str) txid of resulting transaction
}
```

Arguments:

| Parameter   | Description                        |
|:------------|:-----------------------------------|
| claim_id    | (str) id of the claim to abandon   |
| nout        | (int) nout of the claim to abandon |
| txid        | (str) txid of the claim to abandon |
:::



::: api__content__body
## claim_list

List current claims and information about them for a given name.
:::

::: api__content__example
Returns:

```
(dict) State of claims assigned for the name

{
  "claims": (list) list of claims for the name
  [{
    "amount": (float) amount assigned to the claim
    "claim_id": (str) claim ID of the claim
    "effective_amount": (float) total amount assigned to the claim, including supports
    "height": (int) height of block containing the claim
    "nout": (int) nout of the claim
    "permanent_url": (str) permanent url of the claim
    "supports": (list) a list of supports attached to the claim
    "txid": (str) txid of the claim
    "value": (str) the value of the claim
  }],
  "last_takeover_height": (int) the height of last takeover for the name
  "supports_without_claims": (list) supports without any claims attached to them
}
```

Arguments:

| Parameter       | Description                                |
|:----------------|:-------------------------------------------|
| name *required* | (str) name of the claim to list info about |
:::



::: api__content__body
## claim_list_by_channel

Get paginated claims in a channel specified by a channel uri.
:::

::: api__content__example
Returns:

```
{
  resolved channel uri: {
    If there was an error:
    "error": (str) error message

    "claims_in_channel": the total number of results for the channel

    If a page of results was requested:
    "returned_page": page number returned
    "claims_in_channel": [{
      "absolute_channel_position": (int)  claim index number in sorted list of
                                          claims which assert to be part of the
                                          channel
      "address": (str) claim address
      "amount": (float) claim amount
      "claim_id": (str) claim id
      "claim_sequence": (int) claim sequence number
      "decoded_claim": (bool) whether or not the claim value was decoded
      "depth": (int) claim depth
      "effective_amount": (float) claim amount including supports
      "has_signature": (bool) included if decoded_claim
      "height": (int) claim height
      "name": (str) claim name
      "nout": (str) claim nout
      "signature_is_valid": (bool), included if has_signature
      "supports": (list) list of supports [{
        "amount": (float) amount
        "nout": (int) nout
        "txid": (str) txid
      }]
      "txid": (str) claim txid
      "value": ClaimDict if decoded, otherwise hex string
    }]
  }
}
```

Arguments:

| Parameter      | Description                                                                                |
|:---------------|:-------------------------------------------------------------------------------------------|
| page           | (int) which page of results to return where page 1 is the first page, defaults to no pages |
| page_size      | (int) number of results in a page, default of 10                                           |
| uri *required* | (str) uri of the channel                                                                   |
| uris           | (list) uris of the channel                                                                 |
:::



::: api__content__body
## claim_list_mine

List my name claims.
:::

::: api__content__example
Returns:

```
(list) List of name claims owned by user

[{
  "address": (str) address that owns the claim
  "amount": (float) amount assigned to the claim
  "blocks_to_expiration": (int) number of blocks until it expires
  "category": (str) "claim", "update", or "support"
  "claim_id": (str) claim ID of the claim
  "confirmations": (int) number of blocks of confirmations for the claim
  "expiration_height": (int) the block height which the claim will expire
  "expired": (bool) true if expired, false otherwise
  "height": (int) height of the block containing the claim
  "is_spent": (bool) true if claim is abandoned, false otherwise
  "name": (str) name of the claim
  "nout": (int) nout of the claim
  "permanent_url": (str) permanent url of the claim
  "txid": (str) txid of the claim
  "value": (str) value of the claim
}]
```
:::



::: api__content__body
## claim_new_support

Support a name claim.
:::

::: api__content__example
Returns:

```
(dict) Dictionary containing result of the claim

{
  fee: (float) fee paid for the transaction
  nout: (int) nout of the resulting support claim
  txid: (str) txid of resulting support claim
}
```

Arguments:

| Parameter           | Description                        |
|:--------------------|:-----------------------------------|
| amount *required*   | (float) amount of support          |
| claim_id *required* | (str) id of the claim to support   |
| name *required*     | (str) name of the claim to support |
:::



::: api__content__body
## claim_renew

Renew claim(s) or support(s).
:::

::: api__content__example
Returns:

```
(dict) Dictionary where key is the the original claim's outpoint and value is the result of the renewal

{
  "outpoint": {
    "claim_id": (str) claim ID of the resulting claim
    "fee": (float) fee paid for the claim transaction
    "nout": (int) nout of the resulting claim
    "tx": (str) hex encoded transaction
    "txid": (str) txid of resulting claim
  }
}
```

Arguments:

| Parameter           | Description                                                 |
|:--------------------|:------------------------------------------------------------|
| height *required*   | (str) update claims expiring before or at this block height |
| outpoint *required* | (str) outpoint of the claim to renew                        |
:::



::: api__content__body
## claim_send_to_address

Send a name claim to an address.
:::

::: api__content__example
Returns:

```
(dict) Dictionary containing result of the claim

{
  "claim_id": (str) claim ID of the resulting claim
  "fee": (float) fee paid for the claim transaction
  "nout": (int) nout of the resulting claim
  "tx": (str) hex encoded transaction
  "txid": (str) txid of resulting claim
}
```

Arguments:

| Parameter           | Description                                                                            |
|:--------------------|:---------------------------------------------------------------------------------------|
| address *required*  | (str) address to send the claim to                                                     |
| amount              | (int) amount of credits to claim name for, defaults to the current amount on the claim |
| claim_id *required* | (str) claim id to send                                                                 |
:::



::: api__content__body
## claim_show

Resolve claim info from nout/txid or with claim ID.
:::

::: api__content__example
Returns:

```
(dict) Dictionary containing claim info as below

{
  "amount": (float) amount of claim
  "claim_id": (str) claim ID of claim
  "height" : (int) height of claim takeover
  "nout": (int) nout of claim
  "supports": (list) list of supports associated with claim
  "txid": (str) txid of claim
  "value": (str) value of claim
}

If claim cannot be resolved, dictionary as below will be returned

{
  "error": (str) reason for error
}
```

Arguments:

| Parameter   | Description                                                      |
|:------------|:-----------------------------------------------------------------|
| claim_id    | (str) look for claim with this claim id                          |
| nout        | (int) look for claim with this nout, txid must also be specified |
| txid        | (str) look for claim with this txid, nout must also be specified |
:::



::: api__content__body
## cli_test_command

This command is only for testing the CLI argument parsing.
:::

::: api__content__example
Returns:

```
pos args
```

Arguments:

| Parameter          | Description   |
|:-------------------|:--------------|
| a_arg              | a arg         |
| b_arg              | b arg         |
| pos_arg *required* | pos arg       |
| pos_args           | pos args      |
| pos_arg2           | pos arg 2     |
| pos_arg3           | pos arg 3     |
:::



::: api__content__body
## commands

Return a list of available commands.
:::

::: api__content__example
Returns:

```
(list) list of available commands
```
:::



::: api__content__body
## daemon_stop

Stop lbrynet-daemon.
:::

::: api__content__example
Returns:

```
(string) Shutdown message
```
:::



::: api__content__body
## file_delete

Delete a LBRY file.
:::

::: api__content__example
Returns:

```
(bool) true if deletion was successful
```

Arguments:

| Parameter                | Description                                                                                                           |
|:-------------------------|:----------------------------------------------------------------------------------------------------------------------|
| channel_claim_id         | (str) delete by file channel claim id                                                                                 |
| channel_name             | (str) delete by file channel claim name                                                                               |
| claim_id                 | (str) delete by file claim id                                                                                         |
| claim_name               | (str) delete by file claim name                                                                                       |
| delete_all               | (bool) if there are multiple matching files, allow the deletion of multiple files. Otherwise, do not delete anything. |
| delete_from_download_dir | (bool) delete file from download directory, instead of just deleting blobs                                            |
| file_name                | (str) delete by file name in downloads folder                                                                         |
| nout                     | (int) delete by file claim nout                                                                                       |
| rowid                    | (int) delete by file row id                                                                                           |
| sd_hash                  | (str) delete by file sd hash                                                                                          |
| stream_hash              | (str) delete by file stream hash                                                                                      |
| txid                     | (str) delete by file claim txid                                                                                       |
:::



::: api__content__body
## file_list

List files limited by optional filters.
:::

::: api__content__example
Returns:

```
(list) List of files

[{
  "blobs_completed": (int) num_completed, None if full_status is false
  "blobs_in_stream": (int) None if full_status is false
  "channel_claim_id": (str) None if full_status is false or if claim is not found or signed
  "channel_name": (str) None if full_status is false or if claim is not found or signed
  "claim_id": (str) None if full_status is false or if claim is not found
  "claim_name": (str) None if full_status is false or if claim is not found
  "completed": (bool) true if download is completed
  "download_directory": (str) download directory
  "download_path": (str) download path of file
  "file_name": (str) name of file
  "key": (str) key attached to file
  "metadata": (dict) None if full_status is false or if claim is not found
  "mime_type": (str) mime type of file
  "nout": (int) None if full_status is false or if claim is not found
  "outpoint": (str) None if full_status is false or if claim is not found
  "points_paid": (float) credit paid to download file
  "sd_hash": (str) sd hash of file
  "status": (str) downloader status, None if full_status is false
  "stopped": (bool) true if download is stopped
  "stream_hash": (str) stream hash of file
  "stream_name": (str) stream name
  "suggested_file_name": (str) suggested file name
  "total_bytes": (int) file size in bytes, None if full_status is false
  "txid": (str) None if full_status is false or if claim is not found
  "written_bytes": (int) written size in bytes
}]
```

Arguments:

| Parameter        | Description                                                                                                      |
|:-----------------|:-----------------------------------------------------------------------------------------------------------------|
| channel_claim_id | (str) get file with matching channel claim id                                                                    |
| channel_name     | (str) get file with matching channel name                                                                        |
| claim_id         | (str) get file with matching claim id                                                                            |
| claim_name       | (str) get file with matching claim name                                                                          |
| file_name        | (str) get file with matching file name in the downloads folder                                                   |
| full_status      | (bool) full status, populate the "message" and "size" fields                                                     |
| nout             | (int) get file with matching claim nout                                                                          |
| outpoint         | (str) get file with matching claim outpoint                                                                      |
| rowid            | (int) get file with matching row id                                                                              |
| sd_hash          | (str) get file with matching sd hash                                                                             |
| sort             | (str) sort by any property, like "file_name" or "metadata.author"; to specify direction append ",asc" or ",desc" |
| stream_hash      | (str) get file with matching stream hash                                                                         |
| txid             | (str) get file with matching claim txid                                                                          |
:::



::: api__content__body
## file_reflect

Reflect all the blobs in a file matching the filter criteria.
:::

::: api__content__example
Returns:

```
(list) list of blobs reflected
```

Arguments:

| Parameter   | Description                                                                          |
|:------------|:-------------------------------------------------------------------------------------|
| file_name   | (str) get file with matching file name in the downloads folder                       |
| reflector   | (str) reflector server, ip address or url by default choose a server from the config |
| rowid       | (int) get file with matching row id                                                  |
| sd_hash     | (str) get file with matching sd hash                                                 |
| stream_hash | (str) get file with matching stream hash                                             |
:::



::: api__content__body
## file_set_status

Start or stop downloading a file.
:::

::: api__content__example
Returns:

```
(str) Confirmation message
```

Arguments:

| Parameter         | Description                                                              |
|:------------------|:-------------------------------------------------------------------------|
| file_name         | (str) set status of file with matching file name in the downloads folder |
| rowid             | (int) set status of file with matching row id                            |
| sd_hash           | (str) set status of file with matching sd hash                           |
| status *required* | (str) one of "start" or "stop"                                           |
| stream_hash       | (str) set status of file with matching stream hash                       |
:::



::: api__content__body
## get

Download stream from a LBRY name.
:::

::: api__content__example
Returns:

```
(dict) Dictionary containing information about the stream

{
  "blobs_completed": (int) num_completed, None if `full_status` is false
  "blobs_in_stream": (int) None if `full_status` is false
  "channel_claim_id": (str) None if claim is not signed
  "channel_name": (str) None if claim is not signed
  "claim_id": (str) claim id
  "claim_name": (str) claim name
  "completed": (bool) true if download is completed
  "download_directory": (str) download directory
  "download_path": (str) download path of file
  "key": (str) key attached to file
  "file_name": (str) name of file
  "metadata": (dict) claim metadata
  "mime_type": (str) mime type of file
  "nout": (int) claim nout
  "outpoint": (str) claim outpoint string
  "points_paid": (float) credit paid to download file
  "sd_hash": (str) sd hash of file
  "status": (str) downloader status, None if `full_status` is false
  "stopped": (bool) true if download is stopped
  "stream_hash": (str) stream hash of file
  "stream_name": (str) stream name
  "suggested_file_name": (str) suggested file name
  "total_bytes": (int) file size in bytes, None if `full_status` is false
  "txid": (str) claim txid
  "written_bytes": (int) written size in bytes
}
```

Arguments:

| Parameter   | Description                                  |
|:------------|:---------------------------------------------|
| file_name   | (str) specified name for the downloaded file |
| timeout     | (int) download timeout in number of seconds  |
| uri         | (str) uri of the content to download         |
:::



::: api__content__body
## help

Return a useful message for an API command.
:::

::: api__content__example
Returns:

```
(str) Help message
```

Arguments:

| Parameter   | Description                                 |
|:------------|:--------------------------------------------|
| command     | (str) command to retrieve documentation for |
:::



::: api__content__body
## peer_list

Get peers for blob hash.
:::

::: api__content__example
Returns:

```
(list) List of contact dictionaries { "host": <peer ip>, "port": <peer port>, "node_id": <peer node id> }
```

Arguments:

| Parameter            | Description                                   |
|:---------------------|:----------------------------------------------|
| blob_hash *required* | (str) find available peers for this blob hash |
| timeout              | (int) peer search timeout in seconds          |
:::



::: api__content__body
## peer_ping

Find and ping a peer by node id.
:::

::: api__content__example
Returns:

```
(str) pong, or {"error": <error message>} if an error is encountered
```
:::



::: api__content__body
## publish

Make a new name claim and publish associated data to lbrynet, update over existing claim if user already has a claim for name.

Fields required in the final Metadata are:
- author
- description
- language
- license
- nsfw
- title

Metadata can be set by either using the metadata argument or by setting individual arguments fee, title, description, author, language, license, license_url, thumbnail, preview, nsfw, or sources. Individual arguments will overwrite the fields specified in metadata argument.
:::

::: api__content__example
Returns:

```
(dict) Dictionary containing result of the claim

{
  "claim_id": (str) claim ID of the resulting claim
  "fee": (decimal) fee paid for the claim transaction
  "nout": (int) nout of the resulting claim
  "tx": (str) hex encoded transaction
  "txid": (str) txid of resulting claim
}
```

Arguments:

| Parameter       | Description                                                                                                                                                                                                                                                              |
|:----------------|:-------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| author          | (str) author of the publication                                                                                                                                                                                                                                          |
| bid *required*  | (decimal) amount to back the claim                                                                                                                                                                                                                                       |
| channel_name    | (str) name of the publisher channel name in the wallet                                                                                                                                                                                                                   |
| channel_id      | (str) claim id of the publisher channel, does not check for channel claim being in the wallet. This allows publishing to a channel where only the certificate private key is in the wallet.                                                                              |
| claim_address   | (str) address where the claim is sent to, if not specified new address will automatically be created                                                                                                                                                                     |
| description     | (str) description of the publication                                                                                                                                                                                                                                     |
| fee             | (dict) Dictionary representing key fee to download content: {"currency": currency_symbol, "amount": decimal, "address": str, optional } supported currencies: LBC, USD, BTCIf an address is not provided a new one will be automatically generated. Default fee is zero. |
| file_path       | (str) path to file to be associated with name. If provided, a lbry stream of this file will be used in "sources". If no path is given but a sources dict is provided, it will be used. If neither are provided, an error is raised.                                      |
| language        | (str) language of the publication                                                                                                                                                                                                                                        |
| license         | (str) publication license                                                                                                                                                                                                                                                |
| license_url     | (str) publication license url                                                                                                                                                                                                                                            |
| metadata        | (dict) ClaimDict to associate with the claim.                                                                                                                                                                                                                            |
| name *required* | (str) name of the content                                                                                                                                                                                                                                                |
| nsfw            | (bool) title of the publication                                                                                                                                                                                                                                          |
| preview         | (str) preview url                                                                                                                                                                                                                                                        |
| sources         | (str) { "lbry_sd_hash": sd_hash } specifies sd hash of file                                                                                                                                                                                                              |
| thumbnail       | (str) thumbnail url                                                                                                                                                                                                                                                      |
| title           | (str) title of the publication                                                                                                                                                                                                                                           |
:::



::: api__content__body
## report_bug

Report a bug to Slack.
:::

::: api__content__example
Returns:

```
(bool) true if successful
```

Arguments:

| Parameter          | Description                  |
|:-------------------|:-----------------------------|
| message *required* | (str) Description of the bug |
:::



::: api__content__body
## resolve

Resolve given LBRY URIs.
:::

::: api__content__example
Returns:

```
Dictionary of results, keyed by uri

"<uri>": {
  If a resolution error occurs:
  "error": Error message

  If the uri resolves to a channel or a claim in a channel:
  "certificate": {
    "address": (str) claim address
    "amount": (float) claim amount
    "claim_id": (str) claim id
    "claim_sequence": (int) claim sequence number
    "decoded_claim": (bool) whether or not the claim value was decoded
    "depth": (int) claim depth
    "effective_amount": (float) claim amount including supports
    "has_signature": (bool) included if decoded_claim
    "height": (int) claim height
    "name": (str) claim name
    "nout": (str) claim nout
    "permanent_url": (str) permanent url of the certificate claim
    "signature_is_valid": (bool), included if has_signature
    "supports: (list) list of supports [{
      "amount": (float) amount
      "nout": (int) nout
      "txid": (str) txid
    }]
    "txid": (str) claim txid
    "value": ClaimDict if decoded, otherwise hex string
  }

  If the uri resolves to a channel:
  "claims_in_channel": (int) number of claims in the channel,

  If the uri resolves to a claim:
  "claim": {
    "address": (str) claim address
    "amount": (float) claim amount
    "channel_name": (str) channel name if claim is in a channel
    "claim_id": (str) claim id
    "claim_sequence": (int) claim sequence number
    "decoded_claim": (bool) whether or not the claim value was decoded
    "depth": (int) claim depth
    "effective_amount": (float) claim amount including supports
    "has_signature": (bool) included if decoded_claim
    "height": (int) claim height
    "name": (str) claim name
    "nout": (str) claim nout
    "permanent_url": (str) permanent url of the claim
    "signature_is_valid": (bool), included if has_signature
    "supports: (list) list of supports [{
      "amount": (float) amount
      "nout": (int) nout
      "txid": (str) txid
    }]
    "txid": (str) claim txid
    "value": ClaimDict if decoded, otherwise hex string
  }
}
```

Arguments:

| Parameter      | Description                           |
|:---------------|:--------------------------------------|
| force          | (bool) force refresh and ignore cache |
| uri *required* | (str) uri to resolve                  |
| uris           | (list) uris to resolve                |
:::



::: api__content__body
## resolve_name

Resolve stream info from a LBRY name.
:::

::: api__content__example
Returns:

```
(dict) Metadata dictionary from name claim, None if the name is not resolvable
```

Arguments:

| Parameter       | Description                                 |
|:----------------|:--------------------------------------------|
| force           | (bool) force refresh and do not check cache |
| name *required* | (str) the name to resolve                   |
:::



::: api__content__body
## routing_table_get

Get DHT routing information.
:::

::: api__content__example
Returns:

```
(dict) dictionary containing routing and contact information

{
  "buckets": {
    <bucket index>: [{
      "address": (str) peer address
      "blobs": (list) blob hashes announced by peer
      "node_id": (str) peer node id
      "port": (int) peer udp port
    }]
  }
  "blob_hashes": (list) all of the blob hashes stored by peers in the list of buckets
  "contacts": (list) contact node ids
  "node_id": (str) the local dht node id
}
```
:::



::: api__content__body
## settings_get

Get daemon settings.
:::

::: api__content__example
Returns:

```
(dict) Dictionary of daemon settings
See ADJUSTABLE_SETTINGS in lbrynet/conf.py for full list of settings
```
:::



::: api__content__body
## settings_set

Set daemon settings.
:::

::: api__content__example
Returns:

```
(dict) Updated dictionary of daemon settings
```

Arguments:

| Parameter                     | Description                                                                                                                                                                                        |
|:------------------------------|:---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| auto_renew_claim_height_delta | (int) 0 claims set to expire within this many blocks will be automatically renewed after startup (if set to 0, renews will not be made automatically)                                              |
| cache_time                    | (int) 150                                                                                                                                                                                          |
| data_rate                     | (float) 0.0001                                                                                                                                                                                     |
| disable_max_key_fee           | (bool) False                                                                                                                                                                                       |
| download_directory            | (str) path of download directory                                                                                                                                                                   |
| download_timeout              | (int) 180                                                                                                                                                                                          |
| max_key_fee                   | (dict) maximum key fee for downloads, in the format: { "currency": <currency_symbol>, "amount": <amount> }. In the CLI, it must be an escaped JSON stringSupported currency symbols: LBC, USD, BTC |
| peer_port                     | (int) 3333                                                                                                                                                                                         |
| peer_search_timeout           | (int) 3                                                                                                                                                                                            |
| reflect_uploads               | (bool) True                                                                                                                                                                                        |
| run_reflector_server          | (bool) False                                                                                                                                                                                       |
| sd_download_timeout           | (int) 3                                                                                                                                                                                            |
| share_usage_data              | (bool) True                                                                                                                                                                                        |
| use_upnp                      | (bool) True                                                                                                                                                                                        |
:::



::: api__content__body
## status

Get daemon status.
:::

::: api__content__example
Returns:

```
(dict) lbrynet-daemon status

{
  "blockchain_status": {
    "best_blockhash": block hash of most recent block
    "blocks": local blockchain height
    "blocks_behind": remote_height - local_height
  }
  "connection_status": {
    "code": connection status code,
    "message": connection status message
  }
  "installation_id": installation id, base58
  "is_first_run": bool
  "is_running": bool
  "lbry_id": lbry peer id, base58
  "startup_status": {
    "code": status code,
    "message": status message
  }
  "wallet_is_encrypted": bool

  If given the session status option:

  "session_status": {
    "announce_queue_size": number of blobs currently queued to be announced
    "managed_blobs": count of blobs in the blob manager
    "managed_streams": count of streams in the file manager
    "should_announce_blobs": number of blobs that should be announced
  }
}
```

Arguments:

| Parameter      | Description                              |
|:---------------|:-----------------------------------------|
| session_status | (bool) include session status in results |
:::



::: api__content__body
## stream_availability

Get stream availability for lbry uri.
:::

::: api__content__example
Returns:

```
(dict) {
  "did_decode": <bool>
  "did_resolve": <bool>
  "error": <None> | <str> error message
  "head_blob_availability": <dict> see `blob_availability`
  "head_blob_hash": <str>
  "is_available": <bool>
  "is_stream": <bool>
  "num_blobs_in_stream": <int>
  "sd_blob_availability": <dict> see `blob_availability`
  "sd_hash": <str>
  "upnp_redirect_is_set": <bool>
  "use_upnp": <bool>
}
```

Arguments:

| Parameter      | Description                                                |
|:---------------|:-----------------------------------------------------------|
| blob_timeout   | (int) how long to try downloading from a peer              |
| search_timeout | (int) how long to search for peers for the blob in the dht |
| uri *required* | (str) check availability for this uri                      |
:::



::: api__content__body
## stream_cost_estimate

Get estimated cost for a lbry stream.
:::

::: api__content__example
Returns:

```
(float) Estimated cost in lbry credits, returns None if uri is not resolvable
```

Arguments:

| Parameter      | Description                                                               |
|:---------------|:--------------------------------------------------------------------------|
| size           | (float) stream size in bytes. If provided an sd blob won't be downloaded. |
| uri *required* | (str) uri to use                                                          |
:::



::: api__content__body
## transaction_list

List transactions belonging to wallet.
:::

::: api__content__example
Returns:

```
(list) List of transactions

{
  "abandon_info": (list) abandon info if in txn [{
    "address": (str) address of abandoned claim
    "amount": (float) claim amount
    "balance_delta": (float) returned amount
    "claim_id": (str) claim id
    "claim_name": (str) claim name
    "nout": (int) nout
  }]
  "claim_info": (list) claim info if in txn [{
    "address": (str) address of claim
    "amount": (float) claim amount
    "balance_delta": (float) bid amount
    "claim_id": (str) claim id
    "claim_name": (str) claim name
    "nout": (int) nout
  }]
  "confirmations": (int) number of confirmations for the txn
  "date": (str) date and time of txn
  "fee": (float) txn fee
  "support_info": (list) support info if in txn [{
    "address": (str) address of support
    "amount": (float) support amount
    "balance_delta": (float) support amount
    "claim_id": (str) claim id
    "claim_name": (str) claim name
    "is_tip": (bool)
    "nout": (int) nout
  }]
  "timestamp": (int) timestamp
  "txid": (str) txn id
  "update_info": (list) update info if in txn [{
    "address": (str) address of claim
    "amount": (float) absolute amount
    "balance_delta": (float) credited/debited
    "claim_id": (str) claim id
    "claim_name": (str) claim name
    "nout": (int) nout
  }]
  "value": (float) value of txn
}
```
:::



::: api__content__body
## transaction_show

Get a decoded transaction from a txid.
:::

::: api__content__example
Returns:

```
(dict) JSON formatted transaction
```

Arguments:

| Parameter       | Description                   |
|:----------------|:------------------------------|
| txid *required* | (str) txid of the transaction |
:::



::: api__content__body
## utxo_list

List unspent transaction outputs.
:::

::: api__content__example
Returns:

```
(list) List of unspent transaction outputs (UTXOs)

[
  {
    "address": (str) the output address
    "amount": (float) unspent amount
    "height": (int) block height
    "is_claim": (bool) is the tx a claim
    "is_coinbase": (bool) is the tx a coinbase tx
    "is_support": (bool) is the tx a support
    "is_update": (bool) is the tx an update
    "nout": (int) nout of the output
    "txid": (str) txid of the output
  }
  ...
]
```
:::



::: api__content__body
## version

Get lbry version information.
:::

::: api__content__example
Returns:

```
(dict) Dictionary of lbry version information

{
  "build": (str) build type (e.g. "dev", "rc", "release")
  "ip": (str) remote ip, if available
  "lbrynet_version": (str) lbrynet_version
  "lbryschema_version": (str) lbryschema_version
  "lbryum_version": (str) lbryum_version
  "os_release": (str) os release string
  "os_system": (str) os name
  "platform": (str) platform string
  "processor": (str) processor type
  "python_version": (str) python version
}
```
:::



::: api__content__body
## wallet_balance

Return the balance of the wallet.
:::

::: api__content__example
Returns:

```
(float) amount of lbry credits in wallet
```

Arguments:

| Parameter           | Description                                                       |
|:--------------------|:------------------------------------------------------------------|
| address             | (str) If provided only the balance for this address will be given |
| include_unconfirmed | (bool) Include unconfirmed                                        |
:::



::: api__content__body
## wallet_decrypt

Decrypt an encrypted wallet, this will remove the wallet password.
:::

::: api__content__example
Returns:

```
(bool) true if wallet is decrypted, otherwise false
```
:::



::: api__content__body
## wallet_encrypt

Encrypt a wallet with a password, if the wallet is already encrypted this will update
the password.
:::

::: api__content__example
Returns:

```
(bool) true if wallet is decrypted, otherwise false
```

Arguments:

| Parameter               | Description                                            |
|:------------------------|:-------------------------------------------------------|
| new_password *required* | (str) password string to be used for encrypting wallet |
:::



::: api__content__body
## wallet_is_address_mine

Checks if an address is associated with the current wallet.
:::

::: api__content__example
Returns:

```
(bool) true, if address is associated with current wallet
```

Arguments:

| Parameter          | Description            |
|:-------------------|:-----------------------|
| address *required* | (str) address to check |
:::



::: api__content__body
## wallet_list

List wallet addresses.
:::

::: api__content__example
Returns:

```
List of wallet addresses
```
:::



::: api__content__body
## wallet_new_address

Generate a new wallet address.
:::

::: api__content__example
Returns:

```
(str) New wallet address in base58
```
:::



::: api__content__body
## wallet_prefill_addresses

Create new addresses, each containing `amount` credits.
:::

::: api__content__example
Returns:

```
(dict) the resulting transaction
```

Arguments:

| Parameter                | Description                            |
|:-------------------------|:---------------------------------------|
| amount *required*        | (float) initial amount in each address |
| no_broadcast             | (bool) whether to broadcast or not     |
| num_addresses *required* | (int) num of addresses to create       |
:::



::: api__content__body
## wallet_public_key

Get public key from wallet address.
:::

::: api__content__example
Returns:

```
(list) list of public keys associated with address. Could contain more than one public key if multisig.
```

Arguments:

| Parameter          | Description                                   |
|:-------------------|:----------------------------------------------|
| address *required* | (str) address for which to get the public key |
:::



::: api__content__body
## wallet_send

Send credits. If given an address, send credits to it. If given a claim id, send a tip to the owner of a claim specified by uri. A tip is a claim support where the recipient of the support is the claim address for the claim being supported.
:::

::: api__content__example
Returns:

```
If sending to an address:
(bool) true if payment successfully scheduled

If sending a claim tip:
(dict) Dictionary containing the result of the support

{
  "fee": (float) fee paid for the transaction
  "nout": (int) nout of the resulting support claim
  "txid": (str) txid of resulting support claim
}
```

Arguments:

| Parameter           | Description                               |
|:--------------------|:------------------------------------------|
| address *required*  | (str) address to send credits to          |
| amount *required*   | (float) amount of credit to send          |
| claim_id *required* | (float) claim id of the claim to send tip |
:::



::: api__content__body
## wallet_unlock

Unlock an encrypted wallet.
:::

::: api__content__example
Returns:

```
(bool) true if wallet is unlocked, otherwise false
```

Arguments:

| Parameter           | Description                         |
|:--------------------|:------------------------------------|
| password *required* | (str) password for unlocking wallet |
:::



::: api__content__body
## wallet_unused_address

Return an address containing no balance, will create a new address if there is none.
:::

::: api__content__example
Returns:

```
(str) Unused wallet address in base58
```
:::
