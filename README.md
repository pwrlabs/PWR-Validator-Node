
### **PWR Chain Validator Node Guide**

**Important Note**: This is the inaugural testnet launch. While we strive for perfection, there might be unforeseen issues. We appreciate all feedback, bug reports, or any other issues reported in our [Discord server](https://discord.gg/DJkcuy9SAg).

#### **Requirements**:
- **CPU**: Single Core
- **Memory**: 1 GB RAM
- **Disk**: 25 GB SSD
- **Open Ports**: 8231, 8085

#### **Setup on Ubuntu Server**:

1. **Install Java**: 
   ```bash
   apt install openjdk-19-jre-headless
   ```

2. **Clone the PWR Validator Node Repository**:
   ```bash
   git clone https://github.com/PWR-Labs/PWR-Validator-Node.git
   ```

3. **Navigate to the Validator Node Directory**:
   ```bash
   cd PWR-Validator-Node
   ```

4. **Set Up your Password**:
   ```bash
   sudo touch password
   sudo nano password
   ```
   - Enter your desired password.
   - Press `Ctrl + x` to close.
   - Press `Y` to confirm saving the password.

5. **Run the Node**:
   Replace `<YOUR_SERVER_IP>` with your server's actual IP.
   ```bash
   java -jar validator.jar password <YOUR_SERVER_IP>
   ```

   - Upon initialization, the node will generate a wallet, store it locally, and display an address in the format: 
     ```
     My address: 0xf4b2f12afa634c206bdf5f0dd6dd90f024ad62b7
     ```

6. **Become a Validator Node**:

   - Initially, your node will synchronize with the blockchain but will not assume validator responsibilities until it possesses staked PWR Coins.
   
   - To obtain sufficient PWR Coins for staking, [apply to become a testnet validator on our Discord server](https://discord.gg/DJkcuy9SAg). Once approved, share the displayed address with the team, and you'll receive a 100k PWR stake.
   
   - After claiming your coins, your node will initiate a transaction to enlist as a validator.

7. **Running in the Background**:
   If you wish to run the node in the background, ensuring it remains active after closing the terminal, utilize the `nohup` command:
   ```bash
   nohup java -jar validator.jar password <YOUR_SERVER_IP> &
   ```

Congratulations, you've now set up and run a PWR Chain validator node!

---

Feel free to adapt as necessary and inform users to always keep their passwords and private keys secure.
