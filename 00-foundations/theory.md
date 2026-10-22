# 00 Foundations — конспект

**Цель модуля:** понять, из чего сделан контейнер на уровне ядра Linux, что такое OCI, как устроены containerd и runc и чем этот стек отличается от Docker.

> Пишу своими словами. Под каждым заголовком — пустое место для конспекта.

## Процесс в Linux

## Namespaces

### Виды namespaces (pid, net, mnt, uts, ipc, user, cgroup, time)

### Как посмотреть namespaces процесса

## cgroups

### cgroup v1 vs v2

### Ограничение CPU и памяти

## Файловая система контейнера (overlayfs, слои образа)

## OCI

### Image spec

### Runtime spec

## runc

## containerd

### Архитектура (shim, snapshotter, CRI-плагин)

### ctr vs nerdctl vs crictl

## Docker vs containerd

## Контейнер как граница безопасности: что изолировано, а что нет (общее ядро)

## Что читать

- [Linux namespaces (man 7 namespaces)](https://man7.org/linux/man-pages/man7/namespaces.7.html)
- [cgroups v2 (kernel docs)](https://docs.kernel.org/admin-guide/cgroup-v2.html)
- [containerd docs](https://containerd.io/docs/) и [OCI specs](https://opencontainers.org/)
