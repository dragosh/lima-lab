

# Lima and contai`nerd`

https://github.com/lima-vm/lima#getting-started

## Installation


### Update Homebrew formulae
```sh
brew update
```
### Install QEMU
```sh
brew install simnalamburt/x/qemu-hvf
```

### Check version
```sh
which qemu-system-aarch64
/opt/homebrew/bin/qemu-system-aarch64
```

```sh
qemu-system-aarch64 --version
QEMU emulator version 6.1.0
Copyright (c) 2003-2021 Fabrice Bellard and the QEMU Project developers
```

### Check if its valid
```sh
qemu-system-aarch64 -accel help
Accelerators supported in QEMU binary:
hvf
tcg
```

### Install Lima

```sh
brew install lima
```

### Check version
```sh
which limactl
/opt/homebrew/bin/limactl
```

```sh
limactl --version
limactl version 0.6.4
```


## Instance management

```sh
LIMA_INSTANCE=<instance>
```
```sh
limactl stop <instance>
```
```sh
limactl rm <instance>
```

### Start VM
```sh
limactl start default.yml
```
Expected output
```
? Creating an instance "default"  [Use arrows to move, type to filter]
> Proceed with the default configuration
  Open an editor to override the configuration
  Exit


  ......

  INFO[0111] READY. Run `lima` to open the shell.
```

### Debug
```
lima uname -a
```
```sh
tail -f ~/.lima/default/serial.log
tail -f ~/.lima/default/ha.stderr.log| jq
```

### Other OS guests
https://github.com/lima-vm/lima/tree/master/examples

### Containers

#### Nostalgia only or CI legacy commands
alias docker="lima nerdctl"

```sh
lima nerdctl run -d --name nginx -p 127.0.0.1:8080:80 nginx:alpine
```
```sh
lima nerdctl run -d --name nginx -v ${PWD}/www:/usr/share/nginx/html:ro -p 8080:80 nginx:alpine
```
> Privileged ports (1-1023) cannot be forwarded

```sh
lima nerdctl ps
```

```sh
lima nerdctl rm -f nginx
```


#### amd64 support
```
lima sh -c 'sudo apt update && sudo apt install -y qemu-user-static binfmt-support'
```

### Images


### Registries


### Compose
