# 05 gVisor sandboxes — конспект

**Цель модуля (главная цель курса):** понять, как gVisor изолирует контейнеры, и запустить в кластере поды через `RuntimeClass: gvisor` как основу песочниц для ИИ-агентов.

> Пишу своими словами. Под каждым заголовком — пустое место для конспекта.

## Модель угроз: почему общего ядра недостаточно

## gVisor: общая идея (ядро в user space)

### Sentry

### Gofer и доступ к файловой системе

### Сеть (netstack)

## runsc как OCI-runtime

## Перехват syscalls

## Платформы

### systrap

### ptrace

### KVM

### Какую платформу можно использовать в VirtualBox и почему

## Цена по производительности (syscall-heavy, I/O, сеть)

## Совместимость: что не поддерживается

## Интеграция с Kubernetes

### RuntimeClass

### Runtime handlers в containerd (`config.toml`, `runtime_type`)

### Kubespray: `gvisor_enabled` (точное место переменной для моей версии)

## От каких атак gVisor защищает, а от каких нет

## gVisor vs Kata Containers vs Firecracker

## Что читать

- [gVisor docs](https://gvisor.dev/docs/)
- [gVisor: Platforms](https://gvisor.dev/docs/architecture_guide/platforms/)
- [Kubernetes RuntimeClass](https://kubernetes.io/docs/concepts/containers/runtime-class/)
