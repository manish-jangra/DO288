skopeo inspect --creds developer1:MyS3cret! \ 
    docker://registry.redhat.io/rhscl/postgresql-96-rhel7

skopeo copy --dest-tls-verify=false \
    oci:/home/user/myimage \ 
    docker://registry.example.com/myorg/myimage

skopeo copy --src-creds=testuser:testpassword \ 
    --dest-creds=testuser1:testpassword \ 
    docker://srcregistry.domain.com/org1/private \ 
    docker://dstegistry.domain2.com/org2/private

Change Tag
skopeo copy docker://registry.example.com/myorg/myimage:1.0 \ 
    docker://registry.example.com/myorg/myimage:latest

oc create secret docker-registry registrycreds \ 
    --docker-server registry.example.com \
    --docker-username youruser \
    --docker-password yourpassword

oc create secret generic registrycreds \
    --from-file .dockerconfigjson=${XDG_RUNTIME_DIR}/containers/auth.json \ 
    --type kubernetes.io/dockerconfigjson

oc secrets link default registrycreds --for pull

oc secrets link builder registrycreds

Make the OpenShift Internal Registry Accessible from Outside
oc patch config.imageregistry cluster -n openshift-image-registry \ 
    --type merge -p '{"spec":{"defaultRoute":true}}'

oc get route -n openshift-image-registry

oc policy add-role-to-user system:image-puller \ 
    user_name -n project_name