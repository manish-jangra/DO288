#### Various way of creating secured routes in OpenShift
    oc create route edge <route-name> --service=<service-name> --hostname=<example.com> --cert=cert.pem --key=cert.key
    oc create route passthrough --service=<service-name> --hostname=<example.com>
    oc create route reencrypt --service=<service-name> --hostname=<example.com> --cert=cert.pem --key=cert.key

#### Network Policies
    oc label namespaces <namespace> key=value

>**Example**
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