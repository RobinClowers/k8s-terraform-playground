# Practice terraform k8s

Based on the official terraform k8s
[tutorial][tutorial].

## Setup

### KIND

If you are using kind, first create the clsuter:

```shell
kind create cluster --name terraform-learn --config kind-config.yaml
```

Then get the cluster info to populate your tfvars file (covered in the next
section).

```shell
kubectl cluster-info --context kind-terraform-learn
```

### Terraform

Create `learn-terraform-deploy-nginx-kubernetes/terraform.tfvars` and populate
it with values from `kubectl cluster-info`.

```terraform
host                   = "https://127.0.0.1:32768"
client_certificate     = "LS0tLS1CRUdJTiB..."
client_key             = "LS0tLS1CRUdJTiB..."
cluster_ca_certificate = "LS0tLS1CRUdJTiB..."
```

Now you should be able to run `terraform plan`, etc successfully.

[tutorial]: https://developer.hashicorp.com/terraform/tutorials/kubernetes/kubernetes-provider

## Applying changes

From the `learn-terraform-deploy-nginx-kubernetes` subdirectory, run
`terraform plan`. If the diff looks correct, run `terraform apply` to make the
changes to your cluster.

Verify the nginx deployment was created with `kubectl get deployments` or
`k9s`.

Verify the service was created with `kubectl get services`. I'm not sure how to
do this in `k9s`.

If everythink worked, you should be able to see the nginx welcome page at
`http://localhost:30201/`!
