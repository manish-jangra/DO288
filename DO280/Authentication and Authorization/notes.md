### Authentication and Authorization
    oc auth can-i verb resource

#### Creating an HTPasswd  File
    htpasswd -c -B -b /tmp/htpasswd student redhat123

>**Important**
> Use the -c option only when creating a new file. The -c option replaces all file content if the file already exists.

#### Add or update credentials
    htpasswd -b /tmp/htpasswd student redhat1234
    
#### Delete credentials
    htpasswd -D /tmp/htpasswd student