## AIOZ DePIN CLI

Official DePIN CLI implementation of the AIOZ Network.

## What is AIOZ DePIN CLI?

AIOZ DePIN CLI is a command-line appilcation that connects your machine to the AIOZ DePIN network, contribute storage, bandwidth, and compute, and be rewarded in AIOZ tokens for that contribution.

## Requirements

- Windows 10 version 22H2 64-bit or above
- Ubuntu 14.04 64-bit or above
- macOS Catalina version 10.15 or above

## Getting started

### Windows

Download and extract the latest AIOZ DePIN CLI. The scripts below are written for Windows PowerShell.

```shell
curl.exe -LO https://github.com/AIOZNetwork/aioz-depin-cli/releases/download/v1.2.5/aioz-depin-windows-amd64-1.2.5.zip
Expand-Archive -Path aioz-depin-windows-amd64-1.2.5.zip -DestinationPath .
ren aioz-depin-cli-windows-amd64.exe aioz-depin-cli.exe
```

Verify the installation

```shell
.\aioz-depin-cli.exe version
```

The output should be the version of AIOZ DePIN CLI.

Generate a new mnemonic phrase and private key

```shell
.\aioz-depin-cli.exe keytool new --save-priv-key privkey.json
```

`--save-priv-key` writes the private key to file

Response

```json
{
  "address": "aioz1k28nzwgrwgzrwfuwsfcqjyvd0r4lfprql2c4uf",
  "address_hex": "0xB28F313903720437278E827009118d78eBf48460",
  "pub_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"AxSwg94OuvFIn...CqFunK3pMjV0I\"}",
  "priv_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PrivKey\",\"key\":\"rdWGOtJ/Uio4SD...BCCOfegAI9OGMIbE=\"}",
  "mnemonic": "rain wing olive skate effort present long myself combine ... glide absent spider effort attitude enemy mouse"
}
```

Run the node

```shell
.\aioz-depin-cli.exe start --home nodedata --priv-key-file privkey.json
```

`--home` data folder of the node

`--priv-key-file` the private key file which the node starts with. If you do not specify the private key file, the node will ask for it from the standard input stream.

Note:
Because AIOZ DePIN CLI automatically updates itself by downloading and replacing the executable file, make sure to set file permission to writable.
AIOZ DePIN CLI has to stop to perform auto update, it should be run as Windows Service to start again after update and at system boot.

**IMPORTANT NOTE**

- Treat your `priv_key` JSON and mnemonic phrase as **wallet secrets**. Anyone who has them can **control your node rewards**.
- Use a **dedicated key for each node**; **do not reuse** the key from your main wallet, exchange account, or other nodes.
- Store backups in an **offline, encrypted location** such as encrypted USB drives, air-gapped devices, or hardware security modules (HSM).
- **Never paste** your mnemonic or `priv_key` into websites, chats, or support tickets.

### macOS and Linux

Download the latest AIOZ DePIN CLI

For macOS - x86_64

```shell
curl -LO https://github.com/AIOZNetwork/aioz-depin-cli/releases/download/v1.2.5/aioz-depin-darwin-amd64-1.2.5.tar.gz
tar -xzf aioz-depin-darwin-amd64-1.2.5.tar.gz
mv aioz-depin-cli-darwin-amd64 aioz-depin-cli
```

For macOS - ARM64

```shell
curl -LO https://github.com/AIOZNetwork/aioz-depin-cli/releases/download/v1.2.5/aioz-depin-darwin-x86_64-1.2.5.tar.gz
tar -xzf aioz-depin-darwin-x86_64-1.2.5.tar.gz
mv aioz-depin-cli-darwin-x86_64 aioz-depin-cli
```

For Linux

```shell
curl -LO https://github.com/AIOZNetwork/aioz-depin-cli/releases/download/v1.2.5/aioz-depin-linux-amd64-1.2.5.tar.gz
tar -xzf aioz-depin-linux-amd64-1.2.5.tar.gz
mv aioz-depin-cli-linux-amd64 aioz-depin-cli
```

Verify the installation

```shell
./aioz-depin-cli version
```

The output should be the version of AIOZ DePIN CLI.

Generate a new mnemonic phrase and private key

```shell
./aioz-depin-cli keytool new --save-priv-key privkey.json
```

`--save-priv-key` writes the private key to file

Response

```json
{
  "address": "aioz1k28nzwgrwgzrwfuwsfcqjyvd0r4lfprql2c4uf",
  "address_hex": "0xB28F313903720437278E827009118d78eBf48460",
  "pub_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"AxSwg94OuvFIn...CqFunK3pMjV0I\"}",
  "priv_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PrivKey\",\"key\":\"rdWGOtJ/Uio4SD...BCCOfegAI9OGMIbE=\"}",
  "mnemonic": "rain wing olive skate effort present long myself combine ... glide absent spider effort attitude enemy mouse"
}
```

**IMPORTANT NOTE**

- Treat your `priv_key` JSON and mnemonic phrase as **wallet secrets**. Anyone who has them can **control your node rewards**.
- Use a **dedicated key for each node**; **do not reuse** the key from your main wallet, exchange account, or other nodes.
- Store backups in an **offline, encrypted location** such as encrypted USB drives, air-gapped devices, or hardware security modules (HSM).
- **Never paste** your mnemonic or `priv_key` into websites, chats, or support tickets.

Run the node

```shell
./aioz-depin-cli start --home nodedata --priv-key-file privkey.json
```

`--home` data folder of the node

`--priv-key-file` the private key file which the node starts with. If you do not specify the private key file, the node will ask for it from the standard input stream.

**Note**:
Because AIOZ DePIN CLI automatically updates itself by downloading and replacing the executable file, make sure to set file permission to writable.
AIOZ DePIN CLI has to stop to perform auto update, it should be run with `launchctl`(macOS) or `systemctl`(Linux) to start it again after update and at system boot.

## Usage

### View node status

For Windows

```shell
.\aioz-depin-cli.exe stats
```

For macOS and Linux

```shell
./aioz-depin-cli stats
```

Note: This command requires a running node. If your node is not on default port `1317`, you need to specify it with the flag `--endpoint`

Response

```json
{
  "storage": {
    "total_count": 4864,
    "total_size": 149967615893
  },
  "delivery": {
    "upstream_speed": 0
  },
  "transcoding": {
    "status": "Standby"
  }
}
```

### View reward

For Windows

```shell
.\aioz-depin-cli.exe reward balance
```

For macOS and Linux

```shell
./aioz-depin-cli reward balance
```

Note: This command requires a running node. If your node is not on default port `1317`, you need to specify it with the flag `--endpoint`

Response

```json
{
  "balance": [
    {
      "denom": "attoaioz",
      "amount": "7761729917265715262"
    }
  ],
  "storage_earned": [
    {
      "denom": "attoaioz",
      "amount": "810423534750216148"
    }
  ],
  "delivery_earned": [
    {
      "denom": "attoaioz",
      "amount": "7525653191257749557"
    }
  ],
  "transcoding_earned": [
    {
      "denom": "attoaioz",
      "amount": "525653191257749557"
    }
  ],
  "withdraw": [
    {
      "denom": "attoaioz",
      "amount": "1100000000000000000"
    }
  ],
  "delivery_counter": 16521
}
```

`balance` is the amount of reward that is available for withdrawal.

`storage_earned`, `delivery_earned`, `transcoding_earned` are the total amount of reward for storage, delivery and transcode since the beginning.

`withdraw` is the total amount of reward that has been withdrawn since the beginning.

`delivery_counter` is the counter that counts the number of delivery since the beginning.

### Withdraw reward

For Windows

```shell
.\aioz-depin-cli.exe reward withdraw --address 0x9A20600a143745404f1AA1C69Bd280f4bD5B4408 --amount 1aioz --priv-key-file privkey.json
```

For macOS and Linux

```shell
./aioz-depin-cli reward withdraw --address 0x9A20600a143745404f1AA1C69Bd280f4bD5B4408 --amount 1aioz --priv-key-file privkey.json
```

This command requires a running node. If your node is not on default port `1317`, you need to specify it with the flag `--endpoint`.

`--address` the address to withdraw the reward to. The reward is transferred on the **AIOZ Chain**.

`--amount` the amount of reward to withdraw. The unit can be `aioz` or `attoaioz`. 1 AIOZ equals 10¹⁸ attoaioz. Minimum withdrawal is 1 AIOZ. Example values: `1aioz`, `1.1aioz`, `1100000000000000000attoaioz`.

`--priv-key-file` the private key file that the node started with. If you do not specify the private key file, the node will ask for it from the standard input stream.

Response

```json
{
  "txid": "2604F553B62B70136967811B14BA8DB5706A2FA86EF7FD1A6899ECB3EF944D59"
}
```

**Note**: Withdrawal requests are rate-limited to **one request per hour**. Please plan your withdrawals accordingly.

### Recover private key from mnemonic phrase

For Windows

```shell
.\aioz-depin-cli.exe keytool recover "rain wing olive skate effort present long myself combine ... glide absent spider effort attitude enemy mouse" --save-priv-key privkey.json
```

For macOS and Linux

```shell
./aioz-depin-cli keytool recover "rain wing olive skate effort present long myself combine ... glide absent spider effort attitude enemy mouse" --save-priv-key privkey.json
```

`--save-priv-key` writes the private key to file.

Response

```json
{
  "address": "aioz1k28nzwgrwgzrwfuwsfcqjyvd0r4lfprql2c4uf",
  "address_hex": "0xB28F313903720437278E827009118d78eBf48460",
  "pub_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PubKey\",\"key\":\"AxSwg94OuvFIn...CqFunK3pMjV0I\"}",
  "priv_key": "{\"@type\":\"/ethermint.crypto.v1.ethsecp256k1.PrivKey\",\"key\":\"rdWGOtJ/Uio4SD...BCCOfegAI9OGMIbE=\"}"
}
```

