Kubernetes  Course

Deploy
Install minikube and virtual box version 5.2

Database

```bash
$ minikub start
$ cd kubernetes/db/
$ kubectl create -f statefulset.yaml
$ kubectl create -f servico-banco.yaml
$ kubectl create -f permissoes.yaml
$ kubectl get pods
$ kubectl exec -it [mysql pod name]  sh
# mysql -u root
mysql> use loja
```

Paste the mysql script:
```
create table produtos (id integer auto_increment primary key, nome varchar(255), preco decimal(10,2));
alter table produtos add column usado boolean default false;
alter table produtos add column descricao varchar(255);
create table categorias (id integer auto_increment primary key, nome varchar(255));
insert into categorias (nome) values ("Futebol"), ("Volei"), ("Tenis");
alter table produtos add column categoria_id integer;
update produtos set categoria_id = 1;

```
APP

```
$ cd kubernetes/app/
$ kubectl create -f deployment.yaml
$ kubectl create -f servico-aplicacao.yaml
$ kubectl scale deployment aplicacao-deployment --replicas=3
$ kubectl get pods
$ minikube service servico-aplicacao --url
```
