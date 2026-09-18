# Cluster Kubernetes com Kind e Terraform

## Objetivo

Provisionar um cluster Kubernetes local utilizando **Terraform** e **Kind (Kubernetes in Docker)**.

## Cluster

* **Nome:** devops
* **Control Plane:** 1
* **Workers:** 2
* **Kubernetes:** v1.35.0
* **Terraform:** 1.16.0
* **Kind:** utilizado para executar o Kubernetes em containers Docker.

### Topologia

```text
devops
├── devops-control-plane
├── devops-worker
└── devops-worker2
```

## Provisionamento

O cluster foi criado exclusivamente através do Terraform utilizando:

```bash
terraform init
terraform validate
terraform plan
terraform apply
```

O Terraform confirmou a criação:

```text
Apply complete! Resources: 1 added, 0 changed, 0 destroyed.
```

A configuração do `main.tf` define 1 control-plane e 2 workers.

## Principais componentes

* **Control Plane:** gerencia o cluster Kubernetes.
* **Worker Nodes:** executam os Pods e aplicações.
* **kube-apiserver:** disponibiliza a API do Kubernetes.
* **etcd:** armazena o estado do cluster.
* **kube-scheduler:** seleciona os nodes para execução dos Pods.
* **CoreDNS:** realiza a resolução de nomes dentro do cluster.
* **kube-proxy:** auxilia na comunicação de rede dos serviços.

## Evidências

Foram utilizados os seguintes comandos para verificar o cluster:

```bash
kubectl get nodes -o wide
kubectl cluster-info
kind get clusters
```

O comando `kubectl get nodes -o wide` confirmou:

```text
devops-control-plane   Ready   control-plane
devops-worker          Ready   <none>
devops-worker2         Ready   <none>
```

Todos os três nodes estão com status **Ready**.

## Estrutura

```text
terraform-kind/
├── main.tf
├── variables.tf
├── terraform.tfvars
├── README.md
└── evidencias/
    ├── 01-terraform-apply.png
    ├── 02-kubectl-get-nodes.png
    ├── 03-kubectl-cluster-info.png
    └── 04-kind-get-clusters.png
```

## Conclusão

O cluster **devops** foi provisionado com sucesso utilizando Terraform e Kind, atendendo à topologia exigida de **1 control-plane + 2 workers**.

