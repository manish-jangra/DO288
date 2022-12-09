```
RUN chgrp -R 0 directory && \
    chmod -R g=u directory
```
```
oc adm policy add-scc-to-user anyuid -z myserviceaccount
```
👇 This Command allows to use image streams from one namespace to another space and it grants access to service accounts in another namespace
```
oc policy add-role-to-group -n $U-common \
        system:image-puller system:serviceaccounts:$U-expose-image
```
