This is a repo for running K8 using minikube. By following the [kubernates bible](https://www.packtpub.com/product/the-kubernetes-bible/9781838827694)
## Chapter 6
```
k run nginx-pod --image=nginx:latest --dry-run=client -o yaml > multi-container-pod.yaml
```
updating the file [multi-container-pod.yaml](https://github.com/tripathysagar/K8-dryRun/blob/main/multi-container-pod.yaml) with the busybox image