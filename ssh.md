---
title: SSH
date: 2021-01-27 11:48:05
icon: icon-style
background: bg-blue-400
tags:
categories:
    - Linux Command
intro: |
    This quick reference cheat sheet provides various for using SSH.
---

Getting started {.cols-3}
---------------

### Connecting
Connect to a server (default port 22)
```shell script
$ ssh root@192.168.1.5
```
Connect on a specific port
```shell script
$ ssh root@192.168.1.5 -p 6222
```
Connect via pem file (0600 permissions)
```shell script
$ ssh -i /path/file.pem root@192.168.1.5
```

### Executing
Executes remote command
```shell script
$ ssh root@192.168.1.5 'ls -l'
```
Invoke a local script
```shell script
$ ssh root@192.168.1.5 bash < script.sh
```
Compresses and downloads from a server
```shell script {.wrap}
$ ssh root@192.168.1.5 "tar cvzf - ~/source" > output.tgz
```



### scp {.row-span-2}

Copies from remote to local
```shell script
$ scp user@server:/dir/file.ext dest/
```
Copies between two servers
```shell script
$ scp user@server:/file user@server:/dir
```
Copies from local to remote 
```shell script
$ scp dest/file.ext user@server:/dir
```
Copies a whole folder
```shell script
$ scp -r user@server:/dir dest/
```
Copies all files from a folder
```shell script
$ scp user@server:/dir/* dest/
```
Copies from a server folder to the current folder
```shell script
$ scp user@server:/dir/* .
```


### Config location
System-wide ssh config
```shell script
/etc/ssh/ssh_config
```
User-specific ssh config
```shell script
~/.ssh/config
```


### SCP Options

| Options       | Description          |
|---------------|----------------------|
| scp `-C`      | <yel>C</yel>ompresses data      |
| scp `-v`      | Prints <yel>v</yel>erbose info  |
| scp `-P` 8080 | Uses a specific <yel>P</yel>ort |


### Config sample

```toml
Host server1 
    HostName 192.168.1.5
    User root
    Port 22
    IdentityFile ~/.ssh/server1.key
```

Launch by alias
```shell script
$ ssh server1
```
See: Full [Config Options](https://linux.die.net/man/5/ssh_config)



### ProxyJump

```shell script
$ ssh -J proxy_host1 remote_host2
```

```shell script {.wrap}
$ ssh -J user@proxy_host1 user@remote_host2
```

Multiple jumps
```shell script {.wrap}
$ ssh -J user@proxy_host1:port1,user@proxy_host2:port2 user@remote_host3
```

### ssh-copy-id
```shell script {.wrap}
$ ssh-copy-id user@server
```

Copy to alias server
```shell script {.wrap}
$ ssh-copy-id server1
```

Copy specific key
```shell script {.wrap}
$ ssh-copy-id -i ~/.ssh/id_rsa.pub user@server
```



SSH keygen {.cols-5}
---------------

### Explain {.col-span-2}

```shell script
$ ssh-keygen -t rsa -b 4096 -C "your@mail.com" 
```
----
|-  | -             | -                         |
|---|---------------|---------------------------|
|   | `-t`         |  [Type](#key-type) of key  |
|   | `-b`       | The number of bits in the key |
|   | `-C`       | Provides a new comment |
{.left-text}

Generate an RSA 4096 bit key with email as a comment


### Generate {.col-span-2 .row-span-2}

Generate a key interactively
```shell script
$ ssh-keygen
```

Specify filename
```shell script
$ ssh-keygen -f ~/.ssh/filename
```

Generate public key from private key
```shell script
$ ssh-keygen -y -f private.key > public.pub
```

Change comment
```shell script
$ ssh-keygen -c -f ~/.ssh/id_rsa
```

Change private key passphrase 
```shell script
$ ssh-keygen -p -f ~/.ssh/id_rsa
```


### Key type

- rsa
- ed25519
- dsa
- ecdsa



### known_hosts {.col-span-2}

Search from known_hosts
```shell script
$ ssh-keygen -F <ip/hostname>
```

Remove from known_hosts
```shell script
$ ssh-keygen -R <ip/hostname>
```


### Key format

- PEM 
- PKCS8




See also
--------

- [OpenSSH Config File Examples](https://www.cyberciti.biz/faq/create-ssh-config-file-on-linux-unix/) _(cyberciti.biz)_
- [ssh_config](https://linux.die.net/man/5/ssh_config) _(linux.die.net)_

