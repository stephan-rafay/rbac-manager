# 🎯 NameSpaceAdmin

### **NameSpaceAdmin:**

The NameSpaceAdmin role offers read and write access to all namespace scope resources except for Service Accounts, Roles, and RoleBindings. This allows interaction with deployments, pods, services, and other resources essential for developing and maintaining applications, but certain boundaries are in place to secure the Kubernetes environment. Notably, they do not have the authority to create, update, or delete namespaces in the cluster.&#x20;

By assigning the `NameSpaceAdmin` role, you enable your development teams to collaborate effectively, experiment, and innovate within their designated namespaces. It empowers developers to focus on their applications while safeguarding essential cluster-wide configurations.

```yaml
apiVersion: rbac-manager.k8smgmt.io/v1
kind: RBACPolicy
metadata:
  name: tc014-preset-rbac
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
        - roleName: NameSpaceAdmin
          namespaceSelector:
            matchLabels:
              key1: value1
```

The provided YAML snippet represents the specification (spec) for an RBACPolicy, specifically for the "NameSpaceAdmin" preset role. Let's break down the components of this RBACPolicy CRD spec:

* `apiVersion` and `kind`: These fields specify the API version and kind of the Custom Resource. In this case, it's an `RBACPolicy` in the `rbac-manager.k8smgmt.io/v1` API version.
* `metadata`: This section contains metadata about the RBACPolicy resource, including the name.
* `version`: This field specifies the version of the RBACPolicy. In this case, it's set to `1.0.0`.
* `namespaceCreatePolicy`: This field determines how namespaces should be handled. It can have one of two values:
  * `"IfNotPresent"`: This policy indicates that namespaces should be created if they do not already exist.
  * `"Never"`: This policy indicates that namespaces should never be created, and the RBACPolicy should only work with existing namespaces.
* `customRbacBindings`: This section defines custom RBAC bindings. It allows you to associate roles with specific subjects (users, service accounts, etc.). In this case:
  * `name`: A custom RBAC binding with the name `appadmin` is defined.
  * `subjects`: This specifies the subjects to which the RBAC binding applies. In this case, it's a `ServiceAccount` named `robot` in the `app` namespace.
  * `presetBindings`: This field specifies preset bindings. The `NameSpaceAdmin` role is assigned to the subjects defined above. It's a role that grants users read and write access to almost all namespace scope resources in a specific namespace.  It includes namespace selectors that grant access to namespaces based on labels and expressions. Excluded resources are service accounts, roles, and rolebinding.
  * `namespaceSelector`: This field defines criteria for selecting namespaces based on labels and expressions. In this case, namespaces with the label `key1: value1` are allowed for access.

{% hint style="info" %}
Note that the automatic RBAC reconciliation ensures that your access control rules are consistently enforced for existing namespaces and those created in the future that meet the selector criteria.
{% endhint %}

{% hint style="info" %}
Inspect Role and RoleBinding created by rbac-manager in namespaces that match the selector using the commands below.

```
kubectl get role -A -l rbac-manager=k8smgmt
kubectl get rolebinding -A -l rbac-manager=k8smgmt
```
{% endhint %}

\
