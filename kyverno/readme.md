# Kyverno
A Kyverno policy is a collection of rules. Each rule consists of a match declaration, an optional exclude declaration, and one of a validate, mutate, generate, or verifyImages declaration. Each rule can contain only a single validate, mutate, generate, or verifyImages child declaration.

![alt text](https://kyverno.io/images/Kyverno-Policy-Structure.png)

## Instalation
```
kubectl create -f https://raw.githubusercontent.com/kyverno/kyverno/main/config/install.yaml
```


## Privilege escalation example
In this example, the cluster admin will force the use of unprivileged containers in the cluseter. The OPA Gatekeeper will look for the securitycontext field and check if privileged=true. If it’s the case, then, the request will fail.


2. Define the constraint based on the template
```
kubectl create -f constraint.yaml


kubectl get constraint
kubectl get constrainttemplate

```

3. Test the contraint using a bad deployment
```
kubectl create -f bad-nginx.yaml
```



## Cleanup

```
kubectl delete -f https://raw.githubusercontent.com/kyverno/kyverno/main/config/install.yaml
```

