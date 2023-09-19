---
description: >-
  In this section, we provide instructions on how to set up rbac-manager in your
  Kubernetes cluster.
---

# Installation

### **Before You Begin**



Before diving into the installation and configuration of rbac-manager, please make sure you've reviewed the following points:

#### **Kubernetes Cluster:**

* Ensure that you have access to a running Kubernetes cluster.&#x20;

#### **kubectl Command-line Tool:**

* Ensure you have the `kubectl` command-line tool installed and properly configured to interact with your Kubernetes cluster.

#### **Access Permissions:**

* Ensure you have the necessary permissions and access to the Kubernetes cluster to install custom resources and create RBAC policies. You might need cluster admin or similar privileges depending on your cluster setup.

#### **Understanding of RBAC Concepts:**

* Understanding Kubernetes RBAC concepts, such as cluster roles, roles, rolebindings, clusterrolebindings, and service accounts, is beneficial. If you're new to RBAC, consider reading Kubernetes RBAC documentation as a primer.

### **Installation using Helm**

To install rbac-manager using Helm, you can follow these steps. Ensure you have Helm installed on your system before proceeding.

#### **Step 1: Add the rbac-manager Helm Repository**

You'll need to add the rbac-manager Helm repository to Helm using the following command:

```bash
helm repo add rbacmanager https://stephan-rafay.github.io/rbac-manager/
```

#### **Step 2: Update the Helm Repositories**

Update your Helm repositories to ensure you have the latest information:

```bash
helm repo update
```

#### **Step 3: Install rbac-manager**

Now, you can install rbac-manager using Helm.&#x20;

<pre class="language-bash"><code class="lang-bash"><strong>helm install rbacmanager-v010 rbacmanager/rbacmanager --version 0.1.0 \
</strong>--create-namespace --namespace rbac-manager-system
</code></pre>

You can customize the installation by providing a `values.yaml`file with your desired settings.&#x20;

```bash
helm install rbacmanager-v010 rbacmanager/rbacmanager --version 0.1.0 \
--create-namespace --namespace rbac-manager-system -f values.yaml
```

Replace `values.yaml` with the path to your configuration file if you're using one.&#x20;

{% hint style="info" %}
To access the details of values, use the following command.

<pre><code><strong>helm show values rbacmanager
</strong></code></pre>
{% endhint %}

#### **Step 4: Verify the Installation**

After the Helm installation is complete, you can verify that rbac-manager is running correctly in your Kubernetes cluster.&#x20;

Use the Helm list command:

```bash
helm list -n rbac-manager-system
```

> ```
> NAME            	NAMESPACE          	REVISION	UPDATED                             	STATUS  	CHART            	APP VERSION
> rbacmanager-v010	rbac-manager-system	1       	2023-09-18 16:36:45.396931 -0700 PDT	deployed	rbacmanager-0.1.0	0.1.0
> ```

***

You can use `kubectl` to check the pods, services, and logs. You should see the rbac-manager pods and services listed for the installation.

```bash
kubectl get pod -n rbac-manager-system
```

> <pre><code>NAME                                                   READY   STATUS    RESTARTS   AGE
> <strong>rbacmanager-v010-controller-manager-66d5d5b95c-nzcb5   2/2     Running   0          4m37s
> </strong></code></pre>

***

```
kubectl get svc -n rbac-manager-system
```

> ```
> NAME                                                  TYPE        CLUSTER-IP     EXTERNAL-IP   PORT(S)    AGE
> rbacmanager-v010-controller-manager-metrics-service   ClusterIP   10.96.207.34   <none>        8443/TCP   4m26s
> ```

***

```bash
kubectl logs -f -n rbac-manager-system -l control-plane=controller-manager
```

***

```bash
kubectl get crd rbacpolicies.rbac-manager.k8smgmt.io
```

> NAME                                                            CREATED AT
>
> rbacpolicies.rbac-manager.k8smgmt.io     2023-09-18T23:36:46Z

***

#### **Step 5: Configure RBAC Policies**

Now that rbac-manager is installed, you can create RBAC policies using the RBACPolicy custom resource. Refer to the documentation for guidance on creating RBACPolicy resources to define your access control rules.

That's it! You've successfully installed rbac-manager using Helm. You can now start simplifying RBAC policy management in your Kubernetes cluster.&#x20;

\
