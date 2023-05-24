# Role Call Helm Chart

This chart deploys role bindings in Kubernetes using the Helm package manager.

## Prerequisites

- Kubernetes 1.12+
- Helm 3.1.0

## Installing the Chart

To install the chart with the release name `my-release`:

```bash
helm install my-release role-call
```

This command deploys role-call on the Kubernetes cluster with the default configuration.

### Uninstalling the Chart

To uninstall the my-release deployment:

```bash
helm uninstall my-release
```

This command removes all the Kubernetes components associated with the chart and deletes the release.

## Configuration

The following tables list the configurable parameters of the role-call chart.

| Parameter              | Description                                                               | Default |
|------------------------|---------------------------------------------------------------------------|---------|
| `nameOverride`         | Overrides the Chart's name                                                | `""`    |
| `fullnameOverride`     | Overrides the full name of the resources                                  | `""`    |
| `serviceAccounts`      | List of ServiceAccounts to be created, each item should have 'name', 'namespace', 'labels', and 'annotations' fields | `[]`    |
| `roles`                | List of Roles to be created, each item should have 'name', 'namespace', and 'rules' fields | `[]`    |
| `roleBindings`         | List of RoleBindings to be created, each item should have 'name', 'namespace', 'role', and 'subjects' fields | `[]`    |
| `clusterRoles`         | List of ClusterRoles to be created, each item should have 'name' and 'rules' fields | `[]`    |
| `clusterRoleBindings`  | List of ClusterRoleBindings to be created, each item should have 'name', 'clusterRole', and 'subjects' fields | `[]`    |

### `serviceAccounts`

An array of objects, each representing a ServiceAccount. Each object can contain the following keys:

| Key | Description | Default | Required |
|-----|-------------|---------|----------|
| `name` | Name of the ServiceAccount. | | true |
| `namespace` | Namespace where the ServiceAccount will be created. | `default` | false |
| `labels` | Labels to be applied to the ServiceAccount. | `{}` | false |
| `annotations` | Annotations to be applied to the ServiceAccount. | `{}` | false |

### `roles`

An array of objects, each representing a Role. Each object can contain the following keys:

| Key | Description | Default | Required |
|-----|-------------|---------|----------|
| `name` | Name of the Role. | | true |
| `namespace` | Namespace where the Role will be created. | `default` | false |
| `labels` | Labels to be applied to the Role. | `{}` | false |
| `rules` | Array of rules applied to the Role (per [source](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole)) | `[]` | false |

### `roleBindings`

An array of objects, each representing a RoleBinding. Each object can contain the following keys:

| Key | Description | Default | Required |
|-----|-------------|---------|----------|
| `name` | Name of the RoleBinding. | | true |
| `namespace` | Namespace where the RoleBinding will be created. | `default` | false |
| `labels` | Labels to be applied to the RoleBinding. | `{}` | false |
| `role` | Name of the Role to be applied to the RoleBinding roleRef. | | true |
| `subjects` | Array of subjects applied to the RoleBinding (per [source](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding)) | `[]` | false |

### `clusterRoles`

An array of objects, each representing a ClusterRole. Each object can contain the following keys:

| Key | Description | Default | Required |
|-----|-------------|---------|----------|
| `name` | Name of the ClusterRole. | | true |
| `labels` | Labels to be applied to the ClusterRole. | `{}` | false |
| `rules` | Array of rules applied to the ClusterRole (per [source](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole)) | `[]` | false |

### `clusterRoleBindings`

An array of objects, each representing a ClusterRoleBinding. Each object can contain the following keys:

| Key | Description | Default | Required |
|-----|-------------|---------|----------|
| `name` | Name of the ClusterRoleBinding. | | true |
| `labels` | Labels to be applied to the ClusterRoleBinding. | `{}` | false |
| `clusterRole` | Name of the clusterRole to be applied to the ClusterRoleBinding roleRef. | | true |
| `subjects` | Array of subjects applied to the ClusterRoleBinding (per [source](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding)) | `[]` | false |

### Example

Here's an example of how to specify each parameter using a YAML file:

```yaml
serviceAccounts:
  - name: "service-account-1"

roles:
  - name: role-1
    rules:
      - apiGroups: [""]
        resources: ["pods"]
        verbs: ["get", "watch", "list"]

roleBindings:
  - name: role-binding-1
    role: role-1
    subjects:
      - kind: ServiceAccount
        name: service-account-1
      - kind: User
        name: foo@bar.com
      - kind: Group
        name: Users

clusterRoles:
  - name: cluster-role-1
    rules:
      - apiGroups: [""]
        resources: ["pods"]
        verbs: ["get", "watch", "list"]

clusterRoleBindings:
  - name: cluster-role-binding-1
    clusterRole: cluster-role-1
    subjects:
      - kind: ServiceAccount
        name: service-account-1
```
