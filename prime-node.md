# Running a EtherPrime Node

This guide will walk you through the steps to run a EtherPrime node. Follow each step carefully to initialize, start, and run your node properly.

## Prerequisites

Before beginning, make sure you have downloaded the necessary files:

- **[EtherPrime Node Client](https://github.com/EtherPrime/go-prime)**: The binary client required to run the EtherPrime node.
- **[EtherPrime Genesis File](https://github.com/EtherPrime/genesis)**: The `genesis.json` file to initialize the genesis block.

## Steps to Run a EtherPrime Node

### Step 1: Create a Folder and Download the Files

1. Create a new folder where you want to store your EtherPrime node files.
2. Download the **[EtherPrime Node Client](https://github.com/EtherPrime/go-prime)** and the **[genesis file](https://github.com/EtherPrime/genesis)** (`genesis.json`) and place them in this folder.

### Step 2: Initialize the Genesis and Define Directory

1. Use the following command to initialize the genesis block and specify the data directory:

    ```bash
    ./geth --datadir data init genesis.json
    ```

   This command initializes the data folder (`data`) using the genesis file (`genesis.json`).

### Step 3: Start the Node in Fullsync Mode

1. Start your node using the `geth` command. When running your node for the first time, add the `console` flag to interact with it:

    ```bash
    ./geth --datadir ./data --networkid 131071 --port 30131 --http --http.addr 0.0.0.0 --http.port 8545 --http.api personal,eth,net,web3,miner --http.corsdomain "*" --syncmode "full" console
    ```

   This command will start your node in full synchronization mode and enable an interactive console.

### Step 4: Add Peers to Sync

1. To start syncing with the network, add peers using the `admin.addPeer` command:

    ```javascript 
	admin.addPeer("enode://34c8345bae6eb952d89a371b9eed3ac89f0fac724d05f004c3748da9efce28ac3c9d0ee7017fa96369268502447395b5d3cb4e25c8a4fd93b4cb8a50e9847353@209.74.95.181:30131")
    admin.addPeer("enode://5625ff0b84cafefa95bcfbed897e75081b08e4a4c949f90f3caf29c50b4a69f03ad263f55f81b6b9909558a702876decb2d57dbb08950ccff980a7500011f6ed@209.74.80.15:30131")
    ```

   Adding these peers helps to connect your node with the network for synchronization.

### Step 5: Running or Restarting the Node

1. After adding peers, you can keep the node running or restart it without the `console` flag.
2. If you want to enable mining, you can add the `--mine` flag along with mining parameters:

    ```bash
    ./geth --datadir ./data --networkid 131071 --port 30131 --http --http.addr 0.0.0.0 --http.port 8545 --http.api personal,eth,net,web3,miner --http.corsdomain "*" --syncmode "full" --mine --miner.threads=1 --miner.etherbase 0xYourEthereumAddress
    ```

   Replace `0xYourEthereumAddress` with your own Ethereum address to receive mining rewards.

## Additional Information

### Port Configuration for Running a EtherPrime Node

When setting up your EtherPrime node, you can specify any valid, open network port for communication with the network. The `--port` and `--http.port` flags are customizable, allowing you to adjust your node's communication ports to match your network configuration or security preferences.

- **P2P Port (`--port`)**: This port is used for peer-to-peer (P2P) networking, allowing your node to connect to and interact with other nodes on the network. In the example, it’s set to `30131`, but you can use any open port that doesn’t conflict with other services on your system. For security and accessibility, ensure the chosen port is permitted by your firewall or security settings.

- **HTTP Port (`--http.port`)**: This port enables HTTP-based communication with the node’s API, letting you access JSON-RPC API endpoints. The default HTTP port is often `8545`, but it can be set to any valid port number. This port should also be firewall-configured, especially if your node is publicly accessible, to prevent unauthorized access.

- **WebSocket Port (`--ws.port`)**: This port is for WebSocket communication, which enables real-time updates and interaction with the node. By default, this port is often set to `8546`, but, like the other ports, it can be customized. Ensure this port is open in your firewall if you intend to use WebSocket connections with your node.

To customize ports, replace the values in the commands:
```bash
--port <your_desired_port> --http.port <your_http_port> --ws.port <your_ws_port>
```

Be mindful that choosing unique ports outside common ranges can help improve security. However, ensure these ports are allowed on your network for proper connectivity to the EtherPrime network.

- **API Exposure**: The `--http.api` and `--ws.api` flags expose specific APIs. Adjust the options depending on your needs.
- **Security Considerations**: Ensure that your node is protected, especially when running in an open network, by configuring the firewall and using appropriate HTTP settings.

## Troubleshooting

- **Genesis File Error**: Ensure the genesis file path is correct during initialization.
- **Connection Issues**: Make sure your firewall is allowing the necessary ports for peer-to-peer connections.

Happy node running! If you run into issues, feel free to open an issue in the repository.

