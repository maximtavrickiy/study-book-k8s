# 05 gVisor sandboxes — практика

Исходная точка: рабочий кластер, снапшот `04-gitops-done`.

## runsc без Kubernetes (на k8s-1)

- [ ] Найти в docs своей версии Kubespray, где включается gVisor (`gvisor_enabled`: в каком файле group_vars), записать в `notes.md`
- [ ] **На k8s-1:** посмотреть текущий `/etc/containerd/config.toml`, найти секцию runtimes
- [ ] (Опционально) Поставить `runsc` вручную и запустить контейнер через `ctr run --runtime io.containerd.runsc.v1`, чтобы увидеть механику до Kubespray

## Включение gVisor в кластере

- [ ] 📸 **Снапшот перед изменениями: `05-before-gvisor`**
- [ ] В inventory включить gVisor (`gvisor_enabled: true`), перекатить кластер с mgmt
- [ ] **На k8s-1, k8s-2:** проверить, что `runsc` установлен и в `config.toml` появился runtime handler; записать имя handler'а
- [ ] Проверить, какая платформа используется (ожидаемо `systrap`), и почему KVM недоступен в VirtualBox
- [ ] Создать `RuntimeClass` `gvisor` (или проверить, что его создал Kubespray), `handler` должен совпадать с containerd
- [ ] Сохранить манифест RuntimeClass в `artifacts/`

## Сравнение подов

- [ ] Запустить обычный под и под с `runtimeClassName: gvisor` (один образ, например `alpine` / `busybox`)
- [ ] В обоих выполнить `uname -a` и `dmesg`, сравнить вывод; сохранить в `artifacts/`
- [ ] Сравнить `cat /proc/cpuinfo`, `mount`, `ls /proc`
- [ ] На узле найти процессы обоих подов (`ps aux | grep runsc`), сравнить, что видно с хоста
- [ ] Посмотреть логи runsc (где лежат, как включить debug)
- [ ] Простой бенчмарк: `dd` или цикл syscalls в обоих подах, записать разницу
- [ ] Проверить, что NetworkPolicy из модуля 03 работает и для gVisor-пода

## Прототип песочницы

- [ ] Namespace `sandbox-<id>` + под gVisor + NetworkPolicy deny egress + requests/limits
- [ ] Запустить внутри «недоверенный» скрипт (Python), попробовать выйти в сеть и прочитать что-то с хоста; записать результат
- [ ] 📸 **Снапшот: `05-gvisor-done`**
- [ ] ➡️ После завершения модуля открыть `99-backlog/ideas.md`
