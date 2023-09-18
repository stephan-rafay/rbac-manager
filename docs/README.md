---
description: >-
  Welcome to the documentation for rbac-manager. In this section, we provide an
  overview of rbac-manager, its goals, and how it can empower administrators to
  implement RBAC policies efficiently.
---

# Introduction

**What is rbac-manager?**

RBAC manager is a Kubernetes operator designed to streamline the management of RBAC policies in your Kubernetes clusters. By introducing the RBACPolicy custom resource definition (CRD), rbac-manager simplifies the task of granting and denying access to resources, following the least-privilege model.

**Key Goals of rbac-manager**

A few key objectives drive our project:

1. **RBAC Management**: Kubernetes RBAC rules only support allowing access (granting permissions) but do not support a "deny" rule. This limitation can make it challenging to implement fine-grained access controls, especially when you want to deny access to specific resources while allowing access to others.
2. **Complexity Reduction**: Managing RBAC manually through YAML files can become complex and error-prone, especially as the number of users in a cluster grows. rbac-manager introduces a custom resource definition (CRD) called RBACPolicy. With RBACPolicy, administrators can specify which resources should be denied access (or) which should be allowed access. This approach helps simplify the management of RBAC configurations. With RBACPolicy, the administrator can consolidate all the RBAC rules into a single YAML file. The RBAC manager simplifies the complexity by providing a more user-friendly and efficient way to manage RBAC policies.
3. **Automation**: It automates the generation of RBAC rules at run time when namespaces are created. RBACPolicy allows you to specify rules based on label selectors and automate the creation of roles and role bindings as the cluster's namespace is created, reducing the manual effort required to maintain RBAC definitions per namespace.
4. **Least-Privilege Model**: rbac-manager enables administrators to adhere to the least privilege principle, a security best practice. It allows you to define RBAC policies that grant access only to the necessary resources for users and service accounts, enhancing the security of your cluster.

**Getting Started with rbac-manager**

Ready to dive in? Our "Getting Started" section will walk you through the initial steps of deploying and configuring rbac-manager in your Kubernetes environment. We'll guide you through creating your first RBACPolicy custom resource, providing clear code examples and practical use cases to help you hit the ground running.

Join us on this journey to simplify Kubernetes RBAC management with rbac-manager. Let's get started!
