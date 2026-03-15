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
	admin.addPeer("enode://dcbe7cdc198df841f01ff0e3c2d74cbe372eea8a8d47bac479d1a6799684713cab0de1c96e798c2f95d93c13f1b57c7e371389d64b97f4ccb984729585417088@209.74.95.181:30131")
    admin.addPeer("enode://66c6358b0e372ddc48123c200cd82b5e59d3f65cd4b0342c2d1e58e59299466ef99ff7833169a68378f1758f49bc955a3c4e8031c383918e139b9b482cfb7b98@209.74.80.15:30131")
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

