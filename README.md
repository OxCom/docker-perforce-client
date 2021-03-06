# docker-perforce-client
CLI [perforce](https://www.perforce.com/) client.

## Docker
```bash
docker pull docker pull oxcom/perforce-client:ubuntu-2019.2.1908095
```

## Custom build
```bash
docker build . --rm -t docker-perforce-client/ubuntu:latest -f ubuntu/Dockerfile
```

## Usage
Helix Core P4 [Command Reference](https://www.perforce.com/manuals/cmdref/Content/CmdRef/Home-cmdref.html)

```bash
docker run -it --rm -e P4HOST="$(hostname)" -e P4CLIENT=workspace -e P4USER=root -e P4PASSWD=root oxcom/perforce-client:ubuntu-2019.2.1908095 /bin/bash

p4 client -S //depot/main ${P4CLIENT}
p4 sync -f
p4 client -d ${P4CLIENT}
```

You can mount volume ```/var/p4/project/``` into the container to work with workspace
```-v /path/to/local/folder:/var/p4/project```

Use a non-interactive editor:
```bash
EDITOR=/bin/true p4 client -S //ce/main ${P4CLIENT}
```
