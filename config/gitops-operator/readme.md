## Default instance of gitops-operator is controller to:
```
apiVersion: pipelines.openshift.io/v1alpha1
kind: GitopsService
metadata:
  creationTimestamp: '2021-08-25T09:55:19Z'
  generation: 1
  managedFields:
    - apiVersion: pipelines.openshift.io/v1alpha1
      fieldsType: FieldsV1
      fieldsV1:
        'f:spec': {}
      manager: gitops-operator
      operation: Update
      time: '2021-08-25T09:55:19Z'
  name: cluster
  resourceVersion: '9121571'
  uid: 31ab0ff6-f2ce-4672-8d83-eec41247b4b4
spec: {}
```
### when you try t delete default instance the problem is showing that 
![image](https://user-images.githubusercontent.com/14099560/130774556-579e2186-6cff-455b-9950-3e9c329dffbb.png)


## argocd-cm example

```
kind: ConfigMap
apiVersion: v1
metadata:
  name: argocd-cm
  namespace: openshift-gitops
  labels:
    app.kubernetes.io/managed-by: openshift-gitops
    app.kubernetes.io/name: argocd-cm
    app.kubernetes.io/part-of: argocd
data:
  admin.enabled: 'true'
  statusbadge.enabled: 'false'
  resource.exclusions: |
    - apiGroups:
      - tekton.dev
      clusters:
      - '*'
      kinds:
      - TaskRun
      - PipelineRun
  ga.trackingid: ''
  repositories: |
    - passwordSecret:
        key: password
        name: myreposecret
      type: git
      url: <GIT_REPOSITORY> <-- Add Git repository URL here
      usernameSecret:
        key: username
        name: myreposecret
  ga.anonymizeusers: 'false'
  help.chatUrl: ''
  url: 'CLUSTER_URL' <-- Insert cluster URL here
  help.chatText: ''
  kustomize.buildOptions: ''
  resource.inclusions: ''
  repository.credentials: ''
  dex.config: |
    connectors:
    - config:
        clientID: system:serviceaccount:openshift-gitops:openshift-gitops-argocd-dex-server
        clientSecret: CLIENT_SECRET <-- Add client secret here
        insecureCA: true
        issuer: https://kubernetes.default.svc
        redirectURI: https://openshift-gitops-server-openshift-gitops.apps.cluster-name.base-domain.lab/api/dex/callback
      id: openshift
      name: OpenShift
      type: openshift
  users.anonymous.enabled: 'false'
  configManagementPlugins: ''
  application.instanceLabelKey: ''
```
