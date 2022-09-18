 RUN chgrp -R 0 directory && \
    chmod -R g=u directory

oc adm policy add-scc-to-user anyuid -z myserviceaccount