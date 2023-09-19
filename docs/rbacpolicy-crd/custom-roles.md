# Custom Roles

Preset roles in rbac-manager are designed for ease and efficiency, providing predefined access controls for common use cases. However, custom roles become your go-to solution when your access control requirements demand specificity. It allows you to define access rules with exceptional precision. Whether it's read or write access, resource-specific permissions, or complex scenarios, custom roles give you complete control over who can do what within your Kubernetes clusters. The following capabilities provide you with the precision and flexibility you need to craft access policies that align perfectly with your requirements:

### **denyResources:**&#x20;

This feature lets you specify the Kubernetes resources that should be explicitly denied access. This allows you to create strict controls and block access to specific resources.

#### **Example Use Case: Restricting Secrets Management**

Imagine a scenario where you need to grant users full access to the cluster but prevent them from managing one resource, say secrets. With rbac-manager, achieving this level of control is straightforward. You can create a Custom Resource Definition (CRD) like the one below:

```yaml
apiVersion: rbac-manager.k8smgmt.io/v1
kind: RBACPolicy
metadata:
  name: tc007-custom-rbac
spec:
  version: 1.0.0
  namespaceCreatePolicy: "IfNotPresent"
  customClusterRoles:
   - name: deny-secret
     denyResources:
       - secrets
     allowedVerbs:
       - "*"    # for other resources
  customRbacBindings:
    - name: bind-robot-sa
      subjects:
        - kind: ServiceAccount
          namespace: app
          name: robot
      clusterRoleBindings:
        - clusterRole: deny-secret
```

In this example, the `deny-secret` Custom Cluster Role is configured to deny access to the `secrets` resource while permitting full access to all other resources. This specific binding ensures that the user, represented by the `ServiceAccount` named `robot` in the `app` namespace is prevented from managing secrets but has full access to all the other resources in the cluster.

{% hint style="info" %}
Inspect the ClusterRole and ClusterRoleBinding created by rbac-manager for the above CRD using the commands below.&#x20;

```
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
```
{% endhint %}

When you run the above commands, you'll witness rbac-manager's remarkable capability in action. It automatically identifies and includes all available resources within the cluster while crafting a ClusterRole that encompasses whitelisting rules for each resource. It's important to note that it excludes the `secret` resource, thus ensuring a comprehensive access policy.&#x20;

The alternative of manually crafting such extensive YAML specifications for RBAC can be daunting and error-prone. rbac-manager streamlines this process, making complex access control manageable and accurate, ultimately enhancing the security and manageability of your Kubernetes environment.



***

### **allowedResources:**

allowedResources enables you to specify the Kubernetes resources that should be granted access. Whether it's pods, services, or other resources, you can define exactly what can be accessed.

#### **Example Use Case: Grant Access To pods**

Imagine a scenario where you need to grant users access to only manage pods in the cluster. With rbac-manager, achieving this level of control is straightforward. You can create a Custom Resource Definition (CRD) like the one below:

```yaml
apiVersion: rbac-manager.k8smgmt.io/v1
kind: RBACPolicy
metadata:
  name: tc008-custom-rbac
spec:
  version: 1.0.0
  namespaceCreatePolicy: "IfNotPresent"
  customClusterRoles:
   - name: allow-pods
     allowedResources:
       - pods
       - pods/exec
       - pods/log
       - pods/status
       - pods/portforward
       - pods/proxy
     allowedVerbs:
       - "*"    # for other resources
  customRbacBindings:
    - name: bind-robot-sa
      subjects:
        - kind: ServiceAccount
          namespace: app
          name: robot
      clusterRoleBindings:
        - clusterRole: allow-pods
```

In this example, the `allow-pods` Custom Cluster Role is configured to grant access to specific `pods` resources and subresources. while denying access to all other resources. This specific binding ensures that the user, represented by the `ServiceAccount` named `robot` in the `app` namespace is only allowed to manage specific resources and subresources in the cluster.

{% hint style="info" %}
Inspect the ClusterRole and ClusterRoleBinding created by rbac-manager for the above CRD using the commands below.&#x20;

```
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
```
{% endhint %}



***

### **allowedGroups:**&#x20;

This feature lets you specify Kubernetes resource API groups that should be granted access. You can fine-tune access based on specific resource groups, ensuring that permissions are granted only where necessary.

#### **Example Use Case: Grant Access To Specific API Groups**

Imagine a scenario where you need to grant users access to manage all resources in specific [API groups](https://kubernetes.io/docs/reference/generated/kubernetes-api/v1.28/#-strong-api-groups-strong-). With rbac-manager, achieving this level of control is straightforward. You can create a Custom Resource Definition (CRD) like the one below:

```yaml
apiVersion: rbac-manager.k8smgmt.io/v1
kind: RBACPolicy
metadata:
  name: tc009-custom-rbac
spec:
  version: 1.0.0
  namespaceCreatePolicy: "IfNotPresent"
  customClusterRoles:
   - name: allow-groups
     allowedVerbs:
       - "*"    
     allowedGroups:
        - ""               # core group
        - events.k8s.io
        - apps
        - networking.k8s.io
  customRbacBindings:
    - name: bind-robot-sa
      subjects:
        - kind: ServiceAccount
          namespace: app
          name: robot
      clusterRoleBindings:
        - clusterRole: allow-groups
```

In this example, the `allow-groups` Custom Cluster Role is configured to grant access to all resources in specific `groups` such as  `core`, `events.k8s.io`, `apps`, `networking.k8s.io`, while denying access to all other resources. This specific binding ensures that the user, represented by the `ServiceAccount` named `robot` in the `app` namespace, is allowed to manage all resources in the above specific groups.

{% hint style="info" %}
Inspect the ClusterRole and ClusterRoleBinding created by rbac-manager for the above CRD using the commands below.&#x20;

```
kubectl get clusterrole -l rbac-manager=k8smgmt
kubectl get clusterrolebinding -l rbac-manager=k8smgmt
```
{% endhint %}



***

### **allowedVerbs:**&#x20;

rbac-manager allows you to specify Kubernetes resource actions that should be granted access. You can define precisely which actions, such as create, read, update, or delete, are permitted, adding an additional layer of control to your access policies.

Below is a list of available verbs.

<pre class="language-yaml"><code class="lang-yaml"><strong>allowedVerbs:  # all verbs / read and write
</strong>  - "*"   
</code></pre>

```yaml
 allowedVerbs: # all verbs / read and write
  - list
  - get
  - watch
  - create
  - update
  - patch
  - delete

```

```yaml
 allowedVerbs: # read 
  - list
  - get
  - watch
```
