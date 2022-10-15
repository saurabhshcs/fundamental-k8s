# fundamental-k8s
This is a very simple fundamental about Kubernetes learning for revision

### Information 
When you install `docker` desktop version on your Mac or Windows maching then you will get `Kubernetes` by default.

```shell
kubectl version
```

```shell
Client Version: version.Info{Major:"1", Minor:"22", GitVersion:"v1.22.3", GitCommit:"c92036820499fedefec0f847e2054d824aea6cd1", GitTreeState:"clean", BuildDate:"2021-10-27T18:41:28Z", GoVersion:"go1.16.9", Compiler:"gc", Platform:"linux/amd64"}
Server Version: version.Info{Major:"1", Minor:"23", GitVersion:"v1.23.12+IKS", GitCommit:"53eb562c6d6b891973e77f4f96ab3569b3630596", GitTreeState:"clean", BuildDate:"2022-09-21T20:06:42Z", GoVersion:"go1.17.13", Compiler:"gc", Platform:"linux/amd64"}
```


```shell
kubectl config get-clusters
```
#### OUTPUT
```shell
NAME
labs-prod-kubernetes-sandbox/c8ana0sw0ljj8gkugn50
```

```shell
kubectl config get-contexts
```

```shell
CURRENT   NAME                  CLUSTER                                             AUTHINFO      NAMESPACE
*         saurabhshcs-context   labs-prod-kubernetes-sandbox/c8ana0sw0ljj8gkugn50   saurabhshcs   sn-labs-saurabhshcs
```


```shell
kubectl get pods
```

```shell
No resources found in sn-labs-saurabhshcs namespace.
```

```shell
export MY_NAMESPACE=sn-labs-$USERNAME
```

```shell
docker build -t <CONTAINER-REGISTERY_URI>/$MY_NAMESPACE/hello-world:1 . && docker push <CONTAINER-REGISTERY_URI>/$MY_NAMESPACE/hello-world:1
```

```
kubectl run hello-world --image <CONTAINER-REGISTERY_URI>/$MY_NAMESPACE/hello-world:1 --overrides='{"spec":{"template":{"spec":{"imagePullSecrets":[{"name":"CONTAIN-REGISTRY_NAME"}]}}}}'
```

```shell
Sending build context to Docker daemon  6.656kB
Step 1/6 : FROM node:9.4.0-alpine
9.4.0-alpine: Pulling from library/node
605ce1bd3f31: Pull complete 
fe58b30348fe: Pull complete 
46ef8987ccbd: Pull complete 
Digest: sha256:9cd67a00ed111285460a83847720132204185e9321ec35dacec0d8b9bf674adf
Status: Downloaded newer image for node:9.4.0-alpine
 ---> b5f94997f35f
Step 2/6 : COPY app.js .
 ---> 69f50089fb69
Step 3/6 : COPY package.json .
 ---> 653e2911e1db
Step 4/6 : RUN npm install &&    apk update &&    apk upgrade
 ---> Running in d3eceb23f35e
npm notice created a lockfile as package-lock.json. You should commit this file.
npm WARN hello-world-demo@0.0.1 No repository field.
npm WARN hello-world-demo@0.0.1 No license field.

added 57 packages in 2.064s
fetch http://dl-cdn.alpinelinux.org/alpine/v3.6/main/x86_64/APKINDEX.tar.gz
fetch http://dl-cdn.alpinelinux.org/alpine/v3.6/community/x86_64/APKINDEX.tar.gz
v3.6.5-44-gda55e27396 [http://dl-cdn.alpinelinux.org/alpine/v3.6/main]
v3.6.5-34-gf0ba0b43d5 [http://dl-cdn.alpinelinux.org/alpine/v3.6/community]
OK: 8448 distinct packages available
Upgrading critical system libraries and apk-tools:
(1/1) Upgrading apk-tools (2.7.5-r0 -> 2.7.6-r0)
Executing busybox-1.26.2-r9.trigger
Continuing the upgrade transaction with new apk-tools:
(1/7) Upgrading musl (1.1.16-r14 -> 1.1.16-r15)
(2/7) Upgrading busybox (1.26.2-r9 -> 1.26.2-r11)
Executing busybox-1.26.2-r11.post-upgrade
(3/7) Upgrading libressl2.5-libcrypto (2.5.5-r0 -> 2.5.5-r2)
(4/7) Upgrading libressl2.5-libssl (2.5.5-r0 -> 2.5.5-r2)
(5/7) Installing libressl2.5-libtls (2.5.5-r2)
(6/7) Installing ssl_client (1.26.2-r11)
(7/7) Upgrading musl-utils (1.1.16-r14 -> 1.1.16-r15)
Executing busybox-1.26.2-r11.trigger
OK: 5 MiB in 15 packages
Removing intermediate container d3eceb23f35e
 ---> 106a960f8a35
Step 5/6 : EXPOSE  8080
 ---> Running in f027f685ad9f
Removing intermediate container f027f685ad9f
 ---> a523d23f6cc2
Step 6/6 : CMD node app.js
 ---> Running in 3806be222159
Removing intermediate container 3806be222159
 ---> f339163a42cb
Successfully built f339163a42cb
Successfully tagged <CONTAINWE-REGISTRY-URI>/sn-labs-saurabhshcs/hello-world:1
The push refers to repository [<CONTAINWE-REGISTRY-URI>/sn-labs-saurabhshcs/hello-world]
70abbe6f81d7: Pushed 
2574b1666f23: Pushed 
82b8bdad4d9e: Pushed 
0804854a4553: Layer already exists 
6bd4a62f5178: Layer already exists 
9dfa40a0da3b: Layer already exists 
1: digest: sha256:74d874e14652008977b44cea80169a609dbbe85d33df769ac3145bd38c86a9dc size: 1576
```


```shell
kubectl get pods
```
```shell
NAME          READY   STATUS    RESTARTS   AGE
hello-world   1/1     Running   0          6s
```

```shell
kubectl get pods -o wide
```

```shell
NAME          READY   STATUS    RESTARTS   AGE     IP               NODE          NOMINATED NODE   READINESS GATES
hello-world   1/1     Running   0          4m54s   172.17.180.113   10.241.0.58   <none>           <none>
```


```shell
kubectl describe pod hello-world
```

```shell
Name:                 hello-world
Namespace:            sn-labs-saurabhshcs
Priority:             1
Priority Class Name:  normal
Node:                 10.241.0.58/10.241.0.58
Start Time:           Sat, 15 Oct 2022 18:20:44 -0400
Labels:               run=hello-world
Annotations:          cni.projectcalico.org/containerID: 0e5815b5c50f6ee32c1c598d60eb48a828ade1ebcb781ea286441687f5d76f96
                      cni.projectcalico.org/podIP: 172.17.180.113/32
                      cni.projectcalico.org/podIPs: 172.17.180.113/32
                      kubernetes.io/limit-ranger:
                        LimitRanger plugin set: cpu, ephemeral-storage, memory request for container hello-world; cpu, ephemeral-storage, memory limit for contain...
                      kubernetes.io/psp: ibm-privileged-psp
Status:               Running
IP:                   172.17.180.113
IPs:
  IP:  172.17.180.113
Containers:
  hello-world:
    Container ID:   containerd://09a1463ed531ffa7822f9150f4e580eb238ce2bb6bba9ecdef24e0c97daf4b03
    Image:          <CONTAINWE-REGISTRY-URI>/sn-labs-saurabhshcs/hello-world:1
    Image ID:       <CONTAINWE-REGISTRY-URI>/sn-labs-saurabhshcs/hello-world@sha256:74d874e14652008977b44cea80169a609dbbe85d33df769ac3145bd38c86a9dc
    Port:           <none>
    Host Port:      <none>
    State:          Running
      Started:      Sat, 15 Oct 2022 18:20:48 -0400
    Ready:          True
    Restart Count:  0
    Limits:
      cpu:                500m
      ephemeral-storage:  5Gi
      memory:             512Mi
    Requests:
      cpu:                200m
      ephemeral-storage:  512Mi
      memory:             128Mi
    Environment:          <none>
    Mounts:
      /var/run/secrets/kubernetes.io/serviceaccount from kube-api-access-8wgcz (ro)
Conditions:
  Type              Status
  Initialized       True 
  Ready             True 
  ContainersReady   True 
  PodScheduled      True 
Volumes:
  kube-api-access-8wgcz:
    Type:                    Projected (a volume that contains injected data from multiple sources)
    TokenExpirationSeconds:  3607
    ConfigMapName:           kube-root-ca.crt
    ConfigMapOptional:       <nil>
    DownwardAPI:             true
QoS Class:                   Burstable
Node-Selectors:              <none>
Tolerations:                 node.kubernetes.io/not-ready:NoExecute op=Exists for 600s
                             node.kubernetes.io/unreachable:NoExecute op=Exists for 600s
Events:
  Type    Reason     Age    From               Message
  ----    ------     ----   ----               -------
  Normal  Scheduled  5m45s  default-scheduler  Successfully assigned sn-labs-saurabhshcs/hello-world to 10.241.0.58
  Normal  Pulling    5m44s  kubelet            Pulling image "<CONTAINWE-REGISTRY-URI>/sn-labs-saurabhshcs/hello-world:1"
  Normal  Pulled     5m42s  kubelet            Successfully pulled image "<CONTAINWE-REGISTRY-URI>/sn-labs-saurabhshcs/hello-world:1" in 2.423348363s
  Normal  Created    5m41s  kubelet            Created container hello-world
  Normal  Started    5m41s  kubelet            Started container hello-world
```


```shell
kubectl delete pod hello-world
```

```shell
pod "hello-world" deleted
```














