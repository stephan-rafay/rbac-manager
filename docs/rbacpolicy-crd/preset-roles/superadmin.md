# 👑 SuperAdmin

### **SuperAdmin:**

The SuperAdmin role provides comprehensive read and write access to all cluster resources. It is designed for users with the authority to manage other users and service accounts.&#x20;

```yaml
apiVersion: rbac-manager.k8smgmt.io/v1
kind: RBACPolicy
metadata:
  name: example002-preset-rbac
spec:
  version: 1.0.0
  namespaceCreatePolicy: "IfNotPresent"
  customRbacBindings:
    - name: fullaccess
      subjects:
        - kind: ServiceAccount
          namespace: app
          name: robot
      presetBindings:
        - roleName: SuperAdmin
```

The above CRD represents the specification for an RBACPolicy using the `SuperAdmin` preset role. Let's break down the components of this spec:

* `apiVersion` and `kind`: These fields specify the API version and kind of the Custom Resource. In this case, it's an `RBACPolicy` in the `rbac-manager.k8smgmt.io/v1` API version.
* `metadata`: This section contains metadata about the RBACPolicy resource, including the name.
* `version`: This field specifies the version of the RBACPolicy. In this case, it's set to `1.0.0`.
* `namespaceCreatePolicy`: This field determines how namespaces should be handled. It can have one of two values:
  * `"IfNotPresent"`: This indicates that namespaces should be created if they do not already exist.
  * `"Never"`: This indicates that namespaces should never be created, and the RBACPolicy should only work with existing namespaces.
* `customRbacBindings`: This section defines custom RBAC bindings. It allows you to associate roles with specific subjects (users, service accounts, etc.). In this case:
  * `name`: A custom RBAC binding with the name `fullaccess` is defined.
  * `subjects`: This specifies the subjects to which the RBAC binding applies. In this case, it's a `ServiceAccount` named `robot` in the `app` namespace.
  * `presetBindings`: This field specifies preset bindings. The `SuperAdmin` role is assigned to the subjects defined above. It's a role that provides full read-and-write access to all resources.

{% hint style="info" %}
Inspect the ClusterRole and ClusterRoleBinding created by rbac-manager for the above CRD using the command below.

```bash
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
```
{% endhint %}
