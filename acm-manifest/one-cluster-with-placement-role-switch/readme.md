## correct one from label point of view


```
apiVersion: app.k8s.io/v1beta1
kind: Application
metadata:
  name: argocd
  namespace: openshift-gitops
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
          - argocd
---
apiVersion: apps.open-cluster-management.io/v1
kind: Subscription
metadata:
  name: argocd-subscription-1
  namespace: openshift-gitops
  annotations:
    apps.open-cluster-management.io/deployables: 'openshift-gitops/argocd-subscription-1-config-gitops-operator-cluster-admin-gitops-clusterrolebinding,openshift-gitops/argocd-subscription-1-config-gitops-operator-argocd-rbac-cm-configmap,openshift-gitops/argocd-subscription-1-config-gitops-operator-openshift-gitops-argocd'
    apps.open-cluster-management.io/git-branch: structure
    apps.open-cluster-management.io/git-path: config/gitops-operator
    apps.open-cluster-management.io/reconcile-option: replace
  labels:
    app: argocd
    app.kubernetes.io/part-of: argocd
    apps.open-cluster-management.io/reconcile-rate: high
spec:
  channel: ns-channel-ocpgitops/channel-openshift-gitops
  placement:
    placementRef:
      name: argocd-placement-1
      kind: PlacementRule
---
apiVersion: apps.open-cluster-management.io/v1
kind: PlacementRule
metadata:
  name: argocd-placement-1
  namespace: openshift-gitops
  labels:
    app: argocd
spec:
  clusterSelector:
    matchLabels:
      role: bc
```
