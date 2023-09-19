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

rbac-manager offers a range of carefully crafted preset roles to simplify access control management within your Kubernetes clusters. These roles cater to diverse user needs, ensuring you can grant permissions efficiently and securely. Let's explore these roles in detail:

### **SuperAdmin:**

The SuperAdmin role provides comprehensive read and write access to all cluster resources. It is designed for users with the authority to provision clusters, manage other users and service accounts, and manage access to resources for them.

**2. SuperAdminRead:**

* The SuperAdminRead role grants full read access to all cluster resources. It's ideal for users tasked with troubleshooting and monitoring cluster activities.

**3. Admin:**

* The Admin role offers read and write access to most resources, with exceptions. It's tailored for infrastructure administrators who need control but should not manage user access to clusters. Resources exempted include Service Accounts, ClusterRoles, ClusterRoleBindings, Roles, and RoleBindings.

**4. AdminRead:**

* Similar to Admin, the AdminRead role provides read access to most resources while excluding the same set of resources as Admin.

**5. WorkSpaceAdmin:**

* The WorkSpaceAdmin role empowers users to create, update, and delete namespaces. Additionally, it grants read and write access to resources within those namespaces, excluding specific resources like Service Accounts, Roles, and RoleBindings.

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
