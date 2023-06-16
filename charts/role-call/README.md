# role-call

![Version: 0.1.0](https://img.shields.io/badge/Version-0.1.0-informational?style=flat-square) ![Type: application](https://img.shields.io/badge/Type-application-informational?style=flat-square) ![AppVersion: 1.16.0](https://img.shields.io/badge/AppVersion-1.16.0-informational?style=flat-square)

A chart to deploy service accounts and role bindings.

## Installation

```sh
helm install --generate-name dudo/role-call
```

## Configuration

The following table lists the configurable parameters of the chart, its default values, and required parameters.

## Values

| Key | Type | Default | Description |
|-----|------|---------|-------------|
| clusterRoleBindings | list | `[]` | List of ClusterRoleBindings to be created. <br/> *name* -- required -- Name of the RoleBinding <br/> *labels* -- Labels to be applied to the RoleBinding <br/> *clusterRole* -- required -- Name of the Role to be applied to the RoleBinding roleRef <br/> *subjects* -- Array of subjects applied to the RoleBinding (per [source](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding)) |
| clusterRoles | list | `[]` | List of ClusterRoles to be created. <br/> *name* -- required -- Name of the Role <br/> *labels* -- Labels to be applied to the Role <br/> *rules* -- Array of rules applied to the Role (per [source](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole)) |
| fullnameOverride | string | `""` | Override the full qualified app name |
| nameOverride | string | `""` | Override name of app |
| roleBindings | list | `[]` | List of RoleBindings to be created. <br/> *name* -- required -- Name of the RoleBinding <br/> *namespace* -- Namespace where the RoleBinding will be created <br/> *labels* -- Labels to be applied to the RoleBinding <br/> *role* -- required -- Name of the Role to be applied to the RoleBinding roleRef <br/> *subjects* -- Array of subjects applied to the RoleBinding (per [source](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#rolebinding-and-clusterrolebinding)) |
| roles | list | `[]` | List of Roles to be created. <br/> *name* -- required -- Name of the Role <br/> *namespace* -- Namespace where the Role will be created <br/> *labels* -- Labels to be applied to the Role <br/> *rules* -- Array of rules applied to the Role (per [source](https://kubernetes.io/docs/reference/access-authn-authz/rbac/#role-and-clusterrole)) |
| serviceAccounts | list | `[]` | List of ServiceAccounts to be created. <br/> *name* -- required -- Name of the ServiceAccount <br/> *namespace* -- Namespace where the ServiceAccount will be created <br/> *labels* -- Labels to be applied to the ServiceAccount <br/> *annotations* -- Annotations to be applied to the ServiceAccount |

### Example

Here's an example specifying each parameter:

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
