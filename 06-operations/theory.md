# 06 Operations — конспект

**Цель модуля:** освоить базу эксплуатации кластера и применить её к песочницам ИИ-агентов.

> Пишу своими словами. Под каждым заголовком — пустое место для конспекта.

## Ресурсы

### requests и limits

### QoS-классы (Guaranteed, Burstable, BestEffort)

### ResourceQuota

### LimitRange

## Probes (liveness, readiness, startup)

## RBAC

### Role / ClusterRole, RoleBinding / ClusterRoleBinding

### ServiceAccount и токены

## Helm (chart, values, release)

## Мониторинг: Prometheus и Grafana

## Обновление кластера (Kubespray upgrade, порядок, version skew)

## Бэкап и восстановление etcd

## Эксплуатация песочниц

### Namespace на сессию

### TTL подов (`activeDeadlineSeconds`, Job `ttlSecondsAfterFinished`, контроллеры очистки)

### Запрет сети

### Лимиты ресурсов и квоты на сессию

## Что читать

- [Managing Resources for Containers](https://kubernetes.io/docs/concepts/configuration/manage-resources-containers/)
- [Using RBAC Authorization](https://kubernetes.io/docs/reference/access-authn-authz/rbac/)
- [Operating etcd clusters for Kubernetes](https://kubernetes.io/docs/tasks/administer-cluster/configure-upgrade-etcd/)
