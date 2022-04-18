# Table of Contents
1. [About SSH (SecureShell)](#About)
2. [Basic usage](#Basic)
	1. [Connect to a remote host](#Remote)
	2. [Copy data to the remote host](#copytoremote)
	3. [Copy data from the remote host](#copytohost)
	4. [SSH key authentification](#sshkey)

# Using SSH on the Simlab cluster 

## About SSH (SecureShell) <a name="About"></a>
Connection to the SIMLAB front end is done via `ssh`.
 
## Basic usage <a name="Basic"></a>
### Connect to the remote host <a name="Remote"></a>
Connecting directly to the cluster frontends is restricted to networks within the university. So being connected to the university network is needed, or using a VPN, then you can connect via this command: 

```sh
$ ssh -CY <login>@simlab-cluster.um6p.ma
```

for windows users you can use the command-line, or graphical interface third-party clients like [Putty](https://www.chiark.greenend.org.uk/~sgtatham/putty/) and [mobaxterm](https://mobaxterm.mobatek.net).

### Copy data to the remote host <a name="copytoremote"></a>
 For simple file transfers using a command line interface you can use [scp](https://en.wikipedia.org/wiki/Secure_copy_protocol):  

```sh
$  scp -r <filename>  <login>@simlab-cluster.um6p.ma:<remote_directory>
```

 ### Copy data from the remote host <a name="copytohost"></a>
 For simple file transfers using a command line interface you can use scp:  

```sh
$  scp -r <remote_directory> <login>@simlab-cluster.um6p.ma:<path/to/filename>
```

When running Windows, you can also use [WinSCP](https://winscp.net/eng/index.php), which has a graphical user interface.
 For more complex file transfers or a larger amount of files, we recommend using [rsync](https://en.wikipedia.org/wiki/Rsync). It provides more extensive functionality than scp.

### SSH key authentification <a name="sshkey"></a>

SSH key authentification is allowed on SIMLAB. You have to generate a pair of keys following [SIMLAB recommendations](ssh-recommandation.md) and type:
```sh
$ ssh-copy-id <login>@simlab-cluster.um6p.ma
```
It copies your public key in the file `$HOME/.ssh/authorized_keys` on SIMLAB.
