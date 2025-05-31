# Introduction 

Development Environment configuration instructions for 
[East Texas A&M University](https://www.tamuc.edu/dept-of-computer-science-and-information-systems/)
Computer Science and Information System classes.  The development
environment you set up here may be used for many class assignment,
such as data structures, operating systems, computer architecture,
etc. for both undergraduate and graduate computer science classes.

This repository mainly consists of instructions for setting up a
Visual Studio Code (VSCode) development environment that uses Docker
Development Containers (DevContainers) and can be used to submit
assignment in GitHub classrooms using git tools.  You will need a relatively recent
computing system, either laptop or desktop.  It is recommended you use
a system with at least 4GB of memory, though probably at least 8GB
is needed.  Likewise you will need at least 10GB of free space to create
install the software and be able to create a container, possibly more.

You should be able to set up a VSCode DevContainer
environment on Intel/AMD X86_64 hardware or Apple Silicon M1/M2/M3/M4 Arm
architectures.  You should be able to set up the needed development
environment on a Windows, Mac or Linux operating system based machine.
Chromebooks or Android OS are not supported for this
configuration.

The purpose of using VSCode and Docer DevContainers in our classes is so
that we can specify the operating system and development tools and
configuration that should be present for a class assignment.  By opening
and developing code in a Docker provided container for a class, you will
ensoure you have a common setup and all the tools needed to work
on the assignmet. Assignments you are given will assume you are using the exact
development environment and version of these tools, so that we will
minimize any problems from using different versions of build tools or
build environments.  

# System requirements

It is recommended you have 8GB or more of main memory.  You should have
20GB of free space on your drive in order to install the tools and create
a container.

- **MacOS:** 
  - Macs with Apple Silicon M1/M2/M3/M4 chips, as well as Intel architecture
    based macs should work.
  - As long as the most recent version of Docker installs on your system and the
    Docker engine can run, you should have adequate enough hardware to use these tools.

- **Windows:** 
  - You should use a system with at least Windows 10 or Windows 11.
  - You need to have a Windows 10/11 that has WSL (Windows Subsystem for Linux)
    support enabled.
  - Make sure that virtualization is enabled in your BIOS (see instructions below).
  - As long as the most recent version of Docker installes on your system and the
    Docker engine can run, you should have adequate enough hardware to use these tools.

- **Linux:** 
  - If you are using a Ubuntu 22 distribution, or a distribution released in 2022 or after, you
    should be able to run these tools.
  - However, Linux based systems do not use Docker Desktop engine, so the docker
    installation described below is different for Linux systems.

# Instructions

You can watch this video [Video showing Setting Up your DevContainer](set me) 
in which we show an example of performing the steps described below.
This video shows setting up and installing docker and VSCode on a
Windows 11 system, but the steps are mostly the same whether you are
using Windows or Mac OS.

## STEP 1: Create GitHub account and install and configure `git`

You should first install the `git` tools on your system and configure `git` `ssh` keys to access
your GitHub account.

  - **Create GitHub Account**
  
  If you don't have one already, sign up for a free [GitHub account](https://github.com/)
  
  Make sure that you use your student@leomail.tamuc.edu as the primary e-mail address, if at all possible.
  
  - **Install Git and SSH tools**
  
  1. If you are using MacOS or Linux, you may already have a `git` client installed.  On a Windows system you will
   not have `git` already installed.  In all cases, check if `git` is installed by opening a terminal
   on your system and executing:
   ```
   $ git --version
   ```
   On MacOS systems, often it will give you the option to install XCode developer tools if git is currently
   not available.  You should accept this if you see it on MacOS to install the `git` tools.  If you do not
   have `git` on a MacOS or Linux system, it is usually easier to use your brew or Linux package manager to
   install the `git` tools on your system.

  2. For Windows machines, download and install the standard [Git Installer](https://git-scm.com/downloads).
  
     - You should accept all of the default options, except when asked for "Configuring the line ending conversions".
     Windows uses different line ending conventions, but our work will be done in a linux/unix
     environment.  So make sure you select the option to not convert cr/lf endings
     "Checkout as-is, commit as-is".
  
  3. For all operating systems, you need to perform the following git configuration steps.  
     [Initial Git Configuration](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup) 
   and [How to Set up SSH and Generate an SSH Key on Windows 11](https://davidaugustat.com/windows/windows-11-setup-ssh)
   Open up a command line terminal and perform the configuration and generate an `ssh` key like this:
   ```
   $ git config --global user.name "John Doe"
   $ git config --global user.email johndoe@example.com
   $ git config --global core.autocrlf false
   $ git config --list
   $ ssh-keygen
   Generating public/private rsa key pair.
   Enter file in which to save the key (C:\Users\Quickemu/.ssh/id_rsa):
   Created directory 'C:\\Users\\Quickemu/.ssh'.
   Enter passphrase (empty for no passphrase):
   Enter same passphrase again:
   Your identification has been saved in C:\Users\Quickemu/.ssh/id_rsa
   Your public key has been saved in C:\Users\Quickemu/.ssh/id_rsa.pub
   The key fingerprint is:
   SHA256:nywXiR8TIePPUsVVt5wNu5PdmYYgQXkLMXkhD09Shy0 quickemu@classdemo
   The key's randomart image is:
   +---[RSA 3072]----+
   |        +O*==oo.o|
   |       . *XEo..o=|
   |        ..*+o .+.|
   |         =.+. .++|
   |        S B  .++o|
   |         = =  .. |
   |        . *      |
   |         o       |
   |                 |
   +----[SHA256]-----+
   
   ```
     Make sure that you use your real name here and in your GitHub account
   for class assignments.  Also ensure that the e-mail address you
   specify in the `git config` is the same as the primary e-mail
   address you use in creating your GitHub account.
   
  4. Copy the generated ssh key to your GitHub account.  The second link in previous step shows this.  There will be a file
     named something like `c:\Users\username\.ssh\id_rsa.pub` in your home directory, though the location of your home directory
   will differ depending on your operating system.  This file is in a hidden directory (starts with a .), so you may not
   be able to see it in a file browser on your system unless you enable viewing hidden files/directories.  Find the public
   key, and copy it.  Then create a new ssh key in GitHub and paste in this public key.
   
  5. **IMPORTANT** If you have never connected to Github before using ssh, you should ensure that Github is an known host and that your ssh
   key access that you just configured is working.  Do the following to test this:
   ```
   $ ssh git@github.com
    The authenticity of host 'github.com (140.82.112.4)' can't be established.
    ECDSA key fingerprint is SHA256:p2QAMXNIC1TJYWeIOttrVc98/R1BUFWu3/LiyKgUfQM.
    Are you sure you want to continue connecting (yes/no/[fingerprint])? yes
    Warning: Permanently added 'github.com,140.82.112.4' (ECDSA) to the list of known hosts.
    PTY allocation request failed on channel 0
    Hi tamucstudent! You've successfully authenticated, but GitHub does not provide shell access.
    Connection to github.com closed.
   ```

   And say 'yes' if prompted to add Github as a known host as shown here.  If it says you have successfully
   authenticated, then you probably have configured your ssh key correctly for Github use.  If this step does
   not successfully connect, do no proceed until you get help or correctly set up your ssh key to be able to
   access your GitHub account.

  6. **IMPORTANT** Most Windows users, and sometiems MacOS users, find that the `ssh-agent` is not automatically
   configured and running for them when they install the `git` tools.  When you create a container, your key needs
   to be communicated into the container so that you can access your GitHub account using it.  If the `ssh-agent`
   is not running, this will not happen and you won't be able to create and push commits from inside your container.

   On a Windows system you can enable the `ssh-agent` as follows.  You should open the `Windows Services`, see if you
   have the OpenSSH Authentication Agent. Set the startup type to "Automatic (Delayed Start)" and start the agent,
   
   You can also try to start it by hand by opening a terminal and performing:
   ```
   $ ssh-agent
   ```
   But this will only start it for the current system, and it will not be restarted on a reboot.
   When `ssh-agent` is running, ensure that your `ssh` key is added to and available for the
   agent.  On a termin perform:
   ```
   $ ssh-add .ssh\id_ed25519
   ```
   to add your `id_ed25519` key for example to the `ssh-agent` list of keys.  You can also check if the
   agent is running and if so see which keys it is managing by performing
   ```
   $ ssh-add -l
   ```


## STEP 2: Install and configure Docker for your operating system.

Once you have git installed and configured, and your `ssh-agent` is running and managing your key, and you can
access your GitHub account using your ssh key, you should then install and configure docker.

- **Windows Users Only**

Docker now uses WSL (Windows Subsystem for Linux) as its backend for its Docker containers.  If WSL is not setup and active,
Docker is supposed to attempt to configure it for you and create an initial default WSL container.  Howerver in my experince this
setup by Docker of WSL often does not work fully or correctly.

  1. Open a terminal and perform the following to ensure the WSL system is installed and available.
   ```
   $ wsl --install
   ```
  2. Once WSL is installed, ensure a default container is downloaded and available on the system
  ```
  $ wsl --install ubuntu
  ```

- **Windows/Mac:** Get the most recent Docker Desktop installer from [here](https://www.docker.com/get-started/).
 and run the installer on your system.


  **NOTE**: You may need to enable hardware virtualizaiton if you own an Intel / AMD PC.
  
    When booting up, enter your system BIOS

    - [How to Enter the BIOS on Any PC: Access Keys by Manufacturer](https://www.tomshardware.com/reviews/bios-keys-to-access-your-firmware,5732.html)

  Usually the `F2` key should work, but if not there should usually be
  a message on your first boot screen telling you what the BIOS access
  key is.

  In your BIOS, find the setting for hardware Virtualization

    - [Enabling Intel VT or AMD-V virtualization hardware extensions in BIOS](https://docs.redhat.com/en/documentation/red_hat_enterprise_linux/5/html/virtualization/sect-virtualization-troubleshooting-enabling_intel_vt_and_amd_v_virtualization_hardware_extensions_in_bios#sect-Virtualization-Troubleshooting-Enabling_Intel_VT_and_AMD_V_virtualization_hardware_extensions_in_BIOS) 

  Once the installer finishes, you will need to reboot your system.  This might be a good time to get into your BIOS and check your
  virtualization settings if you are unsure.  After reboot, start the Docker Desktop application.  There is a setting to have Docker Desktop
  start automatically on login if you prefer.  In either case you need to ensure that Docker Desktop is running and it says that the
  "engine started" (bottom left of Docker Desktop), before you will be able to create and start a container in VSCode.

## STEP 3: Install VSCode Editor 

Download and install the VSCode Editor on your system from [here](https://code.visualstudio.com/)

There should be standard installers for Windows, Mac and Linux available here, as well as
instructions on how to run the installers if needed.

## STEP 4: Install Microsoft Remote Development Containers 

Once you have VSCode installed, start it up.  You need to install the Micsosoft Remote Dev Containers
extension.  The easiest way to do this is to open up the `Extensions` section in VSCode and search
for "Dev Containers".  When you find the official extension provided by Microsoft, install it in you
VSCode IDE.

The Remote Containers extension page is [here](https://marketplace.visualstudio.com/items?itemName=ms-vscode-remote.remote-containers)

## STEP 5: Test Creating and Opening Docker DevContainers

This repository has a `.devcontainer` directory that can be used to test that your Docker/VSCode DevContainer configuration is working.

  1. Clone a new repository using the Docker `Source Control` (left hand side) area.  Clone the `http` url of this repository to
   a local directory on your host system.
  2. Open the repository in a new VSCode folder when asked.
  3. If Docker Desktop engine is running, you should get a popup (lower right) asking to reopen the Folder in a Container.  Accept
   `Yes`.  If you don't see the popup, you ay not have the `Dev Containers` extension installed, Docker Desktop may not be running,
   or there may be other issues.
  4. If you can successfully reopen in a container, open a terminal inside of your running container and perform a
   ```
   $ ssh git@github.com
   ```
   from inside of the container to test that your `ssh` key has been communicated into the container.  If you get a permission
   denied: ssh key error, probably you need to follow the steps again to check and enable your `ssh-agent`.

# References

- Using remote DevContainers in VSCode:  https://code.visualstudio.com/docs/remote/containers
- Creating DevContainers in VSCode:  https://code.visualstudio.com/docs/remote/create-dev-container
- Windows Subsystem for Linux as Docker container back end on Windows 10: https://docs.microsoft.com/en-us/windows/wsl/tutorials/wsl-containers
- Initial git configuration: https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup
- Creating SSH key for remote GitHub repositories: https://davidaugustat.com/windows/windows-11-setup-ssh


