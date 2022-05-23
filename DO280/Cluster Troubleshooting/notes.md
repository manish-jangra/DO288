### Cluster Troubleshooting

#### Get Cluster Details

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

#### Opening Shell Prompt on OpenShift Nodes

    oc debug node/my-node-name
    chroot /host
    systemctl is-active kubelet
    crictl ps                   # This helps to get low level containers running on Cluster Nodes
    systemctl status kubelet
    systemctl status crio
    crictl ps --name openvswitch    #crictl is more like docker and podman command, this checks for openvmswitch pod

#### Troubleshooting running and terminated pods

    oc logs pod-name
    oc logs -f pod-name
    oc logs pod-name -c container-name
    oc logs pod-name --all-containers
    oc get events -n namespace-name

#### Creating Troubleshooting Pods

    oc debug deployment/deployment-name --as-root

#### Changing a running container

    oc rsh my-pod-name      # Logs in the pod/container shell
    oc rsh my-pod-name -c container-name        # in case of multiple containers in single pod
    oc cp /local/path my-pod-name:/container/path
    oc rsync

#### Miscellaneous Commands
>**Note**
> The --loglevel level option displays OpenShift API requests, starting with level 6. As you increase the level, up to 10, more information about those requests is added. Level 10 also includes a curl command to replicate each request.
    
    oc get pod --loglevel 6
    oc get pod --loglevel 10
    oc whoami -t
