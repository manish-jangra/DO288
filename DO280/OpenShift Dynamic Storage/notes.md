#### Get Storage Class

    oc get storageclass

#### Request Persistent Volume Claim and Attach to the deployment

    oc set volumes deployment/example-application \
    --add --name example-storage --type pvc --claim-class nfs-storage \
    --claim-mode rwo --claim-size 15Gi --mount-path /var/lib/example-app \
    --claim-name example-storage

| Access Mode       | CLI Abbreviation  |
| ------------------| ------------------|
| ReadWriteMany     | RWX               |
| ReadWriteOnce     | RWO               |
| ReadOnlyMany      | ROX               |

#### Delete PVC

    oc delete pvc/example-pvc-storage

#### Trick to get k8s resource properties using custom-column

    oc get pv -o custom-columns=NAME:.metadata.name,CLAIM:.spec.claimRef.name
    image.png