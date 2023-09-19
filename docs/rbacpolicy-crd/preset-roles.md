---
description: >-
  In this section, we explore the convenience and efficiency of using preset
  roles provided by the RBACPolicy Custom Resource Definition (CRD) in
  rbac-manager.
---

# Preset Roles

## **What are Preset Roles?**

Preset roles are preconfigured access control roles that cover common use cases and scenarios within Kubernetes. RBACPolicy CRD simplifies RBAC management by offering these ready-made roles, eliminating the need for extensive custom configurations. These roles are designed to promote security best practices while streamlining your access control setup.

## **Supported Preset Roles**

rbac-manager offers a range of preset roles to simplify access management within your Kubernetes clusters. These roles cater to diverse user needs, ensuring you can grant permissions efficiently and securely. Let's explore these roles in detail:

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

### **SuperAdminRead:**

The SuperAdminRead role grants only read access to all cluster resources. It's ideal for users tasked with troubleshooting and monitoring cluster activities.

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
        - roleName: SuperAdminRead
```

The above CRD represents the specification for an RBACPolicy using the `SuperAdminRead` preset role. Let's break down the components of this spec:

* `apiVersion` and `kind`: These fields specify the API version and kind of the Custom Resource. In this case, it's an `RBACPolicy` in the `rbac-manager.k8smgmt.io/v1` API version.
* `metadata`: This section contains metadata about the RBACPolicy resource, including the name.
* `version`: This field specifies the version of the RBACPolicy. In this case, it's set to `1.0.0`.
* `namespaceCreatePolicy`: This field determines how namespaces should be handled. It can have one of two values:
  * `"IfNotPresent"`: This indicates that namespaces should be created if they do not already exist.
  * `"Never"`: This indicates that namespaces should never be created, and the RBACPolicy should only work with existing namespaces.
* `customRbacBindings`: This section defines custom RBAC bindings. It allows you to associate roles with specific subjects (users, service accounts, etc.). In this case:
  * `name`: A custom RBAC binding with the name `fullaccess` is defined.
  * `subjects`: This specifies the subjects to which the RBAC binding applies. In this case, it's a `ServiceAccount` named `robot` in the `app` namespace.
  * `presetBindings`: This field specifies preset bindings. The `SuperAdminRead` role is assigned to the subjects defined above. It's a role that provides only read access to all resources.

{% hint style="info" %}
Inspect the ClusterRole and ClusterRoleBinding created by rbac-manager for the above CRD using the command below.

```bash
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
```
{% endhint %}

### **Admin:**

The Admin role offers read and write access to most resources, with exceptions. It's tailored for infrastructure administrators who need control but should not manage user access to clusters. Resources exempted include Service Accounts, ClusterRoles, ClusterRoleBindings, Roles, and RoleBindings.

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
        - roleName: Admin
```

The above CRD represents the specification for an RBACPolicy using the `Admin` preset role. Let's break down the components of this spec:

* `apiVersion` and `kind`: These fields specify the API version and kind of the Custom Resource. In this case, it's an `RBACPolicy` in the `rbac-manager.k8smgmt.io/v1` API version.
* `metadata`: This section contains metadata about the RBACPolicy resource, including the name.
* `version`: This field specifies the version of the RBACPolicy. In this case, it's set to `1.0.0`.
* `namespaceCreatePolicy`: This field determines how namespaces should be handled. It can have one of two values:
  * `"IfNotPresent"`: This indicates that namespaces should be created if they do not already exist.
  * `"Never"`: This indicates that namespaces should never be created, and the RBACPolicy should only work with existing namespaces.
* `customRbacBindings`: This section defines custom RBAC bindings. It allows you to associate roles with specific subjects (users, service accounts, etc.). In this case:
  * `name`: A custom RBAC binding with the name `fullaccess` is defined.
  * `subjects`: This specifies the subjects to which the RBAC binding applies. In this case, it's a `ServiceAccount` named `robot` in the `app` namespace.
  * `presetBindings`: This field specifies preset bindings. The `Admin` role is assigned to the subjects defined above.

{% hint style="info" %}
Inspect the ClusterRole and ClusterRoleBinding created by rbac-manager for the above CRD using the command below.

```bash
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
```
{% endhint %}

### **AdminRead:**

The AdminRead role offers only read access to most resources, with exceptions. It's tailored for infrastructure administrators who need to troubleshoot and monitor cluster activities but should not see RBAC details. Like Admin, the exempted resources include Service Accounts, ClusterRoles, ClusterRoleBindings, Roles, and RoleBindings.

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
        - roleName: AdminRead
```

The above CRD represents the specification for an RBACPolicy using the `Admin` preset role. Let's break down the components of this spec:

* `apiVersion` and `kind`: These fields specify the API version and kind of the Custom Resource. In this case, it's an `RBACPolicy` in the `rbac-manager.k8smgmt.io/v1` API version.
* `metadata`: This section contains metadata about the RBACPolicy resource, including the name.
* `version`: This field specifies the version of the RBACPolicy. In this case, it's set to `1.0.0`.
* `namespaceCreatePolicy`: This field determines how namespaces should be handled. It can have one of two values:
  * `"IfNotPresent"`: This indicates that namespaces should be created if they do not already exist.
  * `"Never"`: This indicates that namespaces should never be created, and the RBACPolicy should only work with existing namespaces.
* `customRbacBindings`: This section defines custom RBAC bindings. It allows you to associate roles with specific subjects (users, service accounts, etc.). In this case:
  * `name`: A custom RBAC binding with the name `fullaccess` is defined.
  * `subjects`: This specifies the subjects to which the RBAC binding applies. In this case, it's a `ServiceAccount` named `robot` in the `app` namespace.
  * `presetBindings`: This field specifies preset bindings. The `AdminRead` role is assigned to the subjects defined above.

{% hint style="info" %}
Inspect the ClusterRole and ClusterRoleBinding created by rbac-manager for the above CRD using the command below.

```bash
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
```
{% endhint %}

### **WorkSpaceAdmin:**

The WorkSpaceAdmin role empowers users to create, update, and delete namespaces. Additionally, it grants read and write access to resources within those namespaces, excluding specific resources like Service Accounts, Roles, and RoleBindings. This role is ideal for application administrators who can deploy applications to clusters.

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
        - roleName: WorkSpaceAdmin
          namespaceSelector:
            matchLabels:
              key1: value1
```

The provided YAML snippet represents the specification (spec) for an RBACPolicy, specifically for the "WorkSpaceAdmin" preset role. Let's break down the components of this RBACPolicy CRD spec:

* `apiVersion` and `kind`: These fields specify the API version and kind of the Custom Resource. In this case, it's an `RBACPolicy` in the `rbac-manager.k8smgmt.io/v1` API version.
* `metadata`: This section contains metadata about the RBACPolicy resource, including the name.
* `version`: This field specifies the version of the RBACPolicy. In this case, it's set to `1.0.0`.
* `namespaceCreatePolicy`: This field determines how namespaces should be handled. It can have one of two values:
  * `"IfNotPresent"`: This policy indicates that namespaces should be created if they do not already exist.
  * `"Never"`: This policy indicates that namespaces should never be created, and the RBACPolicy should only work with existing namespaces.
* `customRbacBindings`: This section defines custom RBAC bindings. It allows you to associate roles with specific subjects (users, service accounts, etc.). In this case:
  * `name`: A custom RBAC binding with the name `appadmin` is defined.
  * `subjects`: This specifies the subjects to which the RBAC binding applies. In this case, it's a `ServiceAccount` named `robot` in the `app` namespace.
  * `presetBindings`: This field specifies preset bindings. The `WorkSpaceAdmin` role is assigned to the subjects defined above. It's a role that allows users with this binding to create, update, and delete namespaces and grants read and write access to all resources in those namespaces. However, it includes namespace selectors that restrict access to namespaces based on labels and expressions.
  * `namespaceSelector`: This field defines criteria for selecting namespaces based on labels and expressions. In this case, namespaces with the label `key1: value1` are allowed for access.

{% hint style="info" %}
Note that the automatic RBAC reconciliation ensures that your access control rules are consistently enforced, both for existing namespaces and those created in the future that meet the selector criteria.
{% endhint %}



{% hint style="info" %}
Inspect the ClusterRole, ClusterRoleBinding created by rbac-manager for the above CRD using the command below.

Also, inspect Role and RoleBinding created by rbac-manager in namespaces that match the selector using the command below.

```bash
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
kubectl get role -A -l rbac-manager=k8smgmt
kubectl get rolebinding -A -l rbac-manager=k8smgmt

```
{% endhint %}

### **AdminRead:**

**6. WorkSpaceWriteRestricted:**

* This role is suited for users responsible for creating, updating, and deleting namespaces while maintaining read and write access to resources within them, except for certain exclusions like Service Accounts, Secrets, Roles, RoleBindings, and pod/exec operations.

**7. NameSpaceAdmin:**

* The NameSpaceAdmin role offers read and write access to all resources within a namespace, except for Service Accounts, Roles, and RoleBindings.

**8. NameSpaceRead:**

* For users who require read access to all resources within a namespace, the NameSpaceRead role is a suitable choice. It excludes access to Service Accounts, Roles, and RoleBindings.

**9. NameSpaceWriteRestricted:**

* NameSpaceWriteRestricted allows users to perform read and write operations within a namespace, excluding certain resources like Service Accounts and Secrets.

**10. NameSpaceReadRestricted:** - The NameSpaceReadRestricted role grants read access to resources within a namespace while restricting access to Service Accounts, Secrets, Roles, RoleBindings, and pod/exec operations.

These preset roles are thoughtfully designed to simplify RBAC management in Kubernetes. You can select the role that best aligns with your user's responsibilities, ensuring they have the precise access needed to perform their tasks securely and efficiently.
