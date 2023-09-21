# Architecture

rbac-manager adheres to the Kubernetes operator design pattern, continuously monitoring the alignment between the actual and desired states of RBACPolicy objects. Within this context, rbac-manager executes reconciliation logic for various Kubernetes resources, including:

1. **RBACPolicy CRD:** The central custom resource definition that encapsulates access control policies.
2. **Service Accounts:** Identifying and managing service accounts used for RBAC.
3. **Namespaces:** Creating or updating namespaces as required by RBAC policies.
4. **Roles and ClusterRoles:** Generating role and cluster role objects based on CRD specifications.
5. **RoleBindings and ClusterRoleBindings:** Establishing bindings between roles and subjects, aligning with RBACPolicy directives.

<figure><img src=".gitbook/assets/Screenshot 2023-09-20 at 10.45.58 PM.png" alt=""><figcaption></figcaption></figure>

By closely aligning with the CRD spec, the rbac-manager dynamically generates corresponding RBAC roles and role bindings, ensuring that access controls remain in harmony with the defined policies. rbac-manager also reconciles RBACPolicy CRDs, Service Accounts, Namespaces, Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings.

