# Install Node

#### _Please contact us if you have any questions._ [_https://open.kakao.com/o/gXdk2J5e_](https://open.kakao.com/o/gXdk2J5e)

This page explains how to download and build the **ETH-ECC** source code and install the Worldland node.

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

For building ETH-ECC, it requires Go (version 1.18 or later). You can install them using the following commands.

```
$ sudo apt install gcc
$ sudo apt install make
$ sudo apt install snapd
$ sudo snap install go --classic
```

Then Go will be installed

Check the version of Go (version 1.18 or later)

```
$ go version
```

### 2. Installation

You can download **ETH-ECC** by cloning the ETH-ECC repository.

```
$ git clone https://github.com/cryptoecc/ETH-ECC
```

Once dependencies are installed, You can install ETH-ECC using the following command.\
Then move to `/ETH-ECC`, and follow this.

```
$ cd ETH-ECC
$ make worldland
```

or to build the full suite of utilities:

```
$ make all
```



If you're running a geth node for the first time, or if you've run a different version of Ethereum or a chain with a different network number, run the following to initialize your locally stored block data

```
$ rm -rf ~/.ethereum
```

## Window

### 1. Install Chocolatey

The Chocolatey package manager provides an easy way to install the build tools you need.

**Run Windows Terminal or PowerShell in administrator mode.**

```
PS C:\WINDOWS\system32>
```

With PowerShell, you must ensure [Get-ExecutionPolicy](https://go.microsoft.com/fwlink/?LinkID=135170) is not Restricted.&#x20;

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
C:\WINDOWS\system32> Get-ExecutionPolicyRestrictedSet-ExecutionPolicy AllSignedSet-ExecutionPolicy Bypass -Scope Process
```

Wait a few seconds for the command to complete. If you don't see any errors, you are ready to use Chocolatey!&#x20;

### **2.** Installation

런 다음 빌드 도구를 설치하기 위해 관리자 명령 프롬프트에서 다음 명령을 실행할 수 있습니다.

```
C:\Windows\system32> choco install git
C:\Windows\system32> choco install golang
C:\Windows\system32> choco install mingw
```

Installing these packages sets the path environment variable. You will need to open a new command prompt to get the new path. To install **ETH-ECC**, you can first create a Go workspace directory, then create and build the **ETH-ECC** source code.

```
C:\Users\xxx> mkdir src\github.com\cryptoecc
C:\Users\xxx> git clone https://github.com/cryptoecc/ETH-ECC src\github.com\cryptoecc\ETH-ECC
C:\Users\xxx> cd src\github.com\cryptoecc\ETH-ECC 
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go get -u -v golang.org/x/net/context
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go install -v ./cmd/...
```

If the build fails, run the command below and retry.

```
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go mod tidy
```



Reference:

[https://geth.ethereum.org/docs/getting-started/installing-geth](https://geth.ethereum.org/docs/getting-started/installing-geth)

[https://chocolatey.org/install#individual](https://chocolatey.org/install#individual)\


