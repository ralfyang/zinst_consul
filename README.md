# Hashcorp Consul package made by zinst 
* You can install the consul Server & Client with Bootstrap by zinst

## Consul cluster setup in Bootstrap server
### Add a public key for key-deploy
```
cat ~/.ssh/id_rsa.pub > /root/authorized_keys
```

### Key-deploy to the other servers & clients (root password requires)
* Hostlist:
 * Bootstrap  192.168.133.20
 * Server: 192.168.133.2[1-2]
 * Client: 192.168.133.3[1-2]
```
zinst keydep   -h 192.168.133.2[1-2] 192.168.133.3[1-2] -pass
```

### Setting up the other servers & clients
```
zinst  set consul.encrypt="`cat /data/var/consul_key`" -set consul.start_join="192.168.133.20,192.168.133.21,192.168.133.22"  -h 192.168.133.2[1-2] 192.168.133.3[1-2]
```

### Consul restart
```
zinst  restart consuld  -h 192.168.133.21 192.168.133.3[1-2]
```

### Cluster monitoring
```
consul members
```
