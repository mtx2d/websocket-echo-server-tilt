```
minikube ip
```

Add entry to  the `/etc/hosts` file:
```
192.168.105.3 api.livechat.local
```

Then use this `wscat` to verify websocket can work:
```
wscat -c 'ws:/api.livechat.local/ws/'
```

NOTE:
1. use `ws` not `wss`
2. use `api.livechat.local` NOT directly ip 192.168.105.3
3. use `/ws/` not `/ws`

