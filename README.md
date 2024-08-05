
## Preparation

When setting up `minikube`, use the following command, for M1 Mac:
```
minikube start --driver qemu --network socket_vmnet
```

The `--driver qemu` allows the cluster IP to be reachable.
Otherwise `$(minikube ip)` is not a separte ip from the host machine(M1 laptop).

Refernece:
1. https://github.com/kubernetes/minikube/issues/7332


## Add IP to /etc/hosts

I am not sure why this is needed. 

```
minikube ip
```

Add entry to  the `/etc/hosts` file:
```
192.168.105.3 api.livechat.local
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


