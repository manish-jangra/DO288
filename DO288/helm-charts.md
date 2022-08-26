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