# Truffle

(For Windows 10+, use WSL2 Ubuntu)

{% embed url="https://learn.microsoft.com/en-us/windows/wsl/install" %}

***

In the Ubuntu Terminal, write the commands below.

```bash
sudo apt update
sudo apt upgrade
```

Install nvm

```sh
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.39.1/install.sh | bash
source ~/.bashrc
nvm install --lts
```

Create and change a directory.

```sh
mkdir [YOUR_DIR_NAME]
cd [YOUR_DIR_NAME]
```

Install and initialize Truffle.

```sh
npm install -g truffle
truffle init
```

<figure><img src="https://raw.githubusercontent.com/cryptoecc/WorldlLand-Docs/master/.gitbook/assets/development-environment_truffle_01.png" alt=""><figcaption></figcaption></figure>

Now, you can add WorldLand Network via **truffle-config.js**

{% embed url="https://trufflesuite.com/docs/truffle/reference/configuration/#networks" %}

***
