# Structure

This is a folder-based structure approach.

The _appproj_ folder is the usually called _base_ folder.

Each other folder is meant to be an overlay which collects all the resources
of a specific OpenShift GitOps instance.

Below a few structure examples.

1. `<ENV>-<PLATFORM>`
```
$ mkdir -p {prod,stage}-{gcp,azure}/projects/{default,myproject}/{app,appset}
$ touch {prod,stage}-{gcp,azure}/kustomization.yaml
$ tree
.
├── prod-azure
│   ├── kustomization.yaml
│   └── projects
│       ├── default
│       │   ├── app
│       │   └── appset
│       └── myproject
│           ├── app
│           └── appset
├── prod-gcp
│   ├── kustomization.yaml
│   └── projects
│       ├── default
│       │   ├── app
│       │   └── appset
│       └── myproject
│           ├── app
│           └── appset
├── stage-azure
│   ├── kustomization.yaml
│   └── projects
│       ├── default
│       │   ├── app
│       │   └── appset
│       └── myproject
│           ├── app
│           └── appset
└── stage-gcp
    ├── kustomization.yaml
    └── projects
        ├── default
        │   ├── app
        │   └── appset
        └── myproject
            ├── app
            └── appset
```

2. `<PLATFORM>`
```
$ mkdir -p {gcp,azure}/projects/{default,myproject}/{app,appset}
$ touch {gcp,azure}/kustomization.yaml
$ tree
.
├── azure
│   ├── kustomization.yaml
│   └── projects
│       ├── default
│       │   ├── app
│       │   └── appset
│       └── myproject
│           ├── app
│           └── appset
└── gcp
    ├── kustomization.yaml
    └── projects
        ├── default
        │   ├── app
        │   └── appset
        └── myproject
            ├── app
            └── appset
```
