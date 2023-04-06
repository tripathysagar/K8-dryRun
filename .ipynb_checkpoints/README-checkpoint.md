This is a repo for running K8 using minikube. By following the [kubernates bible](https://www.packtpub.com/product/the-kubernetes-bible/9781838827694)
## Chapter 6
```
k run nginx-pod --image=nginx:latest --dry-run=client -o yaml > multi-container-pod.yaml
```
Added the file `multi-container-pod.yaml` with the new container 

```name: busybox-pod
   image: busybox:latest
   command: ['sh', '-c', 'while true; do date; sleep 10; done']
```.
Remwmber to add the command for the busybox image,as it is not a server. We have to create an infinite loop.

to check the CLI:
```
k exec -it multi-container-pod --container busybox-pod -- /bin/sh
```

Keywords coresponding docker and K8
|docker|K8 |Meaning|
|------|---|-------|
|ENTRYPOINT|command|The primary cmd that will be used for launching DOcker container|
|CMD|args|prams that passed to the entrypoint as additional args|


