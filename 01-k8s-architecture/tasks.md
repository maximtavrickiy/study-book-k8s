# 01 K8s architecture — практика

Исходная точка: все VM на снапшоте `00-clean-ubuntu`.

## k3s на k8s-1

- [ ] **На k8s-1:** установить k3s одной командой (официальный install-скрипт), записать версию
- [ ] **На k8s-1:** проверить `systemctl status k3s`, `k3s kubectl get nodes`
- [ ] Посмотреть, какие процессы запущены: где apiserver, etcd (или sqlite/kine), scheduler — в k3s всё в одном бинарнике
- [ ] **На mgmt:** установить `kubectl`, скопировать kubeconfig с k8s-1 (заменить `127.0.0.1` на `192.168.56.11`), **не коммитить его**
- [ ] **На mgmt:** `kubectl get nodes -o wide`, `kubectl get pods -A`
- [ ] 📸 **Снапшот k8s-1: `01-k3s-done`**

## Объекты

- [ ] Создать namespace `lab`
- [ ] Запустить Pod (`nginx`) из YAML-манифеста, посмотреть `kubectl describe pod` и events
- [ ] Создать Deployment на 3 реплики, удалить один под и наблюдать восстановление (reconcile)
- [ ] Изменить образ в Deployment, посмотреть rolling update и `kubectl rollout history/undo`
- [ ] Создать Service типа ClusterIP и проверить доступ из другого пода (`curl`)
- [ ] Создать Ingress (в k3s есть Traefik) и открыть сервис с хоста по IP k8s-1
- [ ] Вынести конфиг nginx в ConfigMap и смонтировать его в под
- [ ] Создать Secret и передать его в под как env; посмотреть, как он хранится (`base64` — не шифрование)
- [ ] Создать PVC (local-path в k3s), записать файл, пересоздать под и проверить, что файл на месте
- [ ] `kubectl get events --sort-by=.lastTimestamp` во время создания пода: проследить шаги scheduler → kubelet
- [ ] Сохранить манифесты в `artifacts/`

## Инструменты

- [ ] Установить k9s на mgmt, пройтись по ресурсам
- [ ] (Опционально) Подключить Lens на хосте Windows через kubeconfig
- [ ] Записать в `notes.md` сравнение k8s vs k3s: что упрощено, что заменено (Traefik, local-path, sqlite/kine, flannel)
