# SSH

SSH or Secure Shell is a cryptographic network protocol for operating network services securely over an unsecured network.[1] Typical applications include remote command-line, login, and remote command execution, but any network service can be secured with SSH.

Previously was Telnet,but it was insecure.


### Install server

`apt-get imstall openssh-server`

`enable ssh`

### Connecting to server

`ssh user@server1.com`

At the moment we connect the server, a fingerprint from the remote server was added to our trusted sites.
This fingerprint will be stored in ~/.ssh/known_hosts
Fingerprint prevent the "man in the middle" hack

### Generating certificate

`ssh-keygen`

this will generate:

```
.ssh/id_rsa 
.ssh/id_rsa.pub
```

then we need to add the public key (id_rsa.pub) to the .ssh/authorized_keys in the remote server.

To make this more quickly, we have the ssh-copy-id command:

`ssh-copy-id -i ~/.ssh/mykey user@host`

To make asking for the public cert:

`ssh-copy-id user@host:`

### Execute command in the remote server

`ssh -t root@server1.com irssi`

### Proxy

`ssh -D 9999 root@server1.com`

Use localhost:9999 as proxy socks from the OS

### Execute apps with UI in the remote server

`ssh -X root@server1.com` then we run the app, like `firefox`

### To connect to remote servers behind a firewall

`ssh -L 2020:server2:22 root@server1`

then we can do:

`ssh -p 2020 root@localhost` to enter to the server2 through server1
