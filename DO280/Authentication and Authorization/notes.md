#### Authentication and Authorization
    oc auth can-i verb resource

#### Creating an HTPasswd  File
    htpasswd -c -B -b /tmp/htpasswd student redhat123
>**Important**
> Use the -c option only when creating a new file. The -c option replaces all file content if the file already exists.

#### Add or update credentials
    htpasswd -b /tmp/htpasswd student redhat1234

#### Delete credentials
    htpasswd -D /tmp/htpasswd student

#### Creating the HTPasswd Secret
    oc create secret generic htpasswd-secret \
    --from-file htpasswd=/tmp/htpasswd -n openshift-config

#### Updating the OAuth Custom Resource
    oc get oauth cluster -o yaml > oauth.yaml
    
# YAML
    apiVersion: config.openshift.io/v1
    kind: OAuth
    metadata:
      name: cluster
    spec:
      identityProviders:
      - name: my_htpasswd_provider
        mappingMethod: claim
        type: HTPasswd
        htpasswd:
          fileData:
            name: htpasswd-secret

#### Extracting Secret Data
    oc extract secret/htpasswd-secret -n openshift-config \
    --to /tmp/ --confirm /tmp/htpasswd

#### Updating the HTPasswd Secret
    oc set data secret/htpasswd-secret \
    --from-file htpasswd=/tmp/htpasswd -n openshift-config

#### Deleting Users and Identities
    oc extract secret/htpasswd-secret -n openshift-config \
    --to /tmp/ --confirm /tmp/htpasswd

    htpasswd -D /tmp/htpasswd manager

    oc set data secret/htpasswd-secret \
    --from-file htpasswd=/tmp/htpasswd -n openshift-config

    oc delete user manager

    oc get identities | grep manager

    oc delete identity my_htpasswd_provider:manager

#### Assigning Administrative Privileges
    oc adm policy add-cluster-role-to-user cluster-admin student