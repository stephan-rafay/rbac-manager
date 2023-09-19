# 🛰 WorkSpaceWriteRestricted

### **WorkSpaceWriteRestricted:**

This role is suited for users responsible for creating, updating, and deleting namespaces while maintaining read and write access to resources within those namespaces, except for specific exclusions like Service Accounts, Secrets, Roles, RoleBindings, and pods/exec operations.

```yaml
apiVersion: rbac-manager.k8smgmt.io/v1
kind: RBACPolicy
metadata:
  name: tc018-preset-rbac
spec:
  version: 1.0.0
  namespaceCreatePolicy: "IfNotPresent"
  customRbacBindings:
    - name: appadmin
      subjects:
        - kind: ServiceAccount
          namespace: app
          name: robot
      presetBindings:
        - roleName: WorkSpaceWriteRestricted
          namespaceSelector:
            matchLabels:
              key1: value1
```

The provided YAML snippet represents the specification (spec) for an RBACPolicy, specifically for the "WorkSpaceWriteRestricted" preset role. Let's break down the components of this RBACPolicy CRD spec:

* `apiVersion` and `kind`: These fields specify the API version and kind of the Custom Resource. In this case, it's an `RBACPolicy` in the `rbac-manager.k8smgmt.io/v1` API version.
* `metadata`: This section contains metadata about the RBACPolicy resource, including the name.
* `version`: This field specifies the version of the RBACPolicy. In this case, it's set to `1.0.0`.
* `namespaceCreatePolicy`: This field determines how namespaces should be handled. It can have one of two values:
  * `"IfNotPresent"`: This policy indicates that namespaces should be created if they do not already exist.
  * `"Never"`: This policy indicates that namespaces should never be created, and the RBACPolicy should only work with existing namespaces.
* `customRbacBindings`: This section defines custom RBAC bindings. It allows you to associate roles with specific subjects (users, service accounts, etc.). In this case:
  * `name`: A custom RBAC binding with the name `appadmin` is defined.
  * `subjects`: This specifies the subjects to which the RBAC binding applies. In this case, it's a `ServiceAccount` named `robot` in the `app` namespace.
  * `presetBindings`: This field specifies preset bindings. The `WorkSpaceWriteRestricted` role is assigned to the subjects defined above. It's a role that allows users with this binding to create, update, and delete namespaces and grants read and write access to almost all resources in those namespaces except secrets, service accounts, roles, rolebinding, and pods/exec. It includes namespace selectors that grant access to namespaces based on labels and expressions.
  * `namespaceSelector`: This field defines criteria for selecting namespaces based on labels and expressions. In this case, namespaces with the label `key1: value1` are allowed for access.

{% hint style="info" %}
Note that the automatic RBAC reconciliation ensures that your access control rules are consistently enforced for existing namespaces and those created in the future that meet the selector criteria.
{% endhint %}

{% hint style="info" %}
Inspect the ClusterRole and ClusterRoleBinding created by rbac-manager for the above CRD using the commands below.

```bash
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
```
{% endhint %}

{% hint style="info" %}
Inspect Role and RoleBinding created by rbac-manager in namespaces that match the selector using the commands below.

```
kubectl get role -A -l rbac-manager=k8smgmt
kubectl get rolebinding -A -l rbac-manager=k8smgmt
```
{% endhint %}
