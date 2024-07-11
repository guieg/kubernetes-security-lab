# Laboratório: Segurança no contexto de Kubernetes

## Requisitos

- Ansible
- Vagrant
- VirtualBox
- kubectl
- docker
- helm

# Ambiente

Para iniciar esse ambiente siga os passos a seguir:

1. Inicie as máquinas virtuais:

```bash
vagrant up
```

2. Execute o script ansible:

```bash
ansible-playbook -i inventory.yml setup_cluster.yml --ask-pass
```
> Utilize a senha "vagrant"

3. Agora é necessário obter o arquivo de configuração do cluster kubernetes, para isso execute os seguintes commandos:
```bash
vagrant ssh node1 -c "cp ~/.kube/config /vagrant"
export KUBECONFIG=$PWD/config
```

4. Se o ambiente foi corretamente criado o comando seguinte deve dar a saída referente:

```bash
$ kubectl get nodes
NAME    STATUS   ROLES           AGE    VERSION
node1   Ready    control-plane   5min   v1.30.1
node2   Ready    <none>          5min   v1.30.1
node3   Ready    <none>          5min   v1.30.1

```

## Remoção do ambiente

1. É possível desligar as máquinas virtuais com o comando:

```bash
vagrant halt
```

2. Caso deseje apagar as máquinas virtuais, utilize o comando:

```bash
vagrant destroy
```

# Deployment de aplicação

1. Baixe as configurações da aplicação:

```bash
git clone https://github.com/dockersamples/example-voting-app.git
```

2. Faça deployment no kubernetes:

```bash

kubectl create -f example-voting-app/k8s-specifications/
```

3. Duas aplicações estarão disponíveis em:

http://192.168.56.10:31000/
http://192.168.56.10:31001/

# Ferramentas de segurança

## Trivy

1. Utilizaremos o trivy como container local, você pode baixar a imagem com:

```bash
docker pull aquasec/trivy
```

2. Escolher um pod no cluster e obter imagem com:

```bash
kubectl get pods vote-69cb46f6fb-v5mh7 -o yaml
```

3. Escanear a imagem com trivy:

```bash
docker run aquasec/trivy image dockersamples/examplevotingapp_vote
```

5. Para fazer análises do cluster:

```bash
$ helm repo add aqua https://aquasecurity.github.io/helm-charts/
$ helm install trivy-operator aqua/trivy-operator \
     --namespace trivy-system \
     --create-namespace \
     --version 0.21.4

$ kubectl get vulnerabilityreports --all-namespaces -o wide

$ kubectl get ciskubebenchreports -o wide

$ kubectl describe vulnerabilityreports replicaset-vote-69cb46f6fb-vote 
```


