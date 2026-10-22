# 04 ArgoCD / GitOps — конспект

**Цель модуля:** понять принципы GitOps и настроить доставку манифестов в кластер через ArgoCD из моего GitLab.

> Пишу своими словами. Под каждым заголовком — пустое место для конспекта.

## Декларативный vs императивный подход

## Принципы GitOps

### Git как источник истины

### Pull vs push-деплой

## ArgoCD

### Архитектура (api-server, repo-server, application-controller)

### Application

### Sync, sync policy (auto-sync, prune, self-heal)

### Health и sync status

### Drift: ручные изменения в кластере

### Projects (AppProject) и доступ

## Структура репозитория манифестов (plain YAML, Kustomize, Helm)

## App of Apps / ApplicationSet

## Доступ ArgoCD к GitLab (deploy token, SSH-ключ) и где хранить секреты

## Что читать

- [Argo CD docs](https://argo-cd.readthedocs.io/en/stable/)
- [OpenGitOps principles](https://opengitops.dev/)
- [Kubespray: аддоны (argocd)](https://github.com/kubernetes-sigs/kubespray/tree/master/docs)
