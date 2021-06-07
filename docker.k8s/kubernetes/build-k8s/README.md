# 온 프레미너 환경에서 쿠버네티스 구성

본 문서는 ansible 기반의 kubespary 도구를 사용하여 원격에서 클러스터를 구성하는 법을 기록

# 우선 조건

- 마스터 노드는 최소 2 core, 2 memory 이상이 필요하다
- 워커 노드는 최소 1 core, 1 memory 이상이 필요하다
- 각 노드는 호스트 이름, 맥 주소, Product_uuid가 서로 달라야하며, 노드의 포트는 개방되어 있어야한다
- 각 노드는 서로 시간 동기화가 되어야 있어야하며 모든 방화벽을 꺼준다
- 노드들 중에 가상 머신(VM)이 있을 경우, 쿠버네티스를 원격 설치하는 작업 머신의 ssh의 public key의 값을 가상머신의 노드에 있는 authorized_keys 파일에 추가한다 (문서 폴더 참고)

# 설치

```ShellSession
# download kubespray.zip

# cd kubespray

# Install dependencies from ``requirements.txt``
sudo pip3 install -r requirements.txt

# Review and change parameters under ``inventory/mycluster/group_vars``
cat inventory/mycluster/group_vars/all/all.yml
cat inventory/mycluster/group_vars/k8s_cluster/k8s_cluster.yml

# Deploy Kubespray with Ansible Playbook - run the playbook as root
# The option `--become` is required, as for example writing SSL keys in /etc/,
# installing packages and interacting with various systemd daemons.
# Without --become the playbook will fail to run!
ansible-playbook -i inventory/real/host.init  --become --become-user=root cluster.yml

# reset
ansible-playbook -i inventory/real/host.init  --become --become-user=root reset.yml
```

# Allowance load-balancer(service type) in On-premise

MetalLB을 이용: https://metallb.universe.tf/

step0. check requirementes

```
- A Kubernetes cluster, running Kubernetes 1.13.0 or later, that does not already have network load-balancing functionality.
- A cluster network configuration that can coexist with MetalLB.
- Some IPv4 addresses for MetalLB to hand out.
- When using the BGP operating mode, you will need one or more routers capable of speaking BGP.
- Traffic on port 7946 (TCP & UDP) must be allowed between nodes, as required by memberlist.
```

step1. installation

```
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.6/manifests/namespace.yaml
kubectl apply -f https://raw.githubusercontent.com/metallb/metallb/v0.9.6/manifests/metallb.yaml
# On first install only
kubectl create secret generic -n metallb-system memberlist --from-literal=secretkey="$(openssl rand -base64 128)"
```

step2. configuration

1. create config.yaml

```
apiVersion: v1
kind: ConfigMap
metadata:
  namespace: metallb-system
  name: config
data:
  config: |
    address-pools:
    - name: default
      protocol: layer2
      addresses:
      - 192.168.1.240-192.168.1.250
```

2. kubectl apply -f config.yaml

step3. testing

1. create test.yaml

```
apiVersion: v1
kind: Service
metadata:
  name: nginx
spec:
  ports:
  - port: 80
    targetPort: 80
  selector:
    app: nginx
  type: LoadBalancer
```

2. kubectl apply -f test.yaml
