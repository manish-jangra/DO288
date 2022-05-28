### Secrets and Configmaps
#### Create a generic secret containing key-value pairs from literal values
    oc create secret generic secret_name --from-literal key1=secret1 --from-literal key2=secret2

#### Create a generic secret using key names specified on the command line and values from files
    oc create secret generic secret_name \
        --from-file id_rsa=/path-to/id_rsa \
        --from-file id_rsa.pub=/path-to/id_rsa.pub

#### Create a TLS secret specifying a certificate and the associated key
    oc create secret tls secret-tls \
        --cert /path-to-certificate --key /path-to-key

#### Exposing Secrets to Pods
    oc create secret generic demo-secret \
        --from-literal user=demo-user \
        --from-literal root_password=zT1KTgk
```yaml
    env:
    - name: MYSQL_ROOT_PASSWORD
      valueFrom:
        secretKeyRef:
          name: demo-secret 
          key: root_password
```
>**Important**
> You can also use the oc set env command to set application environment variables from either secrets or configuration maps. In some cases, the names of the keys can be modified to match the names of environment variables by using the --prefix option. In the following example, the user key sets the MYSQL_USER environment variable, and the root_password key sets the MYSQL_ROOT_PASSWORD environment variable. If the key name is lowercase, then the corresponding environment variable is converted to uppercase

### Security Context Constraints (SCC)
