# 🌠 Integration of Existing RBAC Rules

rbac-manager offers effortless integration of your current Kubernetes RBAC rules, encompassing `ClusterRoles`, `Roles`, `ClusterRoleBindings`, and `RoleBindings`. The following example demonstrates this capability:

```yaml
apiVersion: rbac-manager.k8smgmt.io/v1
kind: RBACPolicy
metadata:
  name: tc001-existing-clusterrole
spec:
  version: 1.0.0
  namespaceCreatePolicy: "IfNotPresent"
  clusterRoles:
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: ClusterRole
      metadata:
        name: cr-secret-reader
      rules:
      - apiGroups: [""]
        resources: ["secrets"]
        verbs: ["get", "watch", "list"]
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: ClusterRole
      metadata:
        name: cr-secret-writer
      rules:
      - apiGroups: [""]
        resources: ["secrets"]
        verbs: ["get", "watch", "list", "create", "update", "patch", "delete"]
  clusterRoleBindings:
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: ClusterRoleBinding
      metadata:
        name: read-secrets-robot
      subjects:
      - kind: ServiceAccount
        namespace: app
        name: robot-reader
      roleRef:
        kind: ClusterRole
        name: cr-secret-reader
        apiGroup: rbac.authorization.k8s.io
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: ClusterRoleBinding
      metadata:
        name: write-secrets-robot
      subjects:
      - kind: ServiceAccount
        namespace: app
        name: tc001-robot-writer
      roleRef:
        kind: ClusterRole
        name: cr-secret-writer
        apiGroup: rbac.authorization.k8s.io
```

In this example, rbac-manager seamlessly incorporates your existing Kubernetes `ClusterRoles` and `ClusterRoleBindings` into the RBACPolicy CRD specification. When applied, the rbac-manager creates these resources within the cluster, ensuring a smooth transition while preserving your established access control policies. This streamlined approach simplifies RBAC rule management, making it easier to maintain and adapt your access controls as needed.

Here is another example for `Roles` and `RoleBindings`

```yaml
apiVersion: rbac-manager.k8smgmt.io/v1
kind: RBACPolicy
metadata:
  name: tc002-existing-role
spec:
  version: 1.0.0
  namespaceCreatePolicy: "IfNotPresent" # (or) "Never"
  roles:
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: Role
      metadata:
        name: r-secret-reader
        namespace: default
      rules:
      - apiGroups: [""] # "" indicates the core API group
        resources: ["secrets"]
        verbs: ["get", "watch", "list"]
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: Role
      metadata:
        name: r-secret-writer
        namespace: default
      rules:
      - apiGroups: [""] # "" indicates the core API group
        resources: ["secrets"]
        verbs: [ "get", "watch", "list", create, update, patch, delete]
  roleBindings:
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: RoleBinding
      metadata:
        name: read-secrets-robot
        namespace: default
      subjects:
      - kind: ServiceAccount
        namespace: app
        name: tc002-robot-reader
      roleRef:
        kind: Role
        name: r-secret-reader
        apiGroup: rbac.authorization.k8s.io
    - apiVersion: rbac.authorization.k8s.io/v1
      kind: RoleBinding
      metadata:
        name: write-secrets-robot
        namespace: default
      subjects:
      - kind: ServiceAccount
        namespace: app
        name: tc002-robot-writer
      roleRef:
        kind: Role
        name: r-secret-writer
        apiGroup: rbac.authorization.k8s.io
```
