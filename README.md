# Snapshot

## Catch the latest block faster by using our daily snapshots.


![image](https://user-images.githubusercontent.com/38919673/222435157-9236d953-ca85-40c1-8fca-ed18d7864b51.png)

Snapshots allows a new node to join the network by recovering application state from a backup file. Snapshot contains compressed copy of chain data directory. To keep backup files as small as plausible, snapshot server is periodically beeing state-synced.

# Instructions

## Stop the service and reset the data
```
sudo systemctl stop nolusd
cp $HOME/.nolus/data/priv_validator_state.json $HOME/.nolus/priv_validator_state.json.backup
rm -rf $HOME/.nolus/data
```

## Download latest snapshot
```
curl -L https://snapshoots.nolus.kaelvnode.xyz/nolus/nolus-snapshot-20230302.tar.lz4 | tar -Ilz4 -xf - -C $HOME/.nolus
mv $HOME/.nolus/priv_validator_state.json.backup $HOME/.nolus/data/priv_validator_state.json
```

## Restart the service and check the log

```
sudo systemctl start nolusd && sudo journalctl -u nolusd -f --no-hostname -o cat
```
