# kubernetesApplications

I am using the app of apps pattern in Argo CD to deploy and manage Kubernetes applications.

## sync waves

| name | sync wave |
| ---- | --------- |
| namespaceCreation | 0 |
| customResourceDefinitions | 5 |
| certManager | 10 |
| gatewayApi | 20 |
| cilium | 30 |
| longhorn | 40 |
| argocd | 50 |
| coredns | 60 |

## dependency list

| name | dependency list |
| ---- | ---------------- |
| namespaceCreation | none |
| customResourceDefinitions | none |
| certManager | namespaceCreation |
| gatewayApi | namespaceCreation, customResourceDefinitions, certManager |
| cilium | gatewayApi |
| longhorn | namespaceCreation, gatewayApi |
| argocd | gatewayApi |
| coredns | namespaceCreation, gatewayApi |

I am putting the gateway api routes with each application. That means then that gateway api and
certificates have to be in place before the other applications get installed.

## pod security admission standard

By default, this cluster is using the level = `restricted` for all 3 modes = `enforce`, `audit`, and `warn`.
Every namespace receives this level unless explicity overridden.

## kustomize patches

Uses JSON6902 style most of the time. Argocd uses strategic merge patches.
