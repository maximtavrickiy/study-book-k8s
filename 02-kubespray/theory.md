# 02 Kubespray — конспект

**Цель модуля:** понять Ansible на уровне, достаточном для Kubespray, разобраться, что Kubespray делает под капотом, и развернуть с его помощью кластер.

> Пишу своими словами. Под каждым заголовком — пустое место для конспекта.

## Ansible

### Inventory (хосты, группы, host_vars, group_vars)

### Playbook, play, task

### Role

### Модули, идемпотентность, handlers

### Приоритет переменных

## Kubespray под капотом

### Порядок этапов (подготовка ОС, container runtime, etcd, kubeadm, CNI, аддоны)

### Роль kubeadm

### etcd: где и как разворачивается

### Установка CNI

## Структура inventory/mycluster

### hosts.yaml (группы kube_control_plane, kube_node, etcd)

### group_vars/all

### group_vars/k8s_cluster

## Ключевые переменные

### `container_manager: containerd`

### `kube_network_plugin`

### Аддоны (`*_enabled`)

### `vars.yaml` / переопределение через `-e`

## Сценарии: cluster.yml, scale.yml, remove-node.yml, upgrade-cluster.yml, reset.yml

## Поддержка ОС и версий (Ubuntu 24.04, версии Kubernetes)

## Control plane vs worker

## Что читать

- [Kubespray (GitHub, README)](https://github.com/kubernetes-sigs/kubespray)
- [Kubespray docs](https://kubespray.io/)
- [Ansible: Getting started](https://docs.ansible.com/ansible/latest/getting_started/index.html)
