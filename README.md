# kubernetesApplications

I am using the app of apps pattern in Argo CD to deploy and manage Kubernetes applications.

## sync waves

| name | sync wave |
| ---- | --------- |
| namespaceCreation | 0 |
| customResourceDefinitions | 10 |
| argocd | 20 |
| cilium | 30 |
| certManager | 40 |
| envoyGateway | 50 |
| longhorn | 60 |
| gatewayApi | 70 |

## dependency order

| name | dependency order | reason |
| ---- | ---------------- | ------ |
| namespaceCreation | run first | namespaces must exist before everything else |
| customResourceDefinitions | needs namespaceCreation | these can be namespace scoped |
| argocd | run whenever | has no dependencies that have not been met by the time this repo's code is running. best to run these sooner than later though since they are critical to a healthy cluster |
| cilium | run whenever | has no dependencies that have not been met by the time this repo's code is running. best to run these sooner than later though since they are critical to a healthy cluster |
| certManager | needs namespaceCreation |  |
| envoyGateway | needs namespaceCreation, certmanager |  |
| longhorn | needs namespaceCreation |  |
| gatewayApi | needs namespaceCreation, certManager, envoyGateway |  |
