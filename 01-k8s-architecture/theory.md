# 01 K8s architecture — конспект

**Цель модуля:** понять, из каких компонентов состоит Kubernetes, как они взаимодействуют, и освоить базовые объекты API.

> Пишу своими словами. Под каждым заголовком — пустое место для конспекта.

## Control plane

### kube-apiserver

### etcd

### kube-scheduler

### kube-controller-manager

## Узел (node)

### kubelet

### kube-proxy

### Container runtime и CRI

## Цикл reconcile (desired state vs actual state)

## Объекты API

### Pod

### Deployment и ReplicaSet

### Service

### Ingress

### ConfigMap

### Secret

### PersistentVolume и PersistentVolumeClaim

## Namespaces в Kubernetes, labels и selectors

## Путь от `kubectl apply` до запущенного пода

## k8s vs k3s

## Инструменты: kubectl, k9s, Lens

## Что читать

- [Kubernetes Components](https://kubernetes.io/docs/concepts/overview/components/)
- [Kubernetes Concepts](https://kubernetes.io/docs/concepts/)
- [k3s docs](https://docs.k3s.io/)
