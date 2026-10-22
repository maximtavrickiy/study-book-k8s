# 06 Operations — практика

Исходная точка: кластер с gVisor, снапшот `05-gvisor-done`.

## Ресурсы

- [ ] Запустить под с requests/limits, превысить лимит памяти и увидеть OOMKilled
- [ ] Посмотреть QoS-класс подов (`kubectl get pod -o jsonpath='{.status.qosClass}'`)
- [ ] Создать ResourceQuota в namespace и превысить её
- [ ] Создать LimitRange и убедиться, что под без ресурсов получает значения по умолчанию

## Probes

- [ ] Добавить readiness и liveness probe к приложению, сломать их и наблюдать поведение (рестарты, исключение из Service)

## RBAC

- [ ] Создать ServiceAccount с правами только на чтение подов в одном namespace
- [ ] Проверить права через `kubectl auth can-i --as=system:serviceaccount:<ns>:<sa>`
- [ ] Убедиться, что под песочницы не имеет доступа к API (`automountServiceAccountToken: false`)

## Helm и мониторинг

- [ ] **На mgmt:** установить Helm
- [ ] Установить kube-prometheus-stack через Helm (с урезанными ресурсами под стенд)
- [ ] Открыть Grafana, найти дашборды по узлам и подам (пароль **не коммитить**)
- [ ] 📸 **Снапшот: `06-monitoring`**

## Бэкап и обновление

- [ ] **На k8s-1:** сделать снапшот etcd (`etcdctl snapshot save`), проверить `snapshot status`
- [ ] Удалить namespace, восстановить etcd из бэкапа, проверить, что namespace вернулся
- [ ] Прочитать docs Kubespray об обновлении, выполнить `upgrade-cluster.yml` на минорную версию выше
- [ ] 📸 **Снапшот: `06-upgraded`**

## Песочницы

- [ ] Шаблон песочницы: Namespace + ResourceQuota + LimitRange + NetworkPolicy deny egress + ServiceAccount без токена + под gVisor
- [ ] Ограничить время жизни: `activeDeadlineSeconds` или Job с `ttlSecondsAfterFinished`
- [ ] Скрипт (bash/Python) создания и удаления песочницы по session-id
- [ ] Сохранить шаблоны и скрипт в `artifacts/`
