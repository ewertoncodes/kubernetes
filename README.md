# Kubernetes  Course

**Install VirtualBox**

[Virtualbox](https://www.virtualbox.org/wiki/Linux_Downloads)

**Install Minikube**

Install curl:

```
sudo apt-get install curl
```

Open the terminal and type this command:

```
curl -Lo minikube https://storage.googleapis.com/minikube/releases/latest/minikube-linux-amd64 && sudo chmod +x minikube && sudo mv minikube /usr/local/bin/
```

**Install kubectl**

```
curl -LO https://storage.googleapis.com/kubernetes-release/release/$(curl -s https://storage.googleapis.com/kubernetes-release/release/stable.txt)/bin/linux/amd64/kubectl
```



```
 chmod +x ./kubectl 
```



```
sudo mv ./kubectl /usr/local/bin/kubectl 
```

clone the repo:

```
git clone https://github.com/ewertoncodes/kubernetes.git
```
**Database**

```bash
$ minikube start
$ cd kubernetes/db/
$ kubectl create -f statefulset.yaml
$ kubectl create -f servico-banco.yaml
$ kubectl create -f permissoes.yaml
$ kubectl get pods
$ kubectl exec -it [mysql pod name]  sh
# mysql -u root
mysql> use loja
```

Paste the **Mysql** script:
```
create table produtos (id integer auto_increment primary key, nome varchar(255), preco decimal(10,2));
alter table produtos add column usado boolean default false;
alter table produtos add column descricao varchar(255);
create table categorias (id integer auto_increment primary key, nome varchar(255));
insert into categorias (nome) values ("Futebol"), ("Volei"), ("Tenis");
alter table produtos add column categoria_id integer;
update produtos set categoria_id = 1;

```
**Application**

```
$ cd kubernetes/app/
$ kubectl create -f deployment.yaml
$ kubectl create -f servico-aplicacao.yaml
$ kubectl scale deployment aplicacao-deployment --replicas=3
$ kubectl get pods
$ minikube service servico-aplicacao --url
```
