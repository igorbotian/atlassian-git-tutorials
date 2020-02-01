## Install Git

### Install Git on Mac OS X

There are several ways to install Git on a Mac. In fact, if you've installed XCode (or it's Command Line Tools), Git may already be installed. To find out, open a terminal and enter `git --version`.  
`$ git --version`    
`git version 2.7.0 (Apple Git-66)`

Apple actually maintain and ship [their own fork of Git](http://opensource.apple.com/source/Git/), but it tends to lag behind mainstream Git by several major versions. You may want to install a newer version of Git using one of the methods below:

#### Git for Mac Installer

The easiest way to install Git on a Mac is via the stand-alone installer:

1. Download the latest Git for Mac installer.
  
2. Follow the prompts to install Git.  

3. Open a terminal and verify the installation was successful by typing `git --version`:  
`$ git --version`  
`git version 2.9.2`
  
4. Configure your Git username and email using the following commands, replacing Emma's name with your own. These details will be associated with any commits that you create:    
`$ git config --global user.name "Emma Paris"`  
`$ git config --global user.email "eparis@atlassian.com"`  

5. (Optional) To make Git remember your username and password when working with HTTPS repositories, [configure the git-credential-osxkeychain helper](https://www.atlassian.com/git/tutorials/install-git#install-the-git-credential-osx).

#### Install Git with Homebrew

If you have [installed Homebrew](http://brew.sh/) to manage packages on OS X, you can follow these instructions to install Git:

1. Open your terminal and install Git using Homebrew:  
`$ brew install git`

2. Verify the installation was successful by typing which `git --version`:  
`$ git --version`  
`git version 2.9.2`  

3. Configure your Git username and email using the following commands, replacing Emma's name with your own. These details will be associated with any commits that you create:  
`$ git config --global user.name "Emma Paris"`  
`$ git config --global user.email "eparis@atlassian.com"`  

5. (Optional) To make Git remember your username and password when working with HTTPS repositories, install the [git-credential-osxkeychain helper](https://www.atlassian.com/git/tutorials/install-git#install-the-git-credential-osx).

#### Install Git with MacPorts

If you have [installed MacPorts](https://www.macports.org/install.php) to manage packages on OS X, you can follow these instructions to install Git:

1. Open your terminal and update MacPorts:  
`$ sudo port selfupdate`

2. Search for the latest available Git ports and variants:
`$ port search git`  
`$ port variants git`  

3. Install Git with bash completion, the OS X keychain helper, and the docs:
`$ sudo port install git +bash_completion+credential_osxkeychain+doc`  

4. Configure your Git username and email using the following commands, replacing Emma's name with your own. These details will be associated with any commits that you create:  
`$ git config --global user.name "Emma Paris"`  
`$ git config --global user.email "eparis@atlassian.com"`  

5. (Optional) To make Git remember your username and password when working with HTTPS repositories, configure the [git-credential-osxkeychain helper](https://www.atlassian.com/git/tutorials/install-git#install-the-git-credential-osx).

#### Install the git-credential-osxkeychain helper

Bitbucket supports pushing and pulling your Git repositories over both SSH and HTTPS. To work with a private repository over HTTPS, you must supply a username and password each time you push or pull. The **git-credential-osxkeychain** helper allows you to cache your username and password in the OSX keychain, so you don't have to retype it each time.

1. If you followed the MacPorts or Homebrew instructions above, the helper should already be installed. Otherwise you'll need to download and install it. Open a terminal window and check:  
`$ git credential-osxkeychain`  
`usage: git credential-osxkeychain <get|store|erase>`  
If you receive a usage statement, skip to step 4. If the helper is not installed, go to step 2.

2. Use curl to download git-credential-osxkeychain (or [download it via your browser](http://github-media-downloads.s3.amazonaws.com/osx/git-credential-osxkeychain)) and move it to `/usr/local/bin`:  
`$ curl -O http://github-media-downloads.s3.amazonaws.com/osx/git-credential-osxkeychain`  
`$ sudo mv git-credential-osxkeychain /usr/local/bin/`  

3. Make the file an executable:  
`$ chmod u+x /usr/local/bin/git-credential-osxkeychain`

4. Configure git to use the osxkeychain credential helper.  
`$ git config --global credential.helper osxkeychain`  
The next time Git prompts you for a username and password, it will cache them in your keychain for future use.

#### Install Git with Atlassian Sourcetree

Sourcetree, a free visual Git client for Mac, comes with its own bundled version of Git. You can [download Sourcetree here](https://www.sourcetreeapp.com/).

To learn how to use Git with Sourcetree (and how to host your Git repositories on Bitbucket) you can follow our comprehensive [Git tutorial with Bitbucket and Sourcetree](https://confluence.atlassian.com/bitbucket/tutorial-learn-bitbucket-with-sourcetree-760120235.html).

#### Build Git from source on OS X

Building Git can be a little tricky on Mac due to certain libraries moving around between OS X releases. On El Capitan (OS X 10.11), follow these instructions to build Git:

1. From your terminal install XCode's Command Line Tools (if you haven't already):  
`$ xcode-select --install`

2. Install [Homebrew](http://brew.sh/).

3. Using Homebrew, install openssl:  
`$ brew install openssl`

4. Clone the Git source (or if you don't yet have a version of Git installed, [download and extract it](https://github.com/git/git/archive/master.zip)):  
`$ git clone https://github.com/git/git.git`

5. To build Git run make with the following flags:  
`$ NO_GETTEXT=1 make CFLAGS="-I/usr/local/opt/openssl/include" LDFLAGS="-L/usr/local/opt/openssl/lib"`

### Install Git on Windows

#### Git for Windows stand-alone installer

1. Download the latest [Git for Windows installer](https://git-for-windows.github.io/).

2. When you've successfully started the installer, you should see the **Git Setup** wizard screen. Follow the **Next** and **Finish** prompts to complete the installation. The default options are pretty sensible for most users.

3. Open a Command Prompt (or Git Bash if during installation you elected not to use Git from the Windows Command Prompt).

4. Run the following commands to configure your Git username and email using the following commands, replacing Emma's name with your own. These details will be associated with any commits that you create:  
`$ git config --global user.name "Emma Paris"`  
`$ git config --global user.email "eparis@atlassian.com"`  

5. _Optional: Install the Git credential helper on Windows_  
Bitbucket supports pushing and pulling over HTTP to your remote Git repositories on Bitbucket. Every time you interact with the remote repository, you must supply a username/password combination. You can store these credentials, instead of supplying the combination every time, with the [Git Credential Manager for Windows](https://github.com/Microsoft/Git-Credential-Manager-for-Windows).

#### Install Git with Atlassian Sourcetree

Sourcetree, a free visual Git client for Windows, comes with its own bundled version of Git. You can [download Sourcetree here](https://www.sourcetreeapp.com/).

To learn how to use Git with Sourcetree (and how to host your Git repositories on Bitbucket) you can follow our comprehensive [Git tutorial with Bitbucket and Sourcetree](https://confluence.atlassian.com/bitbucket/tutorial-learn-bitbucket-with-sourcetree-760120235.html).

### Install Git on Linux

**Debian / Ubuntu (apt-get)**  
Git packages are available via [apt](https://wiki.debian.org/Apt):

1. From your shell, install Git using apt-get:  
`$ sudo apt-get update`  
`$ sudo apt-get install git`  

2. Verify the installation was successful by typing `git --version`:
`$ git --version`  
`git version 2.9.2`

Configure your Git username and email using the following commands, replacing Emma's name with your own. These details will be associated with any commits that you create:  
`$ git config --global user.name "Emma Paris"`  
`$ git config --global user.email "eparis@atlassian.com"`
  
**Fedora (dnf/yum)**  
Git packages are available via both [yum](https://fedoraproject.org/wiki/Yum) and [dnf](https://fedoraproject.org/wiki/Dnf):

1. From your shell, install Git using dnf (or yum, on older versions of Fedora):  
`$ sudo dnf install git`  
or  
`$ sudo yum install git`

2. Verify the installation was successful by typing `git --version`:  
`$ git --version`  
`git version 2.9.2`

3. Configure your Git username and email using the following commands, replacing Emma's name with your own. These details will be associated with any commits that you create  
`$ git config --global user.name "Emma Paris"`  
`$ git config --global user.email "eparis@atlassian.com"`  

#### Build Git from source on Linux

**Debian / Ubuntu**  

Git requires the several dependencies to build on Linux. These are available via [apt](https://wiki.debian.org/Apt):

1. From your shell, install the necessary dependencies using apt-get:  
`$ sudo apt-get update`  
`$ sudo apt-get install libcurl4-gnutls-dev libexpat1-dev gettext libz-dev libssl-dev asciidoc xmlto docbook2x`

2. Clone the Git source (or if you don't yet have a version of Git installed, [download and extract it](https://www.kernel.org/pub/software/scm/git/)):  
`$ git clone https://git.kernel.org/pub/scm/git/git.git`

3. To build Git and install it under `/usr`, run make:  
`$ make all doc info prefix=/usr`  
`$ sudo make install install-doc install-html install-info install-man prefix=/usr` 

**Fedora**

Git requires the several dependencies to build on Linux. These are available via both [yum](https://fedoraproject.org/wiki/Yum) and [dnf](https://fedoraproject.org/wiki/Dnf):

1. From your shell, install the necessary build dependencies using dnf (or yum, on older versions of Fedora):  
`$ sudo dnf install curl-devel expat-devel gettext-devel openssl-devel perl-devel zlib-devel asciidoc xmlto docbook2X`    
or using yum. For yum, you may need to install the Extra Packages for Enterprise Linux (EPEL) repository first:  
`$ sudo yum install epel-release`  
`$ sudo yum install curl-devel expat-devel gettext-devel openssl-devel perl-devel zlib-devel asciidoc xmlto docbook2X`  

2. Symlink docbook2X to the filename that the Git build expects:  
`$ sudo ln -s /usr/bin/db2x_docbook2texi /usr/bin/docbook2x-texi`  

3. Clone the Git source (or if you don't yet have a version of Git installed, [download and extract it](https://www.kernel.org/pub/software/scm/git/):  
`$ git clone https://git.kernel.org/pub/scm/git/git.git`  

4. To build Git and install it under `/usr`, run make:  
`$ make all doc prefix=/usr`  
`$ sudo make install install-doc install-html install-man prefix=/usr`
 