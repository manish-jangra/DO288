## Helm Charts

### Create hem chart

    helm create openshift

👇 That's how Helm Charts directories are structred.
```
openshift
├── Chart.yaml
├── charts
├── templates
│   ├── NOTES.txt
│   ├── _helpers.tpl
│   ├── deployment.yaml
│   ├── hpa.yaml
│   ├── ingress.yaml
│   ├── service.yaml
│   ├── serviceaccount.yaml
│   └── tests
│       └── test-connection.yaml
└── values.yaml
```

👉 Dependencies are added to **Charts.yaml**

```YAML
dependencies:
  - name: dependency1
    version: 1.2.3
    repository: https://examplerepo.com/charts
  - name: dependency2
    version: 3.2.1
    repository: https://helmrepo.example.com/charts
```
Run the following command after adding dependencies to **Charts.yaml**

    helm dependency update

👉 Variable values are added to **values.yaml**

```YAML
image:
  repository: container.repo/name
  pullPolicy: IfNotPresent
  tag: "2.1"

env:
- name: "QUOTES_HOSTNAME"
  value: "famousapp-mariadb" 
- name: "QUOTES_DATABASE"
  value: "quotesdb"
- name: "QUOTES_USER"
  value: "quotes"
- name: "QUOTES_PASSWORD"
  value: "quotespwd"
```
>**Attention**
Environment Variable names as well as their values should be enclosed in quotes.

👉 How to inject environment variable values stored in **values.yaml**

```YAML
imagePullPolicy: {{ .Values.image.pullPolicy }}
env:
  {{- range .Values.env }}
- name: "{{ .name }}"
  value: "{{ .value }}"
  {{- end }}
```
>**Attention**
{{ .name }} && {{ .value }} shoudl be enclosed in quotes.

Extract Application deployment files from Helm Charts (combined eg deployment, service, route, statefulsets etc) usng the following comamnd 

    helm template app-name helm-directory > base/deployment.yaml

👉 app-name --> Helm Application Name && helm-directory --> directory where helm chart related files are available

## Kustomize

👉 That's how Kustomize application looks like

```
openshift-kustomize
├── base
│   ├── deployment.yaml
│   └── kustomization.yaml
└── overlay
    ├── development
    │   ├── kustomization.yaml
    │   └── patch.yaml
    ├── production
    │   ├── kustomization.yaml
    │   └── patch.yaml
    └── staging
        ├── kustomization.yaml
        └── patch.yaml
```

base/kustomization.yaml
```yaml
resources:
- deployment.yaml
```

overlay/production/kustomization.yaml
```yaml
bases:
- ../../base
patches:
- patch.yaml
```

overlay/production/patch.yaml
```yaml
apiVersion: apps/v1
kind: Deployment
metadata:
  name: deployment-name
spec:
  replicas: 5
  template:
    spec:
      containers:
        - name: container-name
          resources:
            limits:
              memory: "128Mi"
              cpu: "250m"
```