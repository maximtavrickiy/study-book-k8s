# 03 Networking — практика

Исходная точка: кластер из двух узлов, снапшот `02-kubespray-2nodes`.

## Исследование текущей сети (Calico)

- [ ] **На k8s-1, k8s-2:** посмотреть `ip a`, `ip route`; найти интерфейсы Calico и маршруты к pod CIDR другого узла
- [ ] Запустить по поду на каждом узле, `ping` и `curl` между ними
- [ ] Определить режим Calico (IPIP / VXLAN / без инкапсуляции); снять `tcpdump` на адаптере Host-only во время ping и найти инкапсуляцию
- [ ] Создать Service ClusterIP и найти правила kube-proxy (`iptables-save | grep <svc>` или `ipvsadm -Ln`)
- [ ] Создать Service NodePort и открыть его с хоста Windows
- [ ] Из пода проверить DNS: `nslookup <svc>`, `nslookup <svc>.<ns>.svc.cluster.local`, посмотреть `/etc/resolv.conf`
- [ ] Сохранить выводы в `artifacts/`

## NetworkPolicy

- [ ] Создать namespace `sandbox`, под с `curl`
- [ ] Применить политику default deny ingress, проверить, что доступ к поду пропал
- [ ] Применить политику с запретом **всего egress** для пода, проверить: интернет, другие поды, DNS
- [ ] Разрешить только DNS (UDP/TCP 53 к CoreDNS), проверить, что резолвинг работает, а соединения нет
- [ ] Сохранить манифесты политик в `artifacts/`
- [ ] 📸 **Снапшот: `03-calico-netpol`**

## Смена CNI

- [ ] 🔙 Откатить k8s-1, k8s-2 на `00-clean-ubuntu`
- [ ] В inventory поменять `kube_network_plugin` на `flannel`, развернуть кластер заново с mgmt
- [ ] Повторить ping между узлами и `tcpdump` (найти VXLAN)
- [ ] Применить ту же NetworkPolicy и проверить, работает ли она с Flannel; записать вывод
- [ ] Вернуться на Calico (или Cilium, если интересно) для дальнейших модулей; записать выбор в `notes.md`
- [ ] 📸 **Снапшот: `03-cni-final`**
