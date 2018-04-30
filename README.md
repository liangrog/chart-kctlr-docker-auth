ECR Image Pull Secret Controller
===
This [Helm chart](https://github.com/kubernetes/helm) creates a custom controller in Kubernetes cluster that will 

- Oberving all namespaces lifecycle unless excluded
- Create/update/delete ECR docker config secret in all namespaces accordingly
- Periodically refresh all ECR secrets before expiration
 
Values 
---

|         Name        |    Requirement    |        Default       |                 Description             |
|:--------------------|:-----------------:|:--------------------:|:----------------------------------------|
| kubeConfigType | optional | in | "**in**": controller will pick it up within the cluster <br /> "**out**": controller will pick it up from a given path. If set this type, you must set "kubeConfigFilePath" |
| kubeConfigFilePath | conditonal |   | Kubernetes config file path on host when setting "kubeConfigType" to "out" |
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


How to use
---
Simply add the secret name in your deployment/daemonset/pod spec, e.g.

    apiVersion: v1
    kind: Pod
    metadata:
    name: private-reg
    spec:
      imagePullSecrets:
      - name: ecr
      ...
      containers:
      - name: private-reg-container
        image: <your-private-image>
      ...

