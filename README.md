
## Preparation

When setting up `minikube`, use the following command, for M1 Mac:
```
minikube start --driver qemu --network socket_vmnet
```

```
minikube addon enable ingress
```

The `--driver qemu` allows the cluster IP to be reachable.
Otherwise `$(minikube ip)` is not a separte ip from the host machine(M1 laptop).

Refernece:
1. https://github.com/kubernetes/minikube/issues/7332

### Software Versions
```
➜  ~ tilt version
v0.33.18, built 2024-08-01
```

```
➜  ~ minikube version
minikube version: v1.33.1
commit: 5883c09216182566a63dff4c326a6fc9ed2982ff
```

```
➜  ~ docker version
Client:
 Version:           27.0.3
 API version:       1.46
 Go version:        go1.21.11
 Git commit:        7d4bcd8
 Built:             Fri Jun 28 23:59:41 2024
 OS/Arch:           darwin/arm64
 Context:           desktop-linux

Server: Docker Desktop 4.32.0 (157355)
 Engine:
  Version:          27.0.3
  API version:      1.46 (minimum version 1.24)
  Go version:       go1.21.11
  Git commit:       662f78c
  Built:            Sat Jun 29 00:02:44 2024
  OS/Arch:          linux/arm64
  Experimental:     false
 containerd:
  Version:          1.7.18
  GitCommit:        ae71819c4f5e67bb4d5ae76a6b735f29cc25774e
 runc:
  Version:          1.7.18
  GitCommit:        v1.1.13-0-g58aa920
 docker-init:
  Version:          0.19.0
  GitCommit:        de40ad0
```

```
➜  ~ kubectl config get-contexts
CURRENT   NAME             CLUSTER          AUTHINFO         NAMESPACE
          docker-desktop   docker-desktop   docker-desktop
*         minikube         minikube         minikube         default
```

## Add IP to /etc/hosts
```
minikube ip
```

Add entry to  the `/etc/hosts` file:
```
192.168.105.3 api.livechat.local
```

I am not sure why this step is needed. If I do not do this, the ws command directly using ip address will fail to connect.
For example this command would fail:
```
wscat -c 'ws://192.168.105.3/ws/'
```

## Validate that socket connects

Then use this `wscat` to verify websocket can work:
```
wscat -c 'ws:/api.livechat.local/ws/'
```

NOTE:
1. use `ws` not `wss`
2. use `api.livechat.local` NOT directly ip 192.168.105.3
3. use `/ws/` not `/ws`
4. the connection takes about 5s on my machine to establish.


https://github.com/user-attachments/assets/025acf6d-efe6-4e89-810a-72678f4be752

## Tilt
```
tilt up
```

### Tiltfile Logs
<img width="2672" alt="image" src="https://github.com/user-attachments/assets/d5fc3a9e-bbfa-4d51-85f2-f271416a14ba">

### Echo Server Logs
<img width="2672" alt="image" src="https://github.com/user-attachments/assets/c80d780a-460a-48cf-8f14-0838578d14e3">

### Ingress Logs
<img width="2672" alt="image" src="https://github.com/user-attachments/assets/e9b136f6-b02d-4db3-b6d9-447d716306fa">
