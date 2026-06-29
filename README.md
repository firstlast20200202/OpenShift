demo: image streams

network:demos



apiVersion: build.openshift.io/v1
kind: BuildConfig
metadata:
  name: sample-docker-build
  namespace: my-project
  labels:
    app: sample-app
spec:
  runPolicy: Serial
  source:
    type: Git
    git:
      uri: 'https://github.com'
      ref: main
  strategy:
    type: Docker
    dockerStrategy:
      dockerfilePath: Dockerfile
  output:
    to:
      kind: ImageStreamTag
      name: 'sample-app:latest'
  triggers:
    - type: ConfigChange
    - type: ImageChange
      imageChange: {}
  successfulBuildsHistoryLimit: 3
  failedBuildsHistoryLimit: 3



