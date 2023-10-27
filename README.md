
### **PWR Chain Validator Node Guide**

**Important Note**: This is the inaugural testnet launch. While we strive for perfection, there might be unforeseen issues. We appreciate all feedback, bug reports, or any other issues reported in our [Discord server](https://discord.gg/DJkcuy9SAg).

#### **Requirements**:
- **CPU**: Single Core
- **Memory**: 1 GB RAM
- **Disk**: 25 GB SSD
- **Open Ports**: 8231, 8085 (TCP, Incoming & Outgoing)

#### **Setup on Ubuntu Server**:

1. **Update package information**: 
   ```bash
   sudo apt update
   ```

2. **Install Java**: 
   ```bash
   apt install openjdk-19-jre-headless
   ```

3. **Clone the PWR Validator Node Repository**:
   ```bash
   git clone https://github.com/PWR-Labs/PWR-Validator-Node.git
   ```

4. **Navigate to the Validator Node Directory**:
   ```bash
   cd PWR-Validator-Node
   ```

5. **Set Up your Password**:
   ```bash
   sudo nano password
   ```
   - Enter your desired password.
   - Press `Ctrl + x` to close.
   - Press `Y` to confirm saving the password.

6. **Run the Node**:
   Replace `<YOUR_SERVER_IP>` with your server's actual IP.
   ```bash
   java -jar validator.jar password <YOUR_SERVER_IP>
   ```

   - Upon initialization, the node will generate a wallet, store it locally, and display an address in the format: 
     ```
     My address: 0xf4b2f12afa634c206bdf5f0dd6dd90f024ad62b7
     ```

7. **Become a Validator Node**:

   - Initially, your node will synchronize with the blockchain but will not assume validator responsibilities until it possesses staked PWR Coins.
   
   - To obtain sufficient PWR Coins for staking, [apply to become a testnet validator on our Discord server](https://discord.gg/DJkcuy9SAg). Once approved, share the displayed address with the team, and you'll receive a 100k PWR stake.
   
   - After claiming your coins, your node will initiate a transaction to enlist as a validator.

8. **Running in the Background**:
   If you wish to run the node in the background, ensuring it remains active after closing the terminal, utilize the `nohup` command:
   ```bash
   nohup java -jar validator.jar password <YOUR_SERVER_IP> &
   ```

9. **Running on startup**:
   If you wish to run the node when your machine boots up, then follow this step to create a systemd Service that's automatically run on startup.

   - From /home/ubuntu:
	```
	sudo nano runAtStartup.sh
	```

   - Paste the following bash:
	
```
	SERVICE_NAME="PWRChainValidatorService"
	
	SERVICE_DESCRIPTION="Service to automatically start PWR chain validator node upon startup"
	SCRIPT_PATH="/home/ubuntu/runValidator.sh"
	
	cat << EOF > "/etc/systemd/system/${SERVICE_NAME}.service"
		[Unit]
		Description=${SERVICE_DESCRIPTION}
		After=multi-user.target
	
		[Service]
		WorkingDirectory=/home/ubuntu/
		Type=forking
		ExecStart=${SCRIPT_PATH}
	
		[Install]
		WantedBy=multi-user.target
EOF
	
	chmod 777 "/etc/systemd/system/${SERVICE_NAME}.service"
	
	systemctl daemon-reload
	systemctl enable ${SERVICE_NAME}.service
	systemctl start ${SERVICE_NAME}.service
```
	
   - Save and quit (Control + X, then Y, then Enter)
   
   - Then run
   
   ```
   sudo nano runValidator.sh
   ```
   
   - And paste the following bash:
   
   ```
   #!/bin/bash
   
   IPADDR=""
   
   if [ $# -eq 0 ]; then
   echo "Auto-IP mode"
   IPADDR=$(curl -s https://ipinfo.io/ip)
   else
   echo "Custom IP mode"
   IPADDR=$1
   fi
   
   echo "Starting validator for $IPADDR"
   echo "Logging to validator.log"
   echo "nohup PID saved in nohupPID.log"
   nohup java -jar validator.jar password $IPADDR > validator.log 2>&1 &
   echo $! > nohupPID.log
   ```
   
   - Save and quit (Control + X, then Y, then Enter)
   
   - Finally, make the scripts executable and run the runAtStartup.sh script:
   
   ```
   sudo chmod 700 runValidator.sh && sudo chmod 700 runAtStartup.sh
   ```
   
   ```
   sudo ./runAtStartup.sh
   ```
   
   Now your validator is running and will run automatically at boot!
   
10. **Stopping your validator**:
   If you're using the auto-start on boot script, then you may stop your validator with the following command:

   ```
   sudo kill -9 `cat nohupPID.log` && sudo rm nohupPID.log
   ```

Congratulations, you've now set up and run a PWR Chain validator node!
