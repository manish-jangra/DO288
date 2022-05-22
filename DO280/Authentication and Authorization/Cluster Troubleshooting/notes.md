### Troubleshooting Cluster

    oc get nodes
    oc adm top nodes
    oc describe node <node-name>
    oc get clusterversion
    oc describe clusterversion
    oc get clusteroperators

#### Display Logs for OpenShift Nodes

    oc adm node-logs -u crio my-node-name
    oc adm node-logs -u kubelet my-node-name
    oc adm node-logs my-node-name