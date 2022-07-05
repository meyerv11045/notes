# Blob Storage

## Blob Types

[Understanding block blobs, append blobs, and page blobs - Azure Storage | Microsoft Docs](https://docs.microsoft.com/en-us/rest/api/storageservices/understanding-block-blobs--append-blobs--and-page-blobs)

1. Block Blob- optimized foruploading large amounts of data efficiently

   - Composed of blocks each of which have a block id

   - 50k blocks max in a blob

   - Write set of blocks via Put Block op

   - Commit blocks to a blob with Put Block List op

   - *When you upload a block to a blob in your storage account, it is associated with the specified block blob, but it does not become part of the blob until you commit a list of blocks that includes the new block's ID*

   - 4000 MiB max block size
     - Better suited for SJ blocks since stream duration may make them very large depending on length

   - Can upload multiple blocks to same blob in parallel

   - Can include MD5 hash to verify transfer of a block
     - Track upload progress and resend a block if needed

   - Can upload blocks in any order and then finalize the order in the blob in the commit step

2. Append Blob- composed ofblocks and optimized for append operations

   - Blocks added to end of blob

   - Cannot update/delete existing blocks

   - 4 MiB ~ 4MB max size for an append block
     - Could easily go past this since with a longer stream duration and higher bitrate for the video  streams so likely not a good choice

   - Max 50k blocks

3. Page Blob- collection of512-byte pages optimized for random read/write ops

   - Useful for VM disks

## Access Tiers:

- Hot Tier- online; optimized for storing data that is accessed/modified frequently (higheststorage cost, lowest access cost)
- Cool Tier- online; optimized for storing data that is infrequently accessed or modified (lower storage costs, higher access cost)
  - Data stored for min 30 days (pay early deletion fee otherwise)
    - No min retention for blob  storage accounts specifically

- ArchiveTier- offline; optimized for storing data that is rarely accessed and has flexible latency requirements (order of hours)
  - Data stored for min 180 days (pay early deletion fee otherwise)
  - Data can't be read or modified here, must first move it to online tier (can take up to 15 hours to "rehydrate")
  - Blob metadata available for access

- Online- users can access the data immediately
- Offline- must move data to online to access data (this process can take up to 15 hrs)
- Per GB capacity cost decreases as tier gets cooler
- Data access charges increaseas tier gets cooler

## Authorization Methods

- Azure Active Directfory (AAD)
- Connection String
- Access Token/Key

### AAD for Blobs:

- Security Principal- user, group, application service principal, or managed identity

- Resource access has 2 steps w/ AAD

- 1. Security Principal's identity is authenticated and an Oauth 2.0 token is returned
  2. Token is passed as part of a request to the Blob service and used by the service to authorize access to the specified resource

- Requires 1+ Azure RBAC roles be assigned to security principal making the request