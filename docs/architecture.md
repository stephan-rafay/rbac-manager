# Architecture

rbac-manager adheres to the Kubernetes operator design pattern, continuously monitoring the alignment between the actual and desired states of RBACPolicy objects. Within this context, rbac-manager executes reconciliation logic for various Kubernetes resources, including:

1. **RBACPolicy CRD:** The central custom resource definition that encapsulates access control policies.
2. **Service Accounts:** Identifying and managing service accounts used for RBAC.
3. **Namespaces:** Creating or updating namespaces as required by RBAC policies.
4. **Roles and ClusterRoles:** Generating role and cluster role objects based on CRD specifications.
5. **RoleBindings and ClusterRoleBindings:** Establishing bindings between roles and subjects, aligning with RBACPolicy directives.

<figure><img src=".gitbook/assets/Screenshot 2023-09-20 at 10.45.58 PM.png" alt=""><figcaption></figcaption></figure>

By closely aligning with the CRD spec, the rbac-manager dynamically generates corresponding RBAC roles and role bindings, ensuring that access controls remain in harmony with the defined policies. rbac-manager also reconciles RBACPolicy CRDs, Service Accounts, Namespaces, Roles, ClusterRoles, RoleBindings, and ClusterRoleBindings.

### How does rbac-manager create roles?

rbac-manager's role generation process relies on data sourced from the Kubernetes discovery API, which furnishes a comprehensive catalog of accessible API Groups, resources, and subresources within the cluster. Leveraging the RBACPolicy specification, the rbac-manager meticulously filters and includes the requisite resources in its role creation workflow. This dynamic approach ensures that roles are precisely tailored to match the policy's defined criteria, optimizing access control within the Kubernetes environment.

