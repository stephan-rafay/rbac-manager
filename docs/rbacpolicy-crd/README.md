---
description: >-
  In this section, we delve deep into the core of rbac-manager, the RBACPolicy
  CRD. This resource is the linchpin of fine-grained access control.
---

# RBACPolicy CRD

### **What is the RBACPolicy CRD?**

The RBACPolicy CRD, introduced by rbac-manager, allows you to grant and deny access to Kubernetes resources, fostering the principle of least privilege and enhancing the security posture of your clusters.

### **Key Features and Concepts**

#### **Preset Roles**

RBACPolicy CRD simplifies RBAC management by offering a selection of preset roles. Administrators can quickly assign permissions using predefined roles for common use cases without the need for extensive custom configurations. For information on supported preset roles, please refer to the documentation for the respective preset roles.

#### Custom Role

While the Preset roles offer convenience and simplicity, the rbac-manager's custom role capability empowers you to craft RBAC rules to meet your specific needs. The most flexible feature of rbac-manager is the ability to create custom roles, granting you the utmost control over fine-grained access rules without the need for complex RBAC whitelisting configuration.

#### **Seamless Integration of Existing RBAC Rules**

rbac-manager goes the extra mile to simplify RBAC management by offering support for seamlessly integrating your existing Kubernetes RBAC rules into the RBACPolicy CRD. This feature is invaluable for organizations looking to migrate their current RBAC definitions into rbac-manager's streamlined access control framework.

By enabling you to retain your existing RBAC configurations, rbac-manager ensures a smooth transition and preserves your established access control policies. This capability enhances the versatility and adaptability of rbac-manager, making it a powerful tool for both managing existing setups and implementing new access controls.

