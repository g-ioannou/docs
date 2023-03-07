## Creating new user

```bash
sudo adduser [server_user] --disabled-password --gecos ""
```

## Configuring ssh for new user

### Server
 ```bash
[server_user]@[server]: $ mkdir .ssh && cd .ssh
```

#### Set up public key for the new user
```bash
[server_user]@[server]:~/.ssh $ ssh-keygen
```

Public key is located in: `id_rsa.pub`
> You can use the public key for a remote git repo by adding the contents of `id_rsa.pub` to the repo's authorized keys.

Copy the public key to `authorized_keys`
```bash
[server_user]@[server]: touch authorized_keys
```


Copy your `public key` to `authorized_keys`
###### Make sure `PubkeyAuthentication` is enabled in `/etc/ssh/sshd_config`
Client

### Client
Add the following to your `config.ssh`
```
Host [host_name] # this is just an alias 
User [server_user]
Hostname [server_ip]
```

#### Connecting
```bash
[client_user]@[client]: $ ssh [host_name]
```
Or connect as a specific server user
```
[client_user]@[client]: $ ssh [server_user]@[host_name | server_ip]
```