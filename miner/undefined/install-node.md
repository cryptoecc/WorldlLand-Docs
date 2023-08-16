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



## Window

윈도우 전용 Build파일을 다운로드합니다.

### 설치 프로그램 사용

ETH-ECC repogitory의 최신 릴리즈에서 설치 프로그램 **exe** 파일을 다운로드합니다.

<figure><img src="../../.gitbook/assets/image (15).png" alt=""><figcaption></figcaption></figure>

아래 그림과 같은 파란색 창이 나타나면 **추가정보**를 클릭하여 실행합니다.

<figure><img src="../../.gitbook/assets/image (17).png" alt="" width="375"><figcaption></figcaption></figure>

다운로드한 설치 파일을 실행합니다.

<figure><img src="../../.gitbook/assets/image (16).png" alt=""><figcaption></figcaption></figure>

다음 오류 메세지가 표시되면 설치경로를 환경변수에 수동으로 추가해야 합니다. 환경변수의 **Path**에 설치 경로를 추가합니다.

<figure><img src="../../.gitbook/assets/image.png" alt=""><figcaption></figcaption></figure>

환경변수의 Path에 설치경로를 추가합니다.

<figure><img src="../../.gitbook/assets/image (20).png" alt="" width="224"><figcaption></figcaption></figure>

<figure><img src="../../.gitbook/assets/image (21).png" alt="" width="563"><figcaption></figcaption></figure>

**기본 설치 경로 :**

```
C:\Program Files\worldland
```

<figure><img src="../../.gitbook/assets/image (22).png" alt="" width="399"><figcaption></figcaption></figure>



**Installation complete!**

Worldland를 실행하려면 다음 명령어를 작성하십시오.

```
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> worldland --datadir "USER_DATA_DIR" console
```





### Run and Build

### 1. Install Chocolatey

**Chocolatey package**는 필요한 build 도구를 쉽게 설치할 수 있는 방법을 제공합니다.

PowerShell 을 **관리자 모드**로 실행합니다.

```
PS C:\WINDOWS\system32>
```

PowerShell을 사용하여 Get-ExecutionPolicy가 제한되지 않았는지 확인해야 합니다.

```
PS C:\WINDOWS\system32> Get-ExecutionPolicy
```

Restricted인 경우 AllSigned 또는 Bypass로 설정합니다.

```
PS C:\WINDOWS\system32> Set-ExecutionPolicy AllSigned
```

또는

```
PS C:\WINDOWS\system32> Set-ExecutionPolicy Bypass -Scope Process
```

이제 다음 명령을 실행합니다.

```
Set-ExecutionPolicy Bypass -Scope Process -Force; [System.Net.ServicePointManager]::SecurityProtocol = [System.Net.ServicePointManager]::SecurityProtocol -bor 3072; iex ((New-Object System.Net.WebClient).DownloadString('https://community.chocolatey.org/install.ps1'))
```

명령이 완료될 때까지 몇 초간 기다립니다. 오류가 표시되지 않으면 Chocolatey를 사용할 준비가 된 것입니다.



### **2.** Installation

관리자 명령 프롬프트에서 다음 명령을 실행하여 build 도구를 설치ㄹ할 수 있습니다.

패키지를 설치하면 환경변수에 경로가 추가됩니다.

```
C:\Windows\system32> choco install git
C:\Windows\system32> choco install golang
C:\Windows\system32> choco install mingw
```



{% hint style="danger" %}
새로운 경로를 얻으려면 새 명령 프롬프트를 열어야 합니다.
{% endhint %}

ETH-ECC를 설치하려면 먼저 Go 작업공간 디렉토리를 생상한 다음 ETH-ECC 소스 코드를 생성 및 빌드할 수 있습니다.

```
C:\Users\xxx> mkdir src\github.com\cryptoecc
C:\Users\xxx> git clone https://github.com/cryptoecc/ETH-ECC src\github.com\cryptoecc\ETH-ECC
C:\Users\xxx> cd src\github.com\cryptoecc\ETH-ECC 
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go get -u -v golang.org/x/net/context
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go install -v ./cmd/...
```



오류가 발생하면 로그 메세지에 표시된 아래 명령을 실행하십시오. `fatal: detected dubious ownership in repository at`&#x20;

```
git config --global --add safe.directory "USER_DATA_DIR"
```

또는 build가 실패하면 아래 명령을 실행하고 다시 시도하세요.

```
C:\Users\xxx\src\github.com\cryptoecc\ETH-ECC> go mod tidy
```

**Installation complete!**

Worldland를 실행하려면 다음 명령을 작성하세요.

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
