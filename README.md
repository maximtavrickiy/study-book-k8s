# k8s-lab

Учебный репозиторий: путь от основ контейнеров до Kubernetes-кластера с gVisor.

## Цель

Развернуть Kubernetes-кластер (Kubespray) с **gVisor** для изоляции (sandboxing) ИИ-агентов и по дороге разобрать базовые DevOps-темы: контейнеры, архитектуру Kubernetes, Ansible, сеть, GitOps и эксплуатацию.

## Стенд

VirtualBox на Windows, три VM на Ubuntu 24.04 (mgmt, k8s-1, k8s-2). Подробности в [infra/README.md](infra/README.md).

## Модули

| № | Модуль | Тема | Теория | Практика | Лог | Вопросы |
|---|---|---|---|---|---|---|
| 00 | Foundations | namespaces, cgroups, OCI, containerd, runc | [theory](00-foundations/theory.md) | [tasks](00-foundations/tasks.md) | [notes](00-foundations/notes.md) | [questions](00-foundations/questions.md) |
| 01 | K8s architecture | control plane, узел, reconcile, базовые объекты, k3s | [theory](01-k8s-architecture/theory.md) | [tasks](01-k8s-architecture/tasks.md) | [notes](01-k8s-architecture/notes.md) | [questions](01-k8s-architecture/questions.md) |
| 02 | Kubespray | Ansible, kubeadm, inventory, group_vars | [theory](02-kubespray/theory.md) | [tasks](02-kubespray/tasks.md) | [notes](02-kubespray/notes.md) | [questions](02-kubespray/questions.md) |
| 03 | Networking | pod network, Service, CoreDNS, CNI, NetworkPolicy | [theory](03-networking/theory.md) | [tasks](03-networking/tasks.md) | [notes](03-networking/notes.md) | [questions](03-networking/questions.md) |
| 04 | ArgoCD / GitOps | декларативность, pull-деплой, Application | [theory](04-argocd-gitops/theory.md) | [tasks](04-argocd-gitops/tasks.md) | [notes](04-argocd-gitops/notes.md) | [questions](04-argocd-gitops/questions.md) |
| 05 | gVisor sandboxes | runsc, RuntimeClass, платформы, изоляция (**цель**) | [theory](05-gvisor-sandboxes/theory.md) | [tasks](05-gvisor-sandboxes/tasks.md) | [notes](05-gvisor-sandboxes/notes.md) | [questions](05-gvisor-sandboxes/questions.md) |
| 06 | Operations | ресурсы, probes, RBAC, Helm, мониторинг, бэкап etcd | [theory](06-operations/theory.md) | [tasks](06-operations/tasks.md) | [notes](06-operations/notes.md) | [questions](06-operations/questions.md) |
| 99 | Backlog | темы на потом (после модуля 05) | [ideas](99-backlog/ideas.md) | | | |

Прогресс и слабые места: [PROGRESS.md](PROGRESS.md). Инструкции для агента-репетитора: [AGENTS.md](AGENTS.md).

## Принципы

- **Теорию пишу сам** своими словами. В `theory.md` лежит только скелет тем.
- **`notes.md` — это лог ошибок**: симптом → гипотеза → проверка → причина → решение.
- `tasks.md` — практика чеклистом, с указанием VM и точки снапшота.
- `questions.md` — самопроверка, ответы пишу сам.
- `artifacts/` — манифесты, конфиги, выводы команд, которые стоит сохранить.

## ⚠️ Секреты не коммитить

Никаких SSH-ключей, `kubeconfig`/`admin.conf`, токенов ArgoCD, паролей и `.env` в git. Образы VM и снапшоты тоже не храним (см. `.gitignore`).
