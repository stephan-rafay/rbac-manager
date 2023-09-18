# README

The RBAC manager is a Kubernetes operator aiming to simplify managing Role-Based Access Control (RBAC) policies in Kubernetes clusters. RBAC is a critical security feature within Kubernetes that enables administrators to define and execute permissions for users and service accounts.

Here's an overview of what rbac-manager does and why it's valuable:

1. **RBAC Policy Management**: Kubernetes RBAC rules only support allowing access (granting permissions) but does not support a "deny" rule out of the box. This limitation can make it challenging to implement fine-grained access controls, especially when you want to deny access to specific resources while allowing access to others.
2. **RBACPolicy Custom Resource**: rbac-manager introduces a custom resource definition (CRD) called RBACPolicy. With RBACPolicy, administrators can specify which resources should be denied access (or) which should be allowed access. This approach helps simplify the management of RBAC configurations.&#x20;
3. **Complexity Reduction**: Managing RBAC policies manually through YAML files can become complex and error-prone, especially as the number of users in a cluster grows. rbac-manager simplifies this complexity by providing a more user-friendly and efficient way to manage RBAC policies. With RBACPolicy, the administrator can consolidate all the RBAC rules into a single YAML file.
4. **Automation**: It automates the generation of RBAC rules at run time when namespaces are created. RBACPolicy allows you to specify rules based on label selectors and automate the creation of roles and role bindings as the cluster's namespace is created, reducing the manual effort required to maintain RBAC definitions per namespace.
5. **Least-Privilege Model**: rbac-manager enables administrators to adhere to the least privilege principle, a security best practice. It allows you to define RBAC policies that grant access only to the necessary resources for users and service accounts, enhancing the security of your cluster.

In summary, rbac-manager is a tool that streamlines RBAC policy management in Kubernetes by introducing a custom resource (RBACPolicy) and automation. It simplifies defining RBAC policies, making it easier to implement and maintain the principle of least privilege for users and service accounts in your Kubernetes clusters.
