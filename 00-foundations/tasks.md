# 00 Foundations — практика

## Подготовка стенда (VirtualBox)

- [ ] Проверить на хосте, включены ли Hyper-V / WSL2 / VBS; записать в `notes.md`
- [ ] Создать Host-only сеть `192.168.56.0/24` в VirtualBox
- [ ] Создать VM `mgmt`, `k8s-1`, `k8s-2` по таблице из `infra/README.md` (адаптер 1 NAT, адаптер 2 Host-only)
- [ ] Установить Ubuntu 24.04 Server minimal, OpenSSH включён, без Docker и snap-пакетов
- [ ] Настроить статические IP через netplan, сохранить конфиг в `infra/netplan/`
- [ ] Проверить уникальность hostname и `/etc/machine-id` на всех VM
- [ ] **На mgmt:** сгенерировать SSH-ключ и разложить на k8s-1, k8s-2 (`ssh-copy-id`)
- [ ] **На k8s-1, k8s-2:** sudo без пароля для своего пользователя
- [ ] **На k8s-1, k8s-2:** выключить swap, включить `net.ipv4.ip_forward=1`, загрузить `overlay` и `br_netfilter` (с сохранением после перезагрузки)
- [ ] Перезагрузить узлы и проверить, что настройки сохранились
- [ ] 📸 **Снапшот всех VM: `00-clean-ubuntu`** (до установки containerd)

## Контейнер без Docker (на k8s-1)

- [ ] Установить containerd и runc (из пакетов Ubuntu или с GitHub-релизов), записать, откуда и какие версии
- [ ] Скачать образ через `ctr image pull docker.io/library/alpine:latest`
- [ ] Запустить контейнер через `ctr run` (или поставить `nerdctl` и запустить через него)
- [ ] Найти PID процесса контейнера на хосте (`ps`, `ctr task ls`)
- [ ] Сравнить `lsns -p <PID>` с `lsns -p $$` (своя оболочка): какие namespaces разные
- [ ] Посмотреть `/proc/<PID>/cgroup` и найти каталог процесса в `/sys/fs/cgroup`
- [ ] Прочитать `memory.max`, `cpu.max` контейнера; запустить контейнер с лимитом памяти и убедиться, что значение поменялось
- [ ] Зайти в namespaces контейнера с хоста через `nsenter`
- [ ] Внутри контейнера выполнить `uname -a` и сравнить с хостом (запомнить для модуля 05)
- [ ] Найти, где лежат слои образа (snapshotter overlayfs), посмотреть `mount | grep overlay`
- [ ] Сохранить полезные выводы в `artifacts/`
- [ ] 🔙 Откатить k8s-1 на `00-clean-ubuntu` (containerd для k8s поставит k3s / Kubespray)
