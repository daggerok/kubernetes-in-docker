# kubernetes-in-docker-for-mac
Getting started with k8s on Docker for Mac / Windows

## enable kubernetes in Docker for Mac / Windows
![Enable k8s](./01-enable-k8s.png)

## install kubectl auto-completeon (zsh)
I'm using zsh, so all I need to do is add kubectl to plugins section

![Enable kubectl auto-completion](./02-auto-completion.png)

## testing kubernetes setup
So now we are ready to go with k8s!

Let's run nginx:
```bash
➜  ~ kubectl run --image nginx:alpine web
deployment.apps "web" created
```

Check available deployments:
```bash
➜  ~ kubectl get deployments
NAME      DESIRED   CURRENT   UP-TO-DATE   AVAILABLE   AGE
web       1         1         1            1           2m
```

Replication set:
```bash
➜  ~ kubectl get replicaset
NAME           DESIRED   CURRENT   READY     AGE
web-bbcdd5f4   1         1         1         4m
```

And finally get pods where created:
```bash
➜  ~ kubectl get pod
NAME                 READY     STATUS    RESTARTS   AGE
web-bbcdd5f4-zqq5x   1/1       Running   0          5m
```

## deep dive
Let's get more information about our nginx web deployment

```bash
➜  ~ kubectl describe deployment web
Name:                   web
Namespace:              default
CreationTimestamp:      Sun, 04 Nov 2018 15:14:38 +0200
Labels:                 run=web
Annotations:            deployment.kubernetes.io/revision=1
Selector:               run=web
Replicas:               1 desired | 1 updated | 1 total | 1 available | 0 unavailable
StrategyType:           RollingUpdate
MinReadySeconds:        0
RollingUpdateStrategy:  1 max unavailable, 1 max surge
Pod Template:
  Labels:  run=web
  Containers:
   web:
    Image:        nginx:alpine
    Port:         <none>
    Host Port:    <none>
    Environment:  <none>
    Mounts:       <none>
  Volumes:        <none>
Conditions:
  Type           Status  Reason
  ----           ------  ------
  Available      True    MinimumReplicasAvailable
  Progressing    True    NewReplicaSetAvailable
OldReplicaSets:  <none>
NewReplicaSet:   web-bbcdd5f4 (1/1 replicas created)
Events:
  Type    Reason             Age   From                   Message
  ----    ------             ----  ----                   -------
  Normal  ScalingReplicaSet  7m    deployment-controller  Scaled up replica set web-bbcdd5f4 to 1
```
