# 03 Networking — конспект

**Цель модуля:** понять, как устроена сеть в Kubernetes: адресация подов, Services, DNS, CNI-плагины и NetworkPolicy.

> Пишу своими словами. Под каждым заголовком — пустое место для конспекта.

## Сетевая модель Kubernetes (требования к pod network)

## Pod network

### Pod CIDR и адреса узлов

### veth, bridge, маршруты на узле

## Service

### ClusterIP

### NodePort

### LoadBalancer (и почему на голом железе нужен MetalLB или аналог)

### Как kube-proxy реализует Service (iptables / IPVS / nftables)

## CoreDNS

### Имена сервисов (`svc.ns.svc.cluster.local`)

### `/etc/resolv.conf` в поде

## CNI

### Что такое CNI-плагин и когда он вызывается

## Calico vs Flannel

### Overlay (VXLAN, IPIP) vs BGP / маршрутизация без инкапсуляции

### Поддержка NetworkPolicy

## NetworkPolicy

### Ingress и egress-правила

### Default deny

### Политики для песочниц

## Путь пакета: под A на узле 1 → под B на узле 2

## Что читать

- [Cluster Networking](https://kubernetes.io/docs/concepts/cluster-administration/networking/)
- [Network Policies](https://kubernetes.io/docs/concepts/services-networking/network-policies/)
- [Calico docs](https://docs.tigera.io/calico/latest/about/)
