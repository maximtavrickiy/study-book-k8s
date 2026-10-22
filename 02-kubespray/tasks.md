# 02 Kubespray — практика

## Подготовка

- [ ] 🔙 Откатить k8s-1 и k8s-2 на `00-clean-ubuntu`
- [ ] Проверить по README/docs Kubespray, что выбранная версия (тег релиза) поддерживает **Ubuntu 24.04**; записать версию в `notes.md`
- [ ] **На mgmt:** установить git, python3-venv; создать `.venv` (в `.gitignore`)
- [ ] **На mgmt:** клонировать Kubespray на нужный тег, установить `requirements.txt` в venv
- [ ] **На mgmt:** проверить `ansible all -i <inventory> -m ping`

## Ansible на разминку (на mgmt → k8s-1, k8s-2)

- [ ] Написать свой маленький inventory и playbook: поставить пакет `htop`, создать файл `/etc/motd`
- [ ] Запустить дважды и убедиться в идемпотентности (`changed=0` на втором прогоне)
- [ ] Вынести задачи подготовки узлов (swap, sysctl, modules) в роль
- [ ] Сохранить playbook/роль в `artifacts/`

## Кластер на одном узле (k8s-1)

- [ ] Скопировать `inventory/sample` в `inventory/mycluster`
- [ ] Заполнить `hosts.yaml`: k8s-1 в `kube_control_plane`, `etcd`, `kube_node`; указать `ip`/`access_ip` = `192.168.56.11` (адаптер Host-only!)
- [ ] Проверить/задать `container_manager: containerd`, `kube_network_plugin` (начнём с `calico`)
- [ ] Просмотреть переменные аддонов, ничего лишнего не включать
- [ ] Скопировать inventory (без секретов) в `infra/inventory/`
- [ ] **На mgmt:** `ansible-playbook -i inventory/mycluster/hosts.yaml -b cluster.yml`, сохранить время и итоговый лог в `notes.md`
- [ ] Забрать `admin.conf` на mgmt как kubeconfig (**не коммитить**), `kubectl get nodes`
- [ ] Посмотреть на k8s-1: static pods в `/etc/kubernetes/manifests`, etcd (systemd-сервис или под?), `crictl ps`
- [ ] 📸 **Снапшот k8s-1: `02-kubespray-1node`**

## Добавление k8s-2

- [ ] Добавить k8s-2 в `hosts.yaml` в группу `kube_node`
- [ ] **На mgmt:** выполнить `scale.yml` (ограничив `--limit=k8s-2`, если это рекомендуют docs вашей версии)
- [ ] Проверить `kubectl get nodes`, запустить Deployment на 4 реплики и увидеть поды на обоих узлах
- [ ] 📸 **Снапшот k8s-1, k8s-2: `02-kubespray-2nodes`**

## Эксперименты

- [ ] Остановить etcd на k8s-1 и посмотреть, что работает, а что нет (`kubectl get`, уже запущенные поды); вернуть
- [ ] Выключить k8s-2 и наблюдать статус узла и судьбу подов (через сколько поды переедут?)
