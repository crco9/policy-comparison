# OPA Gatekeeper

Gatekeeper is a validating (mutating TBA) webhook that enforces CRD-based policies executed by Open Policy Agent, a policy engine for Cloud Native environments hosted by CNCF as a graduated project.

In addition to the admission scenario, Gatekeeper's audit functionality allows administrators to see what resources are currently violating any given policy.

Finally, Gatekeeper's engine is designed to be portable, allowing administrators to detect and reject non-compliant commits to an infrastructure-as-code system's source-of-truth, further strengthening compliance efforts and preventing bad state from slowing down the organization.

![alt text](https://d33wubrfki0l68.cloudfront.net/ded3b4e7727ada756100da67cfe1cc8251984947/d042a/images/blog/2019-08-06-opa-gatekeeper/v3.png)

## Instalation
```
kubectl install -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/master/deploy/gatekeeper.yaml
```

## Privilege escalation example
In this example, the cluster admin will force the use of unprivileged containers in the cluseter. The OPA Gatekeeper will look for the securitycontext field and check if privileged=true. If it’s the case, then, the request will fail.

1. Define the template including rego
```
kubectl create -f constrainttemplate.yaml
```

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
kubectl delete -f https://raw.githubusercontent.com/open-policy-agent/gatekeeper/master/deploy/gatekeeper.yaml

kubectl delete crd \
  configs.config.gatekeeper.sh \
  constraintpodstatuses.status.gatekeeper.sh \
  constrainttemplatepodstatuses.status.gatekeeper.sh \
  constrainttemplates.templates.gatekeeper.sh
```


## Notes:

Quite easy to install, very complex rules, but you need to learn howto write rego
vscode extension https://marketplace.visualstudio.com/items?itemName=tsandall.opa
