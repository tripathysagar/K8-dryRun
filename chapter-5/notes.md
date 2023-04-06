## Chapter 5
```
k run nginx-pod --image=nginx:latest --dry-run=client -o yaml > multi-container-pod.yaml
```
Added the file `multi-container-pod.yaml` with the new container 

```
name: busybox-pod
image: busybox:latest
command: ['sh', '-c', 'while true; do date; sleep 10; done']
```
Remember to add the command for the busybox image,as it is not a server. We have to create an infinite loop.

to check the CLI:
```
k exec -it multi-container-pod --container busybox-pod -- /bin/sh
```


Keywords coresponding docker and K8
|docker|K8 |Meaning|
|------|---|-------|
|ENTRYPOINT|command|The primary cmd that will be used for launching DOcker container|
|CMD|args|prams that passed to the entrypoint as additional args|
---
initContainer: containers that runs before our actual container. It is used for cloning repo, downloading confiqs or <br>
pre-processing before before actualcontainers. Its execution isserial, so adding more than one initContainers will lead to <br>
slower loading time of container running

to check logs of a container : <br>
```
k logs -f nginx-busybox-with-custom-command-and-args  --container nginx-container
```
to print the logs of all the containers : <br>
```
k logs -f nginx-busybox-with-custom-command-and-args
``` 

Adding tag `--since=10s` will print logs of last 10 sec. Similarly adding tag `--tail=10` will show last 10 entries from backward.


---

### Volumes
- storage assigned to pod's life cycle(creation, deletion)
- used for sahring resource between container running inside of a pod(directory)
- most of the case it is not persitant
- `emptyDir` creates an empty directory to be shared between containers. [emptyDir-pod-example]
    - connect to nginx-containers shell using 
    `
    k exec -it two-containers-with-empty-dir -c nginx-container -- /bin/sh
    `
    - goto `/var/i-am-empty-dir-volume`
    - create a file and enter some dummy text `echo 'hello world!!' >> hello_world.txt`
    - As the volume is shared by the busybox-container we can validate the existance of the file using `k exec  two-containers-with-empty-dir -c busybox-container -- cat /var/i-am-empty-dir-volume/hello_world.txt`
- `hostPath` crates persitant volume which leads to security isseue. Should not implement


