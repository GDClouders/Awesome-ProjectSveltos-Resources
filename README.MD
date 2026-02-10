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

Install ProjectSveltos on your ClusterApi Management Cluster

``` bash
helm repo add projectsveltos https://projectsveltos.github.io/helm-charts
```
``` bash
helm upgrade --install projectsveltos/sveltos-crds projectsveltos/sveltos-crds
```

``` bash
helm upgrade --install projectsveltos projectsveltos/projectsveltos -n projectsveltos --create-namespace --set agent.managementCluster=true
```

## Tips


## Recommended Commit Types

| Type    | Content                                   | Example Commit                                  |
|---------|-----------------------------------------------|------------------------------------------------|
| `feat`  | Adding a new ClusterProfile            | `feat: add Calico clusterprofile`          |
| `fix`   | Fixing an existing issue          | `fix: correct value for Metrics CP`  |
| `docs`  | Updating documentation                         | `docs: add usage instructions for plugin X`  |
| `chore` | Repo cleanup, folder reorganization, config   | `chore: reorganize plugin folders`           |

