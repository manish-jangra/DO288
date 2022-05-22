#### Troubleshooting Cluster

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

### Opening Shell Prompt on OpenShift Nodes

    oc debug node/my-node-name
    chroot /host
    systemctl is-active kubelet
    crictl ps                   # This helps to get low level containers running on Cluster Nodes