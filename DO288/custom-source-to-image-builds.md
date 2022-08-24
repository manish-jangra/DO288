## Source-to-Image Builds
DevOps --> reduce time to market

Source to Image 

👉 Automatic Language Detection (OpenShift Special)

Builder Image Stream points to builder image (Application runtime + common dependencies for runtime)

Scripts: |
1. 👉  assemble --> builds application using source code
2. 👉  run --> sets the entrypoint for the application
3. 👉  save-artifacts --> saves build dependencies and recycles them next time when we build application (oc start-build)

#### Create Custom Source to Image Build

s2i create image-name dir-name

s2i build test/test-app s2i-do288-httpd s2i-sample-app --as-dockerfile ~/dir/Containerfile

oc create secret generic quayio --from-file .dockerconfigjson=${XDG_RUNTIME_DIR}/containers/auth.json --type=kubernetes.io/dockerconfigjson

oc import-image s2i-do288-httpd --from quay.io/${RHT_OCP4_QUAY_USER}/s2i-do288-httpd --confirm

skopeo copy containers-storage:localhost/s2i-do288-httpd docker://quay.io/${RHT_OCP4_QUAY_USER}/s2i-do288-httpd —format v2s

export APP_URL=$(oc get route/hello-s2i -o jsonpath='{.spec.host}{"\n"}')