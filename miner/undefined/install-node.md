# Install Node

This page explains how to download and build the **ETH-ECC** source code and install the **Worldland nod**e.

## Hardware Requirements

<table><thead><tr><th width="147.33333333333331"></th><th>Minimum</th><th>Recommended</th></tr></thead><tbody><tr><td>CPU</td><td>2+ cores</td><td>Fast CPU with 4+ cores</td></tr><tr><td>RAM</td><td>4GB</td><td>16GB+ RAM</td></tr><tr><td>Storage </td><td>500GB free storage</td><td>500 high-performance SSD </td></tr><tr><td>Internet</td><td>8 MBit/sec</td><td>25+ MBit/sec</td></tr></tbody></table>



## Linux and Mac

### 1. Environment

**ETH-ECC** package uses the following two environment

* **Linux Ubuntu 18.04 or later**
* **Go (version 1.18 or later)**

We wrote the document based on **Ubuntu**, but it is expected to work on **UNIX-like operating systems** as well.

Download the basic packages needed for the build.

```
$ sudo apt update
$ sudo apt upgrade
```

For building ETH-ECC, it requires **Go** (version 1.18 or later). You can install them using the following commands.

```
$ sudo apt install gcc
$ sudo apt install make
$ sudo apt install snapd
$ sudo snap install go --classic
```

Then Go will be installed

Check the **version of Go** (version 1.18 or later)

```
$ go version
```

### 2. Installation

You can download **ETH-ECC** by cloning the **ETH-ECC** repository.

```
$ git clone https://github.com/cryptoecc/ETH-ECC
```

Once dependencies are installed, You can install ETH-ECC using the following command.\
Then move to `/ETH-ECC`, and follow this.

```
$ cd ETH-ECC
$ make worldland
```

or to **build** the full suite of utilities:

```
$ make all
```

**Installation complete!**

To **run** the WorldLand, write the following command.

```
./worldland -datadir "USER_DATA_DIR" console
```



## Window

### 1. Install Chocolatey

The **Chocolatey package** manager provides an easy way to install the build tools you need.

Run **PowerShell** in **administrator** mode.

```
PS C:\WINDOWS\system32>
```

With **PowerShell**, you must ensure [Get-ExecutionPolicy](https://go.microsoft.com/fwlink/?LinkID=135170) is not Restricted.&#x20;

```
PS C:\WINDOWS\system32> Get-ExecutionPolicy
```

If it is Restricted, set it to **AllSigned** or **Bypass.**

```
PS C:\WINDOWS\system32> Set-ExecutionPolicy AllSigned
```

or

```
PS C:\WINDOWS\system32> Set-ExecutionPolicy Bypass -Scope Process
```

Now run the following command:

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

Wait a few seconds for the command to complete. If you don't see any errors, you are ready to use **Chocolatey**!&#x20;

### **2.** Installation

Then you can run the following command from an **administrator** command prompt to install the build tools:

Installing these packages sets the path environment variable.&#x20;

```
C:\Windows\system32> choco install git
C:\Windows\system32> choco install golang
C:\Windows\system32> choco install mingw
```





{% hint style="danger" %}
You will need to open a **new command prompt** to get the new path.
{% endhint %}

To install **ETH-ECC**, you can first create a **Go workspace** directory, then create and build the **ETH-ECC** source code.

```
C:\Users\xxx> mkdir src\github.com\cryptoecc
C:\Users\xxx> git clone https://github.com/cryptoecc/ETH-ECC src\github.com\cryptoecc\ETH-ECC
C:\Users\xxx> cd src\github.com\cryptoecc\ETH-ECC 
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go get -u -v golang.org/x/net/context
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go install -v ./cmd/...
```



If you get `fatal: detected dubious ownership in repository at` **error** Execute the command below indicated in the log message.

```
git config --global --add safe.directory "USER_DATA_DIR"
```

or the build fails, run the command below and retry.

```
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go mod tidy
```

**Installation complete!**

To **run** the WorldLand, write the following command.

```
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> worldland --datadir "USER_DATA_DIR" console
```







***

#### References:

{% embed url="https://geth.ethereum.org/docs/getting-started/installing-geth" %}

{% embed url="https://chocolatey.org/install#individual" %}



***
