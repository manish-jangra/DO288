### Source-to-Image Builds
DevOps --> reduce time to market

Source to Image 

👉 Automatic Language Detection (OpenShift Special)

Builder Image Stream points to builder image (Application runtime + common dependencies for runtime)

Scripts: |
1. 👉  assemble --> builds application using source code
2. 👉  run --> sets the entrypoint for the application
3. 👉  save-artifacts --> saves build dependencies and recycles them next time when we build application (oc start-build)