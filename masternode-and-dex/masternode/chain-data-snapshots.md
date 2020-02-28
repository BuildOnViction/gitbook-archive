---
description: >-
  A snapshot is a recording of the state of a blockchain at a particular block
  height.
---

# Chain Data Snapshots

Latest snapshot: [download](https://chaindata.tomochain.com/20190813.tar) \(91 GB, md5sum 0b23a48b0d6585690350e91b0f6c9f14\)

The following commands are step by step instructions for Tomo Masternode operators that can be used for two major use-cases:

1. Fixing nodes that are stuck; evidenced by a node that stays on a block and doesn't progress
2. Jumpstarting a newly setup Masternode; avoid waiting a week for synchronization

Basically, you download a compressed version of the last-known "good" chaindata. This comes from Tomochain Ptd on a weekly basis. You remove the nodes old data and update it with the newly downloaded data. Finally you restart the sync-process from this known-good checkpoint.

_Note: Assure that you have enough disk space for both the tar file AND its uncompressed contents. Double the space or more._

```text
# Login as user that has access to tmn
# Download Tomo's chaindata archive (make sure you have enough disk space available)
wget -c https://chaindata.tomochain.com/20190813.tar -P /tmp

# Stop your node (for tmn users)
tmn stop
# or in the node folder (for docker-compose users)
docker-compose stop

# Find the name of your volume
docker volume ls

# Remove your node old data
sudo rm -rf /var/lib/docker/volumes/NAME_OF_YOUR_VOLUME/_data/data/tomo/chaindata

# Find the name of your volume
docker volume ls

# Extract the data
cd /tmp
sudo tar xvC /var/lib/docker/volumes/NAME_OF_YOUR_VOLUME/_data/data/tomo/ -f 20190813.tar

# Start your node back(for tmn users)
tmn start
# or in the node folder (for docker-compose users)
docker-compose start

# If you're really running out of space, remove the tar file
# keeping it might be a good idea if you get stuck further before a new snapshot is released
rm /tmp/20190813.tar
```

**Tip: extract the data in backgroud**

In case you can not wait for the extraction finish, you can run it in the background

```text
nohup tar xvC /var/lib/docker/volumes/NAME_OF_YOUR_VOLUME/_data/data/tomo/ -f 20190813.tar &
```

