
# note from rela app

apiVersion: app.k8s.io/v1beta1
kind: Application
metadata:
  name: openshift-gitops
  namespace: acm-ocpgitops-prod <<-- this is not correct 
  labels:
    app: openshift-gitops
  annotations:
    apps.open-cluster-management.io/deployables: ''
spec:
  componentKinds:
    - group: apps.open-cluster-management.io
      kind: Subscription
  descriptor: {}
  selector:
    matchExpressions:
      - key: app
        operator: In
        values:
          - openshift-gitops
---
apiVersion: apps.open-cluster-management.io/v1
kind: Subscription
metadata:
  name: sub-openshift-gitops-prod
  namespace: acm-ocpgitops-prod
  annotations:
    apps.open-cluster-management.io/deployables: 'acm-ocpgitops-prod/sub-openshift-gitops-prod-config-gitops-operator-openshift-gitops-argocd,acm-ocpgitops-prod/sub-openshift-gitops-prod-config-gitops-operator-cluster-admin-gitops-clusterrolebinding,acm-ocpgitops-prod/sub-openshift-gitops-prod-config-gitops-operator-argocd-rbac-cm-configmap'
    apps.open-cluster-management.io/git-branch: structure
    apps.open-cluster-management.io/git-path: config/gitops-operator
    apps.open-cluster-management.io/reconcile-option: replace
  labels:
    app: openshift-gitops
    app.kubernetes.io/part-of: openshift-gitops
    apps.open-cluster-management.io/reconcile-rate: high
spec:
  channel: acm-ocpgitops/channel-openshift-gitops
  placement:
    placementRef:
      name: pr-openshift-gitops
      kind: PlacementRule
---
apiVersion: apps.open-cluster-management.io/v1
kind: PlacementRule
metadata:
  name: pr-openshift-gitops
  namespace: acm-ocpgitops-prod
  labels:
    app: penshift-gitops
spec:
  clusterConditions:
    - status: 'True'
      type: ManagedClusterConditionAvailable
  clusterSelector:
    matchLabels:
      role: bc
