# Curated lists of projectSveltos ClusterProfiles

A list of ClusterProfiles included in this repository. 

### Agents  
- **Gitlab Agent**
- **Gitlab Runner**
### Monitoring  
- **Metrics Server**
### Networking
- **Calico**


## Usage

Install ProjectSveltos on your ClusterApi Management Cluster.

``` bash
helm repo add projectsveltos https://projectsveltos.github.io/helm-charts
```
``` bash
helm upgrade --install sveltos-crds projectsveltos/sveltos-crds
```

``` bash
helm upgrade --install projectsveltos projectsveltos/projectsveltos -n projectsveltos --create-namespace --set agent.managementCluster=true
```

### Bootstrap Flux and ClusterProfiles

The Flux `ClusterProfile` is the bootstrap profile and must be applied manually
before the other profiles. It installs Flux on the cluster selected by the
`reconcile: flux` label.

Apply it to the management cluster:

``` bash
kubectl apply -f reconciliation/fluxcd-clusterprofile.yaml
```

Add the selector label to the management cluster:

``` bash
kubectl label cluster <management-cluster> reconcile=flux --overwrite
```

After Flux is available, apply its Kustomization manually:

``` bash
kubectl apply -f reconciliation/clusterprofiles-kustomization.yaml
```

The Kustomization reads all YAML files from
`management/clusterprofiles/` and applies them to the management cluster.
This directory contains the remaining ProjectSveltos `ClusterProfile`
resources. Adding a new YAML file there does not require updating a resource
list.

The `ClusterProfile` resources then select tenant clusters using their labels.
For example, Calico VXLAN is activated by labeling a tenant cluster:

``` bash
kubectl label cluster <tenant-cluster> network=calico-vxlan-v3-32-0 --overwrite
```

Sveltos reads the referenced tenant configuration from the repository and
applies it to the selected tenant cluster.

## Tips


## Recommended Commit Types

| Type    | Content                                   | Example Commit                                  |
|---------|-----------------------------------------------|------------------------------------------------|
| `feat`  | Adding a new ClusterProfile            | `feat: add Calico clusterprofile`          |
| `fix`   | Fixing an existing issue          | `fix: correct value for Metrics CP`  |
| `docs`  | Updating documentation                         | `docs: add usage instructions for plugin X`  |
| `chore` | Repo cleanup, folder reorganization, config   | `chore: reorganize plugin folders`           |

