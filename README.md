# Ethereum-Full-Node-Deployment-Guide
This is a guide on deploying Ethereum Full node (Execution Client and Consensus Client). <br/>

We will be using the Eth Docker (One of the projects recommended from the Ethereum Official Web Site) in this guide. (https://ethereum.org/en/developers/docs/nodes-and-clients/run-a-node/) <br/>

Step 1: <br/>
Please create the instance/cloud in your preferred cloud platform.

Step 2: <br/>
Download eth docker from github by running the following command. <br/>
```sh
cd ~ && git clone https://github.com/eth-educators/eth-docker.git && cd eth-docker
```

If you don’t have git install, please install it with the following command. <br/>
```sh
sudo apt-get update
sudo apt-get install git-all
```

Step 3: <br/>
Please make sure you are inside “eth-docker” directory and run the following command to install all the required library/package. <br/>
```sh
./ethd install
```

Please answer yes when being prompt during the installation. 

Step 4: <br/>
Please configure the eth-docker by running the following command. In this guide, we will setup the Ethereum Holesky Testnet RPC full node with Nethermind client and Prysm client. <br/>
```sh
./ethd config
```

Please select Holesky testnet. <br/>
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/df9e8a88-9b3c-4063-96b6-c5c8d35d17db)

Please select Ethereum RPC node. (Execution client + Consensus client)
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/fb33173c-5133-4532-91a9-3b12ff325a66)

In this guide, we will use Prysm client as the Consensus client so please select Prysm as the Consensus client.
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/f3433c2b-559e-4152-9e7b-ef444780df19)

In this guide, we will use Netheremind client as the Execution client so please select Nethermind as the Execution client. <br/>
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/86273d54-0343-4378-9e95-4e688170a44c)

Feel free to use the recommended value for the CL Checkpoint Sync URL.
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/863c17ba-ee09-4b7e-9565-db7260a795b3)

Feel free to select “Yes” for MEV Boost and use the recommended value for MEV Relay.
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/3406fd24-944c-4638-ad29-e723c1bd0914) <br/>

![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/2530e144-026a-4c2d-9647-b88e4adb72de)

In this guide, we will not setup Grafana monitoring so we will select “No” for Grafana.
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/db05ed17-e3b7-4e8b-8512-f63e0733e92d)

After that, please provide a test wallet for fee recipient.
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/25a4949b-cec0-4026-9806-1b298ec99965)

That's all for configuration. It will take a while to finish so please wait for it.

Please note that we are deploying a full node. The default configuration of the eth docker is for full node. If you are not sure, please check the .env file by running “cat .env” and look for “ARCHIVE NODE”. It should be configured as false. 
![image](https://github.com/dexter68555/Ethereum-Full-Node-Deployment-Guide/assets/46341564/85d4d156-e43f-4ba4-8064-c7a49c31aaee)

Step 5: <br/>
We need to expose port. Please run the following command to edit the configuration. <br/>
```sh
vi .env
```

Look for the COMPOSE_FILE variable of the .env file and append ":el-shared.yml:cl-shared.yml". After that, press escape button and type ":wq" to save the changes.

Step 6: <br/>
Please make sure you are inside “eth-docker” directory and run the following command to start your RPC node with Nethermind Client (Execution client) and Nimbus Client (Consensus client). <br/>
```sh
./ethd up
```

It will take some time for the node to be fully synchronized. You can check the sync status by running the “eth_blockNumber” method to get the latest block number and cross check it with Etherscan latest block number. 
