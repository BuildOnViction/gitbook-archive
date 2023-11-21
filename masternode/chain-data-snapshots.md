---
description: >-
  A snapshot is a recording of the state of a blockchain at a particular block
  height.
---

# Chain Data Snapshots

Please find the latest snapshot here: [https://tomotools.com/](https://tomotools.com/)

The following commands are step by step instructions for TomoChain Masternode operators that can be used for two major use-cases:

1. Fixing nodes that are stuck; evidenced by a node that stays on a block and doesn't progress
2. Jumpstarting a newly setup Masternode; avoid waiting a week for synchronization

Basically, a compressed version of the last-known "good" chaindata is downloaded. This comes from TomoChain on a weekly basis. Remove the node's old data and update it with the newly downloaded data. Finally, restart the sync-process from this known-good checkpoint.

_Note: Ensure there is enough disk space for both the tar file AND its uncompressed contents. Double the space or more._

```
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

**Tip: extract the data in background**

In case you can not wait for the extraction finish, you can run it in the background

```
nohup tar xvC /var/lib/docker/volumes/NAME_OF_YOUR_VOLUME/_data/data/tomo/ -f 20190813.tar &
```
