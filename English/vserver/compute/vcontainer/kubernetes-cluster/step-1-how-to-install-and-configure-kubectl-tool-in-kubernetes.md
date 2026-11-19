# Step 1: How to install and configure kubectl tool in Kubernetes

The command-line tool in Kubernetes, kubectl, allows you to execute commands in Kubernetes clusters. You can use kubectl to deploy applications, monitor and manage cluster resources, and view logs.

<figure><img src="https://docs.vngcloud.vn/download/attachments/59802429/image2023-5-30_10-9-48.png?version=1&#x26;modificationDate=1685499893000&#x26;api=v2" alt=""><figcaption></figcaption></figure>

### **Before you begin** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-beforeyoubegin" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-beforeyoubegin"></a>

You need to use a kubectl version that is no more than one version wrong with the cluster version. For example, a v1.2 client should work with master v1.1, v1.2 and v1.3. Using the latest version of kubectl helps to avoid unforeseen problems.

***

### **Install kubectl on Linux** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlonlinux" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlonlinux"></a>

#### **Install kubectl binary with curl on Linux** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlbinarywithcurlonlinux" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlbinarywithcurlonlinux"></a>

1. &#x20;Download the latest version with the command:\
   curl -LO https://[storage](https://www.thegioimaychu.vn/storage/).googleapis.com/kubernetes-release/release/\`curl -s https://[storage](https://www.thegioimaychu.vn/storage/).googleapis.com/kubernetes-release/release/stable.txt\`/bin/linux/amd64/kubectl\
   To download a specific version, replace the $(curl -s https://[storage](https://www.thegioimaychu.vn/storage/).[googleapis.com/kubernetes-release/release/stable.txt](http://googleapis.com/kubernetes-release/release/stable.txt)) part of the command with a specific version.\
   For example, to download v1.17.0 on Linux, enter the following:\
   `curl -LO https://`[`storage`](https://www.thegioimaychu.vn/storage/)`.googleapis.com/kubernetes-release/release/v1.17.0/bin/linux/amd64/kubectl`
2. Make the kubectl binary executable: **chmod +x ./kubectl**
3. Include the binary in your PATH environment: **variable.sudo mv ./kubectl /usr/local/bin/kubectl**
4. Make sure that the version you have installed is the latest: **kubectl version**

#### **Install kubectl using package manager** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlusingpackagemanager" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlusingpackagemanager"></a>

* Ubuntu, Debian or HypriotOS
* CentOS, RHEL or Fedora\
  `sudo apt-get update && sudo apt-get install -y apt-transport-https curl -s https://packages.cloud.google.com/apt/doc/apt-key.gpg | sudo apt-key add - echo "deb https://apt.kubernetes.io/ kubernetes-xenial main" | sudo tee -a /etc/apt/sources.list.d/kubernetes.list sudo apt-get update sudo apt-get install -y kubectl`

#### **Install with snap** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installwithsnap" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installwithsnap"></a>

If you are using Ubuntu or another Linux distro that supports snap package manager, then kubectl is already available in snap.

1. Switch to user snap and execute the install command:\
   `sudo snap install kubectl --classic`
2. Check that the version you just installed is the latest:\
   `kubectl version`

***

### **Install kubectl on macOS** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlonmacos" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlonmacos"></a>

#### Install kubectl binary with curl on macOS <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlbinarywithcurlonmacos" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlbinarywithcurlonmacos"></a>

1. Download the latest version:\
   curl -LO "[https://storage.googleapis.com/kubernetes-release/release/$](https://storage.googleapis.com/kubernetes-release/release/$)(curl -s [https://storage.googleapis.com/kubernetes-release/release/stable.txt](https://storage.googleapis.com/kubernetes-release/release/stable.txt))/bin/darwin/ amd64/kubectl"\
   To download a specific version, replace the $(curl -s [https://storage.googleapis.com/kubernetes-release/release/stable.txt](https://storage.googleapis.com/kubernetes-release/release/stable.txt)) part of the command with the specific version.\
   For example, to download v1.17.0 on macOS, type:\
   curl -LO [https://storage.googleapis.com/kubernetes-release/releases/v1.17.0/bin/darwin/amd64/kubectl](https://storage.googleapis.com/kubernetes-release/releases/v1.17.0/bin/darwin/amd64/kubectl)
2. Make the kubectl binary executable:\
   chmod +x ./kubectl
3. Include the binary in your PATH environment variable.\
   sudo mv ./kubectl /usr/local/bin/kubectl
4. Make sure that the version you have installed is the latest:\
   kubectl version

#### **Install with Homebrew on macOS** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installwithhomebrewonmacos" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installwithhomebrewonmacos"></a>

If you are on macOS and using the [Homebrew](https://brew.sh/) package manager, you can install kubectl with Homebrew.

1. Run the install command:\
   `brew install kubectl`\
   or\
   `brew install kubernetes-cli`
2. Make sure that the version you have installed is the latest:\
   `kubectl version`

#### **Install with Macports on macOS** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installwithmacportsonmacos" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installwithmacportsonmacos"></a>

If you are on macOS and use the [Macports](https://macports.org/) package manager, you can install kubectl with Macports.

1. Run the install command:\
   `sudo port self-update`\
   `sudo port install kubectl`
2. Make sure that the version you have installed is the latest:\
   `kubectl version`

***

### **Install kubectl on Windows** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlonwindows" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlonwindows"></a>

#### Install kubectl binary with curl on Windows <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlbinarywithcurlonwindows" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installkubectlbinarywithcurlonwindows"></a>

1. Download the latest version v1.17.0 from this link. Or if you have curl installed, use the following command:\
   `curl -LO` [`https://storage.googleapis.com/kubernetes-release/releases/v1.17.0/bin/windows/amd64/kubectl.exe`](https://storage.googleapis.com/kubernetes-release/releases/v1.17.0/bin/windows/amd64/kubectl.exe)\
   To find out the latest stable version, see [https://storage.googleapis.com/kubernetes-release/releases/stable.txt](https://storage.googleapis.com/kubernetes-release/releases/stable.txt).
2. Include the binary in your PATH environment variable.
3. Check that the kubectl version is the same as the downloaded one:\
   `kubectl version`

_**Note:** Docker Desktop for Windows adds its own version of kubectl to PATH. If you have installed Docker Desktop before, you may need to set your PATH before the Docker Desktop installation adds a PATH to or removes Docker Desktop's kubectl._

#### Install with Powershell from PSGallery <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installwithpowershellfrompsgallery" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installwithpowershellfrompsgallery"></a>

If you are on Windows and using the package manager [Powershell Gallery](https://www.powershellgallery.com/), you can install and update kubectl with Powershell.

1.  Execute the following installation commands (make sure you define  DownloadLocation yourself):\
    `Install-Script -Name install-kubectl -Scope CurrentUser -Force`\
    `install-kubectl.ps1 [-DownloadLocation <path>]`\
    &#xNAN;_**Note:** If you do not define DownloadLocation, kubectl  will be installed in the user's temp directory._

    The installation will generate `$HOME/.kube` and instructions for creating the configuration file
2. Make sure that the version you have installed is the latest:\
   `kubectl version`\
   &#xNAN;_**Note:** Update of the installation will be performed when rerunning the commands from step 1._

#### Install on Windows using Chocolatey or Scoop <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installonwindowsusingchocolateyorscoop" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installonwindowsusingchocolateyorscoop"></a>

To install kubectl on Windows you can use the package manager [Chocolatey](https://chocolatey.org/) or the command installer [Scoop](https://scoop.sh/).

* choco\
  `choco install kubernetes-cli`
* scoop\
  scoop install kubectl

1. Make sure that the version you have installed is the latest:\
   `kubectl version`
2. Navigate to your home directory:\
   `cd %USERPROFILE%`
3. Create folder  .kube:\
   `mkdir .kube`
4. Navigate to the  .kube  folder you just created:\
   `cd .kube`
5. Configure kubectl to use a remote Kubernetes cluster:\
   `New-Item config -type file`\
   &#xNAN;_**Note:** Edit the configuration file with a text editor, such as Notepad._

#### Download from part of Google Cloud SDK <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-downloadfrompartofgooglecloudsdk" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-downloadfrompartofgooglecloudsdk"></a>

You can install kubectl from part of the Google Cloud SDK.

1. Install Google Cloud SDK.
2. Execute the kubectl install command:\
   `gcloud components install kubectl`
3. Make sure that the version you have installed is the latest:\
   `kubectl version`

#### Verify kubectl . configuration <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-verifykubectl.configuration" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-verifykubectl.configuration"></a>

In order for kubectl to find and access the Kubernetes cluster, it needs a kubeconfig file, which is automatically created when you create a new cluster using kube-up.sh or successfully deploy a Minikube cluster. By default, kubectl's configuration is located at \~/.kube/config.

* Check that kubectl is properly configured by viewing the state of the cluster:\
  `kubectl cluster-info`
* If you see a response URL, then kubectl is properly configured to access your cluster.
* If you see a message similar to the one below, kuberctl is not configured correctly or cannot connect to the Kubernetes cluster.\
  The connection to the server \<server-name:port> was refused - did you specify the right host or port?
* For example, if you are going to run a Kubernetes cluster on your laptop (locally), you will need a tool like Minikube installed previously and run the commands above again.
* If kubectl cluster-info returns the url but you cannot access your cluster, then check it is configured correctly by:\
  `kubectl cluster-info dump`

### **kubectl . configuration options** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-kubectl.configurationoptions" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-kubectl.configurationoptions"></a>

#### Enable shell autocompletion <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-enableshellautocompletion" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-enableshellautocompletion"></a>

kubectl provides autocompletion support for Bash and Zsh, reducing the need to type multiple commands.

Below are the steps to set up autocompletion for Bash (including the differences between Linux and macOS) and Zsh.

***

### **Bash on Linux** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-bashonlinux" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-bashonlinux"></a>

#### Introduce <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-introduce" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-introduce"></a>

The kubelet completion script for Bash is generated with the kubectl completion bash command. After the script is generated, you need to source (execute) the script to enable autocompletion.

However, completion script depends on bash-completion, so you must install bash-completion first (check bash-completion exists with type \_init\_completion statement).

#### Install bash-completion <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-installbash-completion" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-installbash-completion"></a>

bash-completion is provided by many package managers (see [here](https://github.com/scop/bash-completion#installation)). You can install with `apt-get install bash-completion` or `yum install bash-completion` command.

The above commands `create /usr/share/bash-completion/bash_completion`, which is the main bash-completion script. Depending on your package manager, you must source (execute) this file in the file `~/.bashrc`.

To find this file, reload your current shell and run the command `type _init_completion`. If successful, you're all set, otherwise add the following to your `~/.bashrc` file:

`source /usr/share/bash-completion/bash_completion`\
Reload your shell and confirm bash-completion is properly installed using the `type _init_completion` command.

#### Enable kubectl autocompletion <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-enablekubectlautocompletion" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-enablekubectlautocompletion"></a>

Now you need to make sure that the kubectl completion script is sourced across all shell sessions. There are 2 ways to do this:

* Source script in file \~/.bashrc:\
  echo 'source <(kubectl completion bash)' >>\~/.bashrc
* Add the script to the /etc/bash\_completion.d directory:\
  kubectl completion bash >/etc/bash\_completion.d/kubectl
* If you have an alias for kubectl, you can add another shell completion for that alias:\
  echo 'alias k=kubectl' >>\~/.bashrc\
  echo 'complete -F \_\_start\_kubectl k' >>\~/.bashrc

_**Note:** bash-completion sources all completion scripts in /etc/bash\_completion.d._

The above methods are equally effective. After reloading the shell, kubectl autocompletion should work.

***

### **Zsh** <a href="#step1-howtoinstallandconfigurekubectltoolinkubernetes-zsh" id="step1-howtoinstallandconfigurekubectltoolinkubernetes-zsh"></a>

The Kubectl completion script for Zsh is generated with the kubectl completion zsh command. The source completion script in your shell will trigger kubectl autocompletion.

To make it work for all shells, add the following line to your `~/.zshrc` file:

`source <(kubectl completion zsh)`

If you have an alias for kubectl, you can extend shell completion to work with that alias:

`echo 'alias k=kubectl' >>~/.zshrc`\
`echo 'complete -F __start_kubectl k' >>~/.zshrc`

After reloading the shell, kubectl autocompletion should work.

If you get the error `complete:13: command not found: compdef`, add the following line at the top of your `~/.zshrc` file:

`autoload -Uz compinit`\
`compinit`

\
Source: [kubernetes.io](http://kubernetes.io/)
