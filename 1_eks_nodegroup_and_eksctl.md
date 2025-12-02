# 1_eks_nodegroup_and_eksctl.md

# 1. EKS Node Group – Key Fields

- `nodegroup-name` → Name of the node group
- `node-type: t3.medium` → EC2 instance type for worker nodes
- `nodes: 2` → Desired number of nodes
- `nodes-min: 1` → Minimum nodes in the node group
- `nodes-max: 3` → Maximum nodes in the node group
- `managed` → Managed Node Group (AWS manages lifecycle, scaling, and updates)

---

# 2. EKS / eksctl Cluster Creation (Concept)

- Using `eksctl` to create an EKS cluster:
  - Define cluster name
  - Define region
  - Define nodegroup-name
  - Define node-type and node count (nodes, nodes-min, nodes-max)
- `eksctl` reads the config and provisions:
  - EKS control plane
  - Managed worker node group(s)
