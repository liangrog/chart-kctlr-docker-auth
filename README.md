Kubernetes controller for creating secret of private docker repo
===
This Helm chart creates a custom controller deployment in kuberenetes for creating docker config secret.

What it does
---
- Oberving all namespaces lifecycle unless excluded
- Create/update/delete docker config secret in all namespaces
 
Values 
---
Please refer to `values.yaml` for value overrides. 

Installation
---
    
    $ helm install --namespace <your-namespace> .

Upgrade
---
    
    $ helm upgrade <release-name>

Delete
---

    $ helm delete <release-name>
