# Terraform kubernetes AKS

---
Este repositório faz parte da sequência de videos lançados pelo canal [Estação da TI](https://youtu.be/ZDmX6lqPThg)

---

**Pre requisitos:**
Para utilizar este script é necessário possuir uma conta Azure onde será feito o deploy e realizar a criação das credênciais que serão usadas pelo cluster Kubernetes.

**Criação do RBAC:**
```
az ad sp create-for-rbac --name <rbac-name> --role Contributor --scopes /subscriptions/<sub>
```
**\<rbac-name>** - Nome da credêncial usada pelo terraform
**\<sub>** - ID da subscription na Azure

**Executando o terraform:**
Para realizar a criação deste ambiente deve-se seguir a sequinte sequencia:

1- Preencher as informações do client secret geradas no RBAC nas variáveis.
2- Inicializar o terraform
```
terraform init
```
3- Criar os workspaces para separar os ambientes
```
terraform workspace new dev
``` 
4- Executar o plan passando como parametro as váriaveis do ambiente desejado
```
terraform plan -var-file="dev\dev.tfvars"
``` 
5- Se tudo estiver como esperado, basta executar
```
terraform apply -var-file="dev\dev.tfvars"
``` 

**Acessando o ambiente:**
Após a conclusão da criação do ambiente, pode ser executado o seguinte comando:

```
az aks get-credentials --resource-group $(terraform output -raw resource_group_name) --name $(terraform output -raw kubernetes_cluster_name)
``` 
Ele irá pegar a saída gerada pelo terraform para viabilizar a conexão no cluster usando a ferramenta de sua preferência como **kubectl**, por exemplo.


Se quiser ver este código em execução ou para mais informações acesse: [Estação da TI](https://youtu.be/ZDmX6lqPThg)
