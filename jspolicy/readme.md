# jsPolicy

jsPolicy is a policy engine for Kubernetes that allows you to write policies in JavaScript or TypeScript. 
jsPolicy runs policies with Google's V8 JavaScript engine in a pool of pre-heated sandbox environments which makes the execution of a policy amazing fast.

![alt text](https://www.jspolicy.com/docs/media/diagrams/jspolicy-architecture.svg)

## Instalation
```
helm install jspolicy jspolicy -n jspolicy --create-namespace --repo https://charts.loft.sh
```


## Privilege escalation example
In this example, the cluster admin will force the use of unprivileged containers in the cluseter. The OPA Gatekeeper will look for the securitycontext field and check if privileged=true. If it’s the case, then, the request will fail.

1. Define the policy
```
kubectl create -f policy.yaml
kubectl get jspolicy
```

2. Test the contraint using a bad deployment
```
kubectl create -f bad-nginx.yaml
```



## Cleanup

```
helm delete jspolicy
```