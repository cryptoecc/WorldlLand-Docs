# Install Node

This page explains how to download and build the **ETH-ECC** source code and install the **Worldland nod**e.

## Hardware Requirements

<table><thead><tr><th width="147.33333333333331"></th><th>Minimum</th><th>Recommended</th></tr></thead><tbody><tr><td>CPU</td><td>2+ cores</td><td>Fast CPU with 4+ cores</td></tr><tr><td>RAM</td><td>4GB</td><td>8GB+ RAM</td></tr><tr><td>Storage </td><td>500GB free storage</td><td>500 high-performance SSD </td></tr><tr><td>Internet</td><td>8 MBit/sec</td><td>25+ MBit/sec</td></tr></tbody></table>



## Linux and Mac

### 1. 환경

#### **Linux**

Ubuntu 를 기반으로 문서를 작성했지만 Unix와 같은 운영체제에서도 작동할 것으로 예상됩니다.

build에 필요한 기본 패키지를 다운로드합니다.

```
$ sudo apt update
$ sudo apt upgrade
```

ETH-ECC를 build하려면 Go ( 버전 1.18 이상 )가 필요합니다. 다음 명령을 사용하여 설치할 수 있습니다.

```
$ sudo apt install gcc
$ sudo apt install make
$ sudo apt install snapd
$ sudo snap install go --classic
```



#### **Mac**

Ubuntu 를 기반으로 문서를 작성했지만 Unix와 같은 운영체제에서도 작동할 것으로 예상됩니다.

build에 필요한 기본 패키지를 다운로드합니다

```
$ sudo brew update
$ sudo brew upgrade
```

ETH-ECC를 build하려면 Go ( 버전 1.18 이상 )가 필요합니다. 다음 명령을 사용하여 설치할 수 있습니다.

```
$ sudo brew install gcc
$ sudo brew install make
$ sudo brew install snapd
$ sudo brew install go --classic
```



설치가 완료되었으면 Go 버전을 확인합니다. ( 1.18 이상)

```
$ go version
```



### 2. 설치

ETH-ECC repository 를 Clone 합니다.

```
$ git clone https://github.com/cryptoecc/ETH-ECC
```

위의 종속성들이 설치되면 다음 명령어를 사용하여 ETH-ECC를 build할 수 있습니다.

/ETH-ECC 경로로 이동해 주세요.

```
$ cd ETH-ECC
$ make worldland
```

또는 전체 utilities 를 활용하시려면 make all 명령어를 사용하세요.

```
$ make all
```

**Installation complete!**

Worldland를 실행하려면 다음 명령을 작성하세요.

```
./worldland --datadir "USER_DATA_DIR" console
```



## Windowkzx

### Using Installer

Download the installer **exe** file from the [**latest release**](https://github.com/cryptoecc/ETH-ECC/releases) of the **ETH-ECC repository**.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

If blue window like the picture below appears, click **More Information** and run it.

<figure><img src="../../.gitbook/assets/image (17).png" alt="" width="375"><figcaption></figcaption></figure>

Run the downloaded installer file.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

If the following error message is displayed, You must manually add the installation path to **environment variables**. Add the **installation path** to **Path** in your environment variables.&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Add the **installation path** to **Path** in your environment variables.&#x20;

<figure><img src="../../.gitbook/assets/image (20).png" alt="" width="224"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (21).png" alt="" width="563"><figcaption></figcaption></figure>

**Default installation path:**

```
C:\Program Files\worldland
```

<figure><img src="../../.gitbook/assets/image (22).png" alt="" width="399"><figcaption></figcaption></figure>



**Installation complete!**

To **run** the WorldLand, write the following command.

```
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> worldland --datadir "USER_DATA_DIR" console
```





### Run and Build

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







































## Linux and Mac

### 1. Environment

#### **Linux**

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



#### **Mac**

We wrote the document based on **Ubuntu**, but it is expected to work on **UNIX-like operating systems** as well.

Download the basic packages needed for the build.

```
$ sudo brew update
$ sudo brew upgrade
```

For building ETH-ECC, it requires **Go** (version 1.18 or later). You can install them using the following commands.

```
$ sudo brew install gcc
$ sudo brew install make
$ sudo brew install snapd
$ sudo brew install go --classic
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
./worldland --datadir "USER_DATA_DIR" console
```



## Window

You can use the **Windows Installer** or **build** the ETH-ECC **source code** yourself.

### Using Installer

Download the installer **exe** file from the [**latest release**](https://github.com/cryptoecc/ETH-ECC/releases) of the **ETH-ECC repository**.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

If blue window like the picture below appears, click **More Information** and run it.

<figure><img src="../../.gitbook/assets/image (17).png" alt="" width="375"><figcaption></figcaption></figure>

Run the downloaded installer file.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

If the following error message is displayed, You must manually add the installation path to **environment variables**. Add the **installation path** to **Path** in your environment variables.&#x20;

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

Add the **installation path** to **Path** in your environment variables.&#x20;

<figure><img src="../../.gitbook/assets/image (20).png" alt="" width="224"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (21).png" alt="" width="563"><figcaption></figcaption></figure>

**Default installation path:**

```
C:\Program Files\worldland
```

<figure><img src="../../.gitbook/assets/image (22).png" alt="" width="399"><figcaption></figcaption></figure>



**Installation complete!**

To **run** the WorldLand, write the following command.

```
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> worldland --datadir "USER_DATA_DIR" console
```





### Run and Build

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
