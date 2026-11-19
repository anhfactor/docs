# Install Terraform

### **Install Terraform** <a href="#installterraform-installterraform" id="installterraform-installterraform"></a>

To use Terraform, you will need to install it (You can install Terraform according to the instructions at the [Terrafrom homepage](https://developer.hashicorp.com/terraform/tutorials/aws-get-started/install-cli) or you can install it according to our article below).

HashiCorp phân phối Terraform dưới dạng **binary package**. Bạn cũng có thể cài đặt Terraform bằng các trình quản lý gói phổ biến.

**Step 1**: Install Terraform

**Step 1.1**: Retrieve `TERRAFORM` `binary` by downloading Pre-complied binary or Compile from source follow the instructions below:

#### **Pre-complied binary** <a href="#installterraform-pre-compliedbinary" id="installterraform-pre-compliedbinary"></a>

To install `TERRAFORM`, find the [appropriate package](https://developer.hashicorp.com/terraform/downloads) for your system and download it as a zip file.

After downloading Terraform, unzip the package. Terraform runs as a binary terrain uniquely named `TERRAFORM`. Any other files in the package can be safely deleted and Terraform will still work.

Finally, make sure that your `TERRAFORM binary` is available on your PATH. This process will vary depending on your operating system.



#### **Pre-complied binary** <a href="#installterraform-pre-compliedbinary.1" id="installterraform-pre-compliedbinary.1"></a>

Để biên dịch tệp nhị phân Terraform từ nguồn, hãy sao chép kho lưu trữ [HashiCorp Terraform](https://github.com/hashicorp/terraform).

| `git clone https://github.com/hashicorp/terraform.git` |
| ------------------------------------------------------ |

Điều hướng đến thư mục mới.

| `cd terraform` |
| -------------- |

Sau đó, biên dịch binary. Lệnh này sẽ biên dịch tệp binary và lưu trữ nó trong _$GOPATH/bin/terraform_.

| `go install` |
| ------------ |

Cuối cùng, đảm bảo rằng `TERRAFORM binary` có sẵn trên PATH của bạn. Quá trình này sẽ khác nhau tùy thuộc vào hệ điều hành của bạn.

To compile the Terraform binary from source, clone the HashiCorp Terraform.

| `git clone https://github.com/hashicorp/terraform.git` |
| ------------------------------------------------------ |

Navigate to the new folder.

| `cd terraform` |
| -------------- |

Then compile binary. This command will compile the binary and store it in $GOPATH/bin/terraform.

| `go install` |
| ------------ |

Finally, make sure that  `TERRAFORM binary` is available on your . This process will vary depending on your operating system.

**Step 1.2**: Install on Mac or Linux:

Print a colon-separated list of locations in your PATH.

| `echo $PATH` |
| ------------ |

Move the  `TERRAFORM binary` to one of the listed locations. This command assumes that the binary is present in your download directory and that your PATH includes /usr/local/bin, but you can customize it if your location is different.

| `sudo ~/Downloads/terraform /usr/local/bin/` |
| -------------------------------------------- |

For more details on adding  binaries  to your  binary paths, check out this [Stack Overflow](https://stackoverflow.com/questions/14637979/how-to-permanently-set-path-on-linux-unix) article.

**Step 1.2**: Install on Windows

This [Stack Overflow](https://stackoverflow.com/questions/1618280/where-can-i-set-path-to-make-exe-on-windows) article contains instructions for setting PATH on Windows through the user interface.

<br>

**Xác minh cài đặt**

Verify that the installation worked by opening a new terminal session and listing the available Terraform subcommands.

| `terraform -helpUsage: terraform [-version] [-help] <command> [args]` `The available commands for execution are listed below.The most common, useful commands are shown first, followed byless common or more advanced commands. If you're just gettingstarted with Terraform, stick with the common commands. For theother commands, please read the help and docs before usage.#...` |
| -------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |

Add any subcommands to TERRAFORM -HELP to learn more about what this command does and the options available.

| `terraform -help plan` |
| ---------------------- |

### **Troubleshoot** <a href="#installterraform-troubleshoot" id="installterraform-troubleshoot"></a>

If you get an error that the terrain cannot be found, your PATH environment variable is not set up properly. Please go back and make sure your PATH variable contains the Terraform installation directory.

### **Turn on Tab completion** <a href="#installterraform-turnontabcompletion" id="installterraform-turnontabcompletion"></a>

If you use Bash or Zsh, you can enable tab completion for Terraform commands. To enable autocomplete, first make sure that a configuration file exists for your chosen shell.

**Bash**

| `touch ~/.bashrc` |
| ----------------- |

**Zsh**

| `touch ~/.zshrc` |
| ---------------- |

Then install the autocomplete package.

| `terraform -install-autocomplete` |
| --------------------------------- |

Once autocomplete support is installed, you will need to restart your shell.

***

### **Quick Start**  <a href="#installterraform-quickstart" id="installterraform-quickstart"></a>

Now that you have Terraform installed, you can provision an NGINX server in less than a minute using Docker on Mac, Windows, or Linux. You can also follow the rest of this tutorial in your web browser.

**Step 1**: Click the tab(s) below relevant to your operating system.

**Docker Desktop for Mac**

Download [Docker Desktop for Mac](https://docs.docker.com/desktop/install/mac-install/)

After you install Terraform and Docker on your local machine, start Docker Desktop.

| `open -a Docker` |
| ---------------- |

**Docker Desktop for Window**

To run Docker on your Windows 10 machine, you must use the Windows Subsystem for Linux (WSL2). [Download and install WSL2 ](https://learn.microsoft.com/en-us/windows/wsl/install)before continuing.

Download[ Docker Desktop for Windows](https://docs.docker.com/desktop/install/windows-install/).

After you install Terraform and Docker on your local machine, start Docker Desktop by searching for Docker from your Start Menu and selecting Docker Desktop in the search results. As long as the whale icon in the status bar remains stable, Docker Desktop is active and accessible from any terminal window.

For more information about Docker Desktop for Windows requirements, visit the [Docker documentation](https://docs.docker.com/desktop/install/windows-install/#start-docker-desktop).

**Docker Engine for Linux**

To follow this tutorial on Linux, first install the [Docker Engine](https://docs.docker.com/engine/install/) for your distro.

**Step 2**: Create a folder named _learn-terraform-docker-container._

| `mkdir learn-terraform-docker-container` |
| ---------------------------------------- |

This working directory contains configuration files that you write to describe the infrastructure you want Terraform to create and manage. When you initialize and apply the configuration here, Terraform uses this directory to store required plugins, modules (pre-written configurations), and information about the actual infrastructure it has created.

**Step 3**: Navigate to the working directory.

| `cd learn-terraform-docker-container` |
| ------------------------------------- |

In the working directory, create a file named **`main.tf`**  and paste the Terraform configuration (Server, Container, LB) after that.

<br>
