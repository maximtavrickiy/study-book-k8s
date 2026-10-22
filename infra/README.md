# Стенд

## Хост

- ОС: Windows, гипервизор: **VirtualBox**.
- CPU: Intel i5-12400F (6 ядер / 12 потоков), RAM: 32 ГБ.
- ⚠️ Машину **192.168.21.105** (отдельный приватный сервер) **не трогаем**. Весь стенд живёт в VirtualBox.
- ⚠️ Включённые Hyper-V / WSL2 / Virtualization-Based Security заставляют VirtualBox работать через Hyper-V API и заметно его замедляют. Проверить и записать в `notes.md`, что включено на хосте.

## Сеть

| Адаптер | Тип | Назначение |
|---|---|---|
| 1 | NAT | доступ в интернет |
| 2 | Host-only, `192.168.56.0/24` | связь VM между собой и с хостом, статические IP |

Конфиги netplan хранить в [`netplan/`](netplan/).

## VM

ОС: **Ubuntu 24.04 Server minimal**, без Docker и snap-версий пакетов, OpenSSH включён.

| VM | Роль | vCPU | RAM | Диск | IP |
|---|---|---|---|---|---|
| mgmt | Ansible, Kubespray, kubectl, git | 1 | 2 ГБ | 20 ГБ | 192.168.56.10 |
| k8s-1 | control plane + worker | 4 | 8 ГБ | 40 ГБ | 192.168.56.11 |
| k8s-2 | worker (добавим позже) | 2 | 6 ГБ | 30 ГБ | 192.168.56.12 |

## Подготовка узлов перед Kubespray

- [ ] swap выключен (`swapoff -a` + убрать из `/etc/fstab`)
- [ ] `net.ipv4.ip_forward=1` (через `/etc/sysctl.d/`)
- [ ] модули ядра `overlay` и `br_netfilter` (через `/etc/modules-load.d/`)
- [ ] уникальные hostname и `/etc/machine-id` (важно при клонировании VM)
- [ ] SSH-ключ с mgmt на k8s-1 и k8s-2
- [ ] sudo без пароля для пользователя Ansible
- [ ] проверить по README и docs Kubespray, что выбранная версия поддерживает **Ubuntu 24.04**

Inventory Kubespray хранить в [`inventory/`](inventory/) (без секретов).

## Снапшоты

Снапшоты VirtualBox **не хранятся в git**. В `notes.md` модуля записываем только имя снапшота и что в нём.

Соглашение об именах: `NN-описание`, например:
- `00-clean-ubuntu` — чистая Ubuntu после подготовки
- `01-k3s-done` — k3s установлен на k8s-1

## Ограничения

- **Kata Containers** в VirtualBox скорее всего не заработает (нужна вложенная виртуализация), в основной план не входит.
- gVisor с платформой KVM тоже требует вложенной виртуализации, в стенде используем `systrap`.

## Позже

Описать стенд кодом в [`vagrant/`](vagrant/) (Vagrant/Packer), см. `99-backlog/ideas.md`.
