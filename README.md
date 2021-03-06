# alastria-docker

## Build the image
### Node with monitor
```
docker build -t alastria-node .
```

### Node without monitor
```
docker build --build-arg MONITOR_ENABLED=0 -t alastria-node .
```

## Launch a node manually
Note that `NODE_TYPE` and `NODE_NAME` environment variables have to be specified.
```
docker run -tid \
-v "$(pwd)"/alastria:/root/alastria \
-p 21000:21000 \
-p 21000:21000/udp \
-p 22000:22000 \
-p 9000:9000 \
-p 8443:8443 \
-e NODE_TYPE=<node_type> \
-e NODE_NAME=<node_name> \
--restart unless-stopped \
--name alastria-node \
councilbox/alastria-node
```

## Launch a node with the `launch.sh` script
1. Clone this repository with `git clone https://github.com/councilbox/cbx-alastria-docker`.
2. Change the values of the following environment variables in the file `env.sh`:
    - `NODE_NAME` with the name of your node.
    - `NODE_TYPE` with the node type `general` or `validator`.
    - `DATA_DIR` with the directory path where the node's data will be stored.

Execute the `launch.sh` script:
```bash
./launch.sh
```

Note: custom `docker run` options can be added as arguments to the script.

## Backup
### Keys only
```bash
./backup.sh
```

### Full backup (keys and chain data)
```bash
./backup.sh all
```
