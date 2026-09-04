# Relatório de Provisionamento - Cluster Kubernetes (Kind)

##  Informações Gerais
* **Nome do Cluster:** devops
* **Topologia:** 1 Nó Controller (Control Plane) e 2 Nós Workers.
* **Ferramenta de Provisionamento:** Terraform (Provider: `tehcyx/kind`).

---

##  Principais Componentes Provisionados pelo Kind

O Kind (Kubernetes in Docker) cria um cluster simulando os nós como containers Docker. Dentro deste ambiente, os seguintes componentes principais foram provisionados de forma automatizada:

### 1. Control Plane (Nó Controller)
Responsável por gerenciar todo o cluster, tomar decisões globais e responder aos eventos. Contém:
* **kube-apiserver:** A porta de entrada do cluster. Tudo o que fazemos via `kubectl` ou Terraform passa por ele.
* **etcd:** Banco de dados chave-valor ultra-seguro que armazena todas as configurações e o estado atual do cluster.
* **kube-scheduler:** O cérebro que decide em qual nó worker cada aplicação nova deve rodar, baseando-se nos recursos disponíveis.
* **kube-controller-manager:** O fiscal do cluster. Ele garante que o número planejado de pods e serviços esteja sempre rodando corretamente.

### 2. Nós Workers (Trabalhadores)
São os nós responsáveis por executar as aplicações de fato. Contêm:
* **kubelet:** Um agente que roda em cada nó e garante que os containers estejam rodando dentro dos pods conforme as ordens do Control Plane.
* **kube-proxy:** O guarda de trânsito da rede. Ele cuida das regras de rede de cada nó, permitindo a comunicação entre os componentes.

### 3. Componentes de Sistema (Add-ons padrão)
* **CoreDNS:** Responsável por dar nomes (DNS) aos serviços internos do cluster, permitindo que uma aplicação ache a outra facilmente.
