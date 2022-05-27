### Authentication and Authorization

    oc auth can-i verb resource

#### Creating an HTPasswd  File

- Create the htpasswd file
    
    htpasswd -c -B -b /tmp/htpasswd student redhat123
