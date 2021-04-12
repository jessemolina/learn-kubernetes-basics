# Lab 01

1. Create a new Pod named `nginx` running the image `nginx:1.17.10`. Expose container to port `80`. 

Imperative approach. 

```code
# group imperatives by namespace
$ kubectl create namespace lab01

# run pod in namespace
$ kubectl run nginx --image=nginx:1.17.10 --port=80 --namespace=lab01
```

Declerative approach.

Write `YAML` file for nampespace. 

```code
apiVersion: v1
kind: Namespace
metadata:
  name: lab01
```

Write `YAML` file for pod.

```code
apiVersion: v1
kind: Pod
metadata:
  name: nginx
spec:
  containers:
  - name: nginx
    image: nginx:1.17.10
    ports:
    - containerPort: 80
```

Create imperative objects from `YAML` files.  

```code
# group imperatives by namespace
$ k create -f namespace-lab01.yaml

# run pod in namespace
$ k create -f pod-nginx.yaml -n lab01
```

2. Get the details of the Pod, including its IP address.

```code
# specify namespace and container name
$ k get pod nginx -n lab01 -o wide

# grep results
$ k describe pod nginx -n labl01 | grep IP
```

3. Create a temporary Pod that uses the busybox image to execute a `wget` command inside of the container. The `wget` command should access the endpoint exposed by the `nginx` container.

```code
$ kubectl run busybox --image=busybox --restart=Never --rm -it -n ckad -- wget -O- 10.1.0.66:80
```

4. Get the logs of the `nginx` container.

```code
$ kubectl logs nginx -n lab01
```

5. Add the environment variables `DB_URL=postgressql://mydb:5432` and `DB_USERNAME=admin` to the container of the `nginx` Pod. 


```code
# view current pod config, save copy, and append environment variables
$ k edit pod nginx -n lab01

# delete existing pod
$ k delete pod nginx -n lab01

# create new pod
$ k create -f pod-nginx-edit.yaml
```

6. Open a shell for the `nginx` container and inspect the contents of the currently directory `ls -l`.

```code
$ k exec -it nginx -n lab01 -- /bin/sh
```

7. Create a YAML manifest for a Pod named `loop` that runs the `busybox` image in a container. The container should run the following command: `for i in (1...10); do echo "Welcome $i times"; done`. Create the pod from the YAML manifest. What's the status of the Pod?

```code
# create loop pod
$ k run loop --image=busybox -o yaml --dry-run=client --restart=Never -- /bin/sh -c 'for i in 1 2 3 4 5 6 7 8 9 10; \
do echo "Welcome $i times"; done' > pod-busybox-loop.yaml

# 
$ k create -f pod-busybox-loop.yaml -n lab01

$ k get pod loop -n lab01
```

8. Edit the Pod named `loop`. Change the command to run in an endless loop. Each iteration should `echo` the current date. 

```code
# save copy and edit
$ k edit pod loop -n lab01

$ k delete pod loop -n lab01

$ k create -f pod-loop.yaml -n lab01

$ k describe pod look -n lab01 | grep -C 10 Events
```

9. Inspect the events and the status of the Pod `loop`.

```code
$ k describe pod look -n lab01 | grep -C 10 Events
```

10. Delete the namespace `ckad` and its Pods. 

```code
$ k delete ns lab01
```
# Notes

```code
# reference - get all
$ k get all -A

# get events
$ k get events -n lab01
```
