Development Environment for Renner
-----------------------------------

## Prerequisites:
 - [Chocolatey](https://chocolatey.org/) - it's a piece of cake! 
 - VirtualBox
 - Vagrant

#### If you haven't the prerequisites above, let's start with chocolatey.

### You'll need check before:
 - .NET Framework 4+
 - PowerShell v3+

### Then run this command in powershell with admin credentials:

```powershell
PS C:\set-executionpolicy remotesigned; get-executionPolicy
```
[https://technet.microsoft.com/pt-br/library/ee176961.aspx](https://technet.microsoft.com/pt-br/library/ee176961.aspx)

[http://ss64.com/ps/set-executionpolicy.html](http://ss64.com/ps/set-executionpolicy.html)

### To install chocolatey, run this command in powershell with admin credentials:

```powershell
PS C:\iwr https://chocolatey.org/install.ps1 -UseBasicParsing | iex
```

### After that, open the cmd with admin privileges:

```cmd
C:\choco install git.install virtualbox vagrant curl openssh -y
```

#### Your development environment is ready.
#### Now just download the repository and access the folder.

## Finally run this command:

```cmd
C:\[myrepo]\vagrant up
```