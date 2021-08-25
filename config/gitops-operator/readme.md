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
