Kubernetes controller for creating secret of private docker repo
===
This Helm chart creates a custom controller deployment in kuberenetes for creating docker config secret.

What it does
---
- Oberving all namespaces lifecycle unless excluded
- Create/update/delete docker config secret in all namespaces (if not specify exclusion)
 
Values 
---

|         Name        |    requirement    |        Default       |                 Description             |
|:-------------------:|:-----------------:|:--------------------:|:---------------------------------------:|
| kubeConfigType | optional | in | "in": controller will pick it up within the cluster <br /> "out": controller will pick it up from a given path. If set this type, you must set "kubeConfigPath" |
| kubeConfigPath | conditonal |   | Kubernetes config file path when setting "kubeConfigType" to "out" |
| workerNumber | optional | 2 | Number of workers to spawn
| exclude | optional |   | Namespaces not to observe. Comma delimited string. e.g. "ns1,ns2" |
| awsKey | mandatory |    | AWS access key id |
| awsSecret | mandatory |    | AWS secret access key |
| awsRegion | mandatory |    | AWS region |
| awsHttpsProxy | optional |    | Https proxy address if using proxy to make AWS calls |
| ecrResyncPeriod | optional |  2  | How often to globally sync ECR login token in hours |
| ecrSecretName | optional | ecr | Name of the ECR secret get created |

Installation
---
    
    $ helm install --namespace <your-namespace> .

Upgrade
---
    
    $ helm upgrade <release-name>

Delete
---

    $ helm delete <release-name>
