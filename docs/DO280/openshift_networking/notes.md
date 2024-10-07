#### Various way of creating secured routes in OpenShift
    oc create route edge <route-name> --service=<service-name> --hostname=<example.com> --cert=cert.pem --key=cert.key
    oc create route passthrough --service=<service-name> --hostname=<example.com>
    oc create route reencrypt --service=<service-name> --hostname=<example.com> --cert=cert.pem --key=cert.key

#### Network Policies
    oc label namespaces <namespace> key=value

>**Example-1**
> The following network policy allows traffic from all the pods and ports in the network-1 namespace to all pods and ports in the network-2 namespace

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: network-2-policy
spec:
  podSelector: {}
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          name: network-1
```

>**Example-2**
> This example combines the selectors into one rule, thereby only allowing access from pods in the dev namespace with the app=mobile label. This is an example of a logical AND
```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: network-2-policy
spec:
    podSelector: {}
    ingress:
    - from:
        - namespaceSelector:
            matchLabels:
                name: dev
        podSelector:
            matchLabels:
                app: mobile
```
>**Example-3**
> By changing the podSelector field in the previous example to be an item in the from list, all pods in the dev namespace and all pods from any namespace labeled app=mobile can reach the pods that match the top-level podSelector field. This is an example of a logical OR
```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: network-2-policy
spec:
    podSelector: {}
    ingress:
    - from:
        - namespaceSelector:
            matchLabels:
                name: dev
        - podSelector:
            matchLabels:
                app: mobile
```
>**Important**
> If a pod is matched by selectors in one or more network policies, then the pod will only accept connections that are allowed by at least one of those network policies

>**Example**
> Deny All .. No Pod in cluster will be able to communicate with the other pod. Never apply this policy in production. 

```yaml
kind: NetworkPolicy
apiVersion: networking.k8s.io/v1
metadata:
  name: default-deny
spec:
  podSelector: {}
```

If you have Cluster Monitoring or exposed routes, then you need to allow ingress from them as well. The following policies allow ingress from OpenShift monitoring and Ingress Controllers:

```yaml
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-from-openshift-ingress
spec:
  podSelector: {}
  ingress:
  - from:
    - namespaceSelector:
        matchLabels:
          network.openshift.io/policy-group: ingress
---
apiVersion: networking.k8s.io/v1
kind: NetworkPolicy
metadata:
  name: allow-from-openshift-monitoring
spec:
    podSelector: {}
    ingress:
    - from:
      - namespaceSelector:
          matchLabels:
            network.openshift.io/policy-group: monitoring
```